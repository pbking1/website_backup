---
layout: post
title: "HTML5和移动平台的原生应用对比"
date: 2014-05-27 13:17:39 +0800
comments: true
categories: Android html
---

###问题所在
- 當前熱門已極的移动開發，所面臨的卻是一個使用平台與裝置類型極其複雜的開發環境，光就行動平台而言，便同時有Windows、Mac、iOS與Android四大平台；再就CPU機器碼來說，則有Intel與ARM兩大平台；即使是Android平台，開發者可能面對的會是百家爭鳴、大小廠牌林立的複雜狀況。

###哪些App适合用HTML5开发？
- 搜索产品
- 社交产品
- 资讯新闻产品
- 游戏产品

###HTML5的优点
- HTML5最主要的优势就在于它适合**`众多平台`**，从PC浏览器到手机、平板电脑，甚至将来的智能电视。只要设备浏览器支持HTML5，HTML5应用或游戏在该平台中就可以直接运行。
- 如今大部分浏览器
- <img src="/images/internship_zst/compare_1.png">
- 这带来原生应用所没有的优点(注：原生应用通常需要进行重新设计，方能投放至另一个目标操作系统)。若开发者想要将自己的iOS游戏移植到Android平台，他就需要对游戏做出根本性的调整。有了HTML5技术，此过程就会简单许多。
- HTML5可`跨平台`运行
<!--more-->
- Zynga德国工作室的Paul Bakaus(他曾协助公司将此技术植入公司的各款网页和手机游戏中)表示，“推广HTML5技术的理由很多。”

    - 他表示，“一个优点就是我们能够轻松将其推广至手机浏览器。例如，你无需进行安装——这是一大优点。再来就是内容更新和跨平台开发。若你创建的是原生应用，多数情况下你需要分别在Android和iOS平台创建内容，也许还有桌面平台。`基于HTML5技术，你只需要制作一次，就可以将其推广至各平台`。”

- 美国消费者在Apps上花费的时间依然远多于移动Web 
- <img src="/images/internship_zst/compare_2.png">

- 对HTML5移动Web及其他平台感兴趣的开发者比例
- <img src="/images/internship_zst/compare_6.png">


###HTML5的缺点
- 虽然HTML5原先旨在服务各种设备，但我们依然`无法确保其能够顺利适应各种硬件标准。`
- HTML5的运作情况无法预测
- 为保证获得较高质量的内容，我们得在多种设备上测试应用——只有这样我们才能保证应用能够顺利运作。我相信未来我们会看到更多测试工具及更优质的标准，但Android QA依然是HTML5开发的痛处。
- **`声音`**显然在游戏开发中占据重要位置。但遗憾的是，这是HTML5的一大缺陷所在。该平台的可用API相比原生应用环境略逊一筹。
- `浏览器的HTML5兼容性不统一`
- HTML5应用区别于手机原生应用的重要地方在于`其没有统一的应用商店`。这有其利弊，我们需要事先把握。显然投身网络平台的主要优点在于发行和更新内容无 需经过审批过程。和苹果iTunes 不同，HTML5允许开发者随时更新或发行游戏，无需等待平台所有者的回应。
- 开发者对HTML5的几点不满——绿色为满意，红色为不满，从左到右依次为跨平台开发、快速更新、盈利、安全性、碎片化、性能、适时更新、用户体验、发行
    - <img src="/images/internship_zst/compare_7.png">
- 一方面，浏览器市场本身就呈现出“群雄割据”之势；另一方面，很多智能手机用户（尤其是Android用户）**不会及时更新软件**。

    - 即便是最新的浏览器，对HTML5的支持也并不完善——例如我们在近期的一份分析报告中发现，Android上的最新版Chrome浏览器在虽然支持98项HTML5功能，但是也不支持28项功能。

    - 这种不均衡会影响HTML5的跨平台吸引力，而事实上，大量HTML5开发工作依然是致力于桌面环境的。

    - 此外，HTML5在移动领域也面临一些**安全性的问题**，部分原因是HTML5应用与数据的互动方式导致的。“保障HTML5数据的安全是件极其困难的事情。”金说道。

###原生应用的优点
- 可访问手机所有功能（GPS、摄像头）；
- 速度更快、性能高、整体用户体验不错；
- 可线下使用（因为是在跟Web相对地平台上使用的）；
- 支持大量图形和动画; 容易发现（在App Store里面）和重新发现（应用图标会一直在主页上）；
- 应用下载能创造盈利（当然App Store抽取20-30% 的营收）。
 
- 移动应用云计算技术公司Appcelerator的企业策略总监迈克尔•金（Michael King）表示,原生应用的优势用一个词概括就是：`性能`。

    - Appcelerator 提出了“互动性斜坡（The Slope Of Interactivity）”概念，指出HTML5适合那些互动性不太强的应用，例如那些单纯提供网络内容或界面非常简单的应用。然而，如果沿着互动性斜坡上行，那些互动更多的应用就需要原生手段了。

    - 但是，有些设备功能时HTML5做不到的，这往往是因为用户的移动浏览器或浏览器版本不支持HTML5实现那些功能。
    
###原生应用的缺点
- 开发成本高；
- 支持设备非常有限（一般是哪个系统就在哪个平台专属设备上用）；
- 上线时间不确定（App Store审核过程不一）；
- 内容限制（App Store限制）；
- 获得新版本时需重新下载应用更新。



###对比
- 为何从长远来看，HTML5在移动开发领域比原生应用更具优势。
    - 性能差距：HTML5的监管机构W3C已经大大推动了相关标准的制定和移动浏览器对HTML5功能的支持，但是很多性能方面的问题依然没有解决。
    
    - 开发者的心声：我们采访了各种各样的人——从怀疑者、早期使用者到倡导者和先行者，我们向他们提出了同一个问题：“在这场HTML5与原生应用的大争论当中，我们的立场又是什么？”
    - 总体而言，我们发现HTML5正在被越来越多人接受，而一些项目已经证明了它的价值。
    - <img src="/images/internship_zst/compare_3.png">
    - <img src="/images/internship_zst/compare_4.png">
    - <img src="/images/internship_zst/compare_5.png">
- 说到底，HTML5与原生应用在质量上的差别，更多来自于移动开发者运用相关语言的才华和经验，而并非HTML5的局限性
- 你喜欢用什么方法来开发支持多平台的应用？紫色为HTML5、绿色为混合应用、红色为一个原生加一个HTML5、蓝色为原生；从上到下依次为全球化企业、大型企业、中型公司、小公司、初创企业（少于5人）、整体。
    
    - <img src="/images/internship_zst/compare_8.png">
    - HTML5是大型企业打造大量应用的一个重要技术趋势（参见上图）。在全球化企业中，近40%的开发人员表示将采用纯HTML5技术开发多平台应用
- 最近，Business Insider在一份新出炉的报告中分析了HTML5和原生应用的优缺点
    - 在`用户体验及性能方面`，**原生应用要超过HTML5应用**，理由是HTML5依然不能很好地通过所有移动浏览器访问设备原生功能，在打造图形丰富的用户界面和呈现数据方面也存在局限性。
    - 在`跨平台部署成本方面`，**HTML5要占优势**，因为HTML5是Web领域的通用语言，不受设备或操作系统限制。W3C正在接洽汽车、出版和电视行业的公司以推广Web。
    - 在`快速更新和发行控制方面`，**HTML5胜过原生应用**。HTML5的一大优势是开放性——它基于Web，所以没有任何一家公司（如谷歌、苹果、亚马逊或三星）可以充当“掌门人”、放缓更新或者瓜分应用收入。不过，HTML5在支持设备厂商推出的创新手机功能时有点慢。
    - 在`盈利方面`，**原生应用更胜一筹**。苹果App Store和谷歌Google Play等原生应用商店优势明显。而HTML5除了软件开发商各自在线销售应用之外，还没有出现令人信服的盈利模式。
    - 在`编程人才数量方面`，**HTML5占优势**。HTML5、Javascript和CSS都是Web领域的通用语言，而相比之下，iOS工程师比较短缺而且开价昂贵。
    
###网友评论
- **网友A**
    - HTML5 技术开发的 Web 应用应该还是有前途的，应该会随着本身的稳定和设备本身的支持也好，性能增强也好，会越来越普遍。不过当前由于种种条件不是特别的成熟。使得HTML5的发展遇到了一些限制。

    - 当然，要想获得更好的体验，无疑是要用原生的语言来进行应用开发。

    - 从目前来看HTML5，与原生应用，还不存在多大的竞争关系，前者更多的是尝试，一直在成熟中，从将来来看，也应该分领域，比如要求比较高的游戏，是不太可能全用HTML5开发的。 而对于传统领域到移动领域的转型所做的展示类型的应用，可能HTML5更合适一些，满足要求又跨平台。
    
- 网友B
    - 我觉得Web App和Native App是互补的关系，而如果能利用2者的优点制作出Hybrid App那是最好的。
   - 首先说说Web App，从开发成本，适配，还有便捷都是最好的。但是劣势就是在于，HTML5不是很成熟，还有就是对于消息推送，还有调用本地文件能力有点弱。以及在类似中国部分地区网络貌似不是很给力的说。
   - 而Native App在提供用户体验更胜一筹，而且消息推送，调用本地功能【相机、语音等】方便，但因这样就必须针对不同平台提供不同体验。同时开发成本也就高，而且移植到不同平台上也麻烦。最关键就是在于开发的APP是需要审核。
    - 所以如果能利用好HTML5的优点，结合原生态的优点，达到互补用户体验应该可以上一层。

###资料来源
- http://www.cnblogs.com/Better-Me/p/3478973.html
- http://www.ithome.com.tw/pr/87940
- http://mobile.51cto.com/app-show-410661.htm
- http://mobile.51cto.com/comment-386277.htm
- http://mobile.51cto.com/comment-385747.htm
- http://www.infoq.com/cn/news/2013/03/html5-native-mobile
