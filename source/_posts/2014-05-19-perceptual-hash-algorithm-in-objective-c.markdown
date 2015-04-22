---
layout: post
title: "Perceptual hash algorithm in objective c"
date: 2014-05-19 17:47:06 +0800
comments: true
categories: IOS Algorithm
---

####此文为借鉴阮一峰2011年和2013年发布的相似图片搜索原理
- 原文已经写得很好了，所以我只是把它整理了一下，学习学习~~

###又名感知哈希算法
- 主要思想是
	- 对每个图片生成一个“指纹”字符串，然后比较不同图片的指纹。结果越接近，就说明图片越相似
- 这种算法的优点是简单快速，不收图片大小缩放的影响
	- 缺点是图片内容不能变更。如果在图片上加几个文字，他就认不出来了
- 因此最佳应用应该是根据缩略图找出原图
<!--more-->
- 算法样例
	- 第一步 缩小尺寸
		- 把图片缩小大8*8的尺寸，总共有64个像素。这一步的作用是去除图片的细节，只保留结构，明暗等基本信息，摒弃不同的尺寸，比例带来的图片差异
	- 第二步 简化色彩
		- 将缩小之后的图片转为64级灰度。也就是说，所有的像素点总共之后64中颜色
	- 第三步 计算平均值
		- 计算所有64个像素的灰度平均值
	- 第四步 比较像素的灰度
		- 把每个像素的灰度，和平均值进行比较。大于或者等于平均值的，记为1；小于平均值，记为0；
	- 第五步 计算hash值
		- 把上一步比较的结果，组合在一起，就构成一个64位的整数，这就是这张图片的指纹。组合的次序并不重要，只要保证所有图片采用同样的次序就行了。
		- hash_value = 127ysje82ewrdfw3(16个数字)
		- 这个值也就是指纹
		- 得到指纹之后就可以对比不同的图片，看看64为中有多少位是不一样的。理论上，这等同与计算”汉明距离“。如果不相同的数据位不超过5，这就说明两张图片很相似；如果大于10，就说明这是两张不同的图片。

###网上其他两种类似的算法
####颜色分布法
- 每张图片都可以生成颜色分布的直方图。如果两种那个图片的直方图很接近，那么就可以认为他们很相似
- 由于任何一种颜色都是有红绿蓝三原色（RGB）构成的，所以可以画出四幅图（三原色直方图和最后合成的直方图）
- 如果每种原色都可以取256个值，那么整个颜色空间共有1600万种颜色（256的三次方）。针对这1600万种颜色比较直方图，计算量实在太大了，因此需要采用简化方法。可以将0～255分成四个区：0～63为第0区，64～127为第1区，128～191为第2区，192～255为第3区。这意味着红绿蓝分别有4个区，总共可以构成64种组合（4的3次方）。
- 任何一种颜色必然属于这64种组合中的一种，这样就可以统计每一种组合包含的像素数量。
- {% img /images/oc_algorithm1.png %}
- 上图是某张图片的颜色分布表，将表中最后一栏提取出来，组成一个64维向量(7414, 230, 0, 0, 8, ..., 109, 0, 0, 3415, 53929)。这个向量就是这张图片的特征值或者叫"指纹"。
- 于是，寻找相似图片就变成了找出与其最相似的向量。这可以用皮尔逊相关系数或者余弦相似度算出。

####内容特征法
- 除了颜色构成还可以从比较图片内容的相似性入手
- 首先
	- 把图片装成一张比较小的灰度图片，假设为50*50像素。然后，确定一个阀值，把灰度图片转成黑白图片
- 其次
	- 如果两张图片很相似，那么他们的黑白轮廓应该是相近的。因此，问题就变成了如何去顶一个合理的阀值，正确的呈现图片中的轮廓
- 因此
	- **前景色和背景色反差越大，轮廓就越明显**
	- 这意味着，如果我们找到一个值，可以使得前景色和背景色格子的“类内差异最小”，或者“类间差异最大”，那么这个值就是理想的阀值
- 后来因为有个如本的学者叫大津展之证明了两个是一样的，可以用他的“大津法”来求阀值
	- 假定一张图片共有n个像素，其中灰度值小于阈值的像素为 n1 个，大于等于阈值的像素为 n2 个（ n1 + n2 = n ）。w1 和 w2 表示这两种像素各自的比重。
		- w1 = n1 / n
		- w2 = n2 / n
	- 再假定，所有灰度值小于阈值的像素的平均值和方差分别为 μ1 和 σ1，所有灰度值大于等于阈值的像素的平均值和方差分别为 μ2 和 σ2。于是，可以得到
		- 类内差异 = w1(σ1的平方) + w2(σ2的平方)
　　		- 类间差异 = w1w2(μ1-μ2)^
	- 可以证明，这两个式子是等价的：得到"类内差异"的最小值，等同于得到"类间差异"的最大值。不过，从计算难度看，后者的计算要容易一些。
	- 下一步用"穷举法"，将阈值从灰度的最低值到最高值，依次取一遍，分别代入上面的算式。使得"类内差异最小"或"类间差异最大"的那个值，就是最终的阈值.
	- 有了50x50像素的黑白缩略图，就等于有了一个50x50的0-1矩阵。矩阵的每个值对应原图的一个像素，0表示黑色，1表示白色。这个矩阵就是一张图片的特征矩阵。

	- 两个特征矩阵的不同之处越少，就代表两张图片越相似。这可以用"异或运算"实现（即两个值之中只有一个为1，则运算结果为1，否则运算结果为0）。对不同图片的特征矩阵进行"异或运算"，结果中的1越少，就是越相似的图片。

###objective c源码

- tphash.h

```
#import <Foundation/Foundation.h>

@interface tphash : NSObject

+ (uint64_t)ptHash:(UIImage*)image;
+ (int)hamdistance:(uint64_t)x with:(uint64_t) y;
+ (UIImage *)scaleImage:(UIImage *)image toSize(CGSize)newSize;
+ (uint64_t *) convertTogreyscale64Array: (UIImage *)i;

@end
```

- tphash.m

```
#import "tphash.h"

@implementation tphash

+ (uint64_t)ptHash:(UIImage *)image{
    image = [self scaleImage:image toSize:CGSizeMake(8,8)];
    uint64_t* imageArray = [self convertTogreyscale64Array:image];
    int sum = 0;
    for(int i = 0; i < 64; i++){
        sum += imageArray[i];
    }
    uint8_t avg = sum/64;
    uint64_t ret = 0;
    for(int i = 0; i < 64; i++){
        if(imageArray[i] >= avg){
            ret++;
        }
        ret <<= 1;
    }
    return ret;
}

+ (int)hamdistance:(uint64_t)x with:(uint64_t) y{
    unsigned dist = 0, val = x^y;
    while (val) {
        ++dist;
        val &= val - 1;
    }
}

+ (UIImage *)scaleImage:(UIImage *)image toSize(CGSize)newSize{
    UIGraphicsBeginIMageContextWithOptions(newSize, NO, 0.0);
    [image drawInRect:CGRectMake(0,0,newSize.width, newSize.height)];
    UIImage *newImage = UIGraphicsBeginImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    return newImage;
}

+ (uint64_t *) convertTogreyscale64Array: (UIImage *)i{
    int kRed = 1;
    int kGreen = 2;
    int kBlue = 4;
    
    int colors = kGreen;
    int m_width = i.size.width;
    int m_height = i.size.height;
    
    uint32_t *rgbImage = (uint32_t *) malloc(m_width * meight * sizeof(uint32_t));
    CGColorSpaceRef colorSpace = CGColorSpaceCreateDeviceRGB();
    CGContextRef context = CGBitmapContextCreate(rgbImage, m_width, m_height, 8, m_width * 4, colorSpace, kCGBitmapByteOrder32Little | kCGImageAlphaNoneSkipLast);
    CGContextSetInterpolationQuality(context, kCGInterpolationHigh);
    CGContextSetShouldAntialias(context, NO);
    CGContextDrawImage(context, CGRectMake(0, 0, m_width, m_height), [i CGImage]);
    CGContextRelease(context);
    CGColorSpaceRelease(colorSpace);
    
    uint8_t *m_imageData = (uint8_t *) malloc(m_width * m_height);
    for(int y = 0; y < m_height; y++) {
        for(int x = 0; x < m_width; x++) {
            uint32_t rgbPixel=rgbImage[y*m_width+x];
            uint32_t sum=0,count=0;
            if (colors & kRed) {sum += (rgbPixel>>24)&255; count++;}
            if (colors & kGreen) {sum += (rgbPixel>>16)&255; count++;}
            if (colors & kBlue) {sum += (rgbPixel>>8)&255; count++;}
            m_imageData[y*m_width+x]=sum/count/4;
        }
    }
    free(rgbImage);
    return m_imageData;
}
@end

```





