---
layout: post
title: "Congiure My octopress blog"
date: 2014-04-09 17:03:02 +0800
comments: true
categories: Octopress
keywords: octopress, blog, markdown, ruby
---

###1.In the _config.yml file
```
default_asides: [asides/recent_posts.html, asides/category_list.html, asides/comment.html, asides/github.html, custom/asides/earth.html]

```

- and 
<!--more-->
```
# ----------------------- #
#   3rd Party Settings    #
# ----------------------- #

# Github repositories
github_user: pbking1
github_repo_count: 3
github_show_profile_link: true
github_skip_forks: true


# Google Analytics
google_analytics_tracking_id:

# Facebook Like
facebook_like: false

# Sina Weibo
sina_weibo_follow_button: true

#comment and share                                                                                    
comment_and_share: true

#share
share: true

#Jiathis
jiathis: true

# duoshuo
duoshuo: true
duoshuo_comments: true
duoshuo_short_name: pbking1
duoshuo_asides_num: 5
duoshuo_asides_avatars: 1
duoshuo_asides_time: 1
duoshuo_asides_title: 1
duoshuo_asides_admin: 0
duoshuo_asides_length: 20

```

- are important.

###2. When overcome the problem that there is a blank near the jiathis button
- the find the file under source/javascripts/octopress.js
- locate the function wrapFlashVideos()

```
function wrapFlashVideos() {
  $('object').each(function(i, object) {
    if( $(object).find('param[name=movie]').length ){
      	$(object).wrap('<div class="flash-video">')
    }
  });
  $('iframe[src*=vimeo],iframe[src*=youtube]').wrap('<div class="flash-video">')
}
```
- add the code ```if(object.attr('id') != "JIATHISSWF")```
```
function wrapFlashVideos() {
  $('object').each(function(i, object) {
	if(object.attr('id') != "JIATHISSWF") {
    	if( $(object).find('param[name=movie]').length ){
      		$(object).wrap('<div class="flash-video">')
    	}
	}
  });
  $('iframe[src*=vimeo],iframe[src*=youtube]').wrap('<div class="flash-video">')
}
```
- and soon the error blank will disappear

###3.We will use 
```
rake generate 
rake deploy
```
- to update the blog

- And use the command 
```
rake new_post["test"]
```
- to create a new post blog article called "test"
- So that you can edit the markdown file in the source/_posts 
- Add the article under the existing content using the markdown syntax

```
rake new_page["about me"]
```
- to create a new tab named "about me"
- And add the following code to finish the change
```
<ul class="main-navigation">
  <li><a href="{{ root_url }}/">Blog</a></li>
  <li><a href="{{ root_url }}/blog/archives">Archives</a></li>
  <li><a href="{{ root_url }}/project">Project</a></li>
  <li><a href="{{ root_url }}/about">About Me</a></li>
</ul>
```
- And we can use the command 
```
rake preivew
```
- to preview the blog in the browser in the address "localhost:4000"
###Only show the abstract of the article on the first page
- Add ``` <!--more-->``` in the article
- Then edit _config.yml in
```
excerpt_link: "read more"
```

###4.if can not push the blog
- The solution is to force a push on the master branch.

- Edit the Rakefile and look for this line:

- `system "git push origin #{deploy_branch}"`
- Alter the line by adding a plus (+) before the #{deploy_branch} tag:

- `system "git push origin +#{deploy_branch}"`
- Run the command

- `rake deploy`
- It should succeed.

- *Undo* the edit you made to the Rakefile!

####5.向Octopress添加JiaThis分享工具及冲突解决
- 在_config.yml底部添加如下配置：
```
# JiaThis
jiathis: true
```

- 修改`source/_include/post/sharing.html`，在最后一行`</div>`前添加如下代码：

```
{% if site.jiathis %}
  <!-- JiaThis Button BEGIN -->
  <div class="jiathis_style">
    <span class="jiathis_txt">分享到：</span>
    <a class="jiathis_button_tsina">新浪微博</a>
    <a class="jiathis_button_googleplus">Google+</a>
    <a class="jiathis_button_renren">人人网</a>
    <a class="jiathis_button_qzone">QQ空间</a>
    <a class="jiathis_button_tqq">腾讯微博</a>
    <a href="http://www.jiathis.com/share" class="jiathis jiathis_txt jiathis_separator jtico jtico_jiathis" target="_blank">更多</a>
    <a class="jiathis_counter_style"></a>
  </div>
  <script type="text/javascript" src="http://v2.jiathis.com/code/jia.js?uid=1334720487296344" charset="utf-8"></script>
  <!-- JiaThis Button END -->
{% endif %}
```

- *解决JiaThis与Octopress冲突*

- Octopress会对所有有movie属性的object标签添加一层形如`<div class="flash-video"><div>`的wrapper，用于视频回放。 
- 实现代码在`source/javascripts/octopress.js`中的wrapFlashVideos()函数：

```
function wrapFlashVideos() {
  $('object').each(function(object) {
    object = $(object);
    if ( $('param[name=movie]', object).length ) {
      var wrapper = object.before('<div class="flash-video"><div>').previous();
      $(wrapper).children().append(object);
    }
  });
  $('iframe[src*=vimeo],iframe[src*=youtube]').each(function(iframe) {
    iframe = $(iframe);
    var wrapper = iframe.before('<div class="flash-video"><div>').previous();
    $(wrapper).children().append(iframe);
  });
}
```
- 这层wrapper即是形成JiaThis分享工具条左下角小白框的原因。我们需要对object做一个判断，过滤掉JiaThis的object。 将wrapFlashVideos()函数改为以下代码即可：

```
function wrapFlashVideos() {
  $('object').each(function(object) {
    object = $(object);
    if (object.attr('id') != "JIATHISSWF") {
      if ( $('param[name=movie]', object).length ) {
  var wrapper = object.before('<div class="flash-video"><div>').previous();
  $(wrapper).children().append(object);
      }
    }
  });
  $('iframe[src*=vimeo],iframe[src*=youtube]').each(function(iframe) {
    iframe = $(iframe);
    var wrapper = iframe.before('<div class="flash-video"><div>').previous();
    $(wrapper).children().append(iframe);
  });
}
```

###6.加入disqus评论

- 把下面这段代码加入到系统原有的disqus_thread.html中，文件在_include/post里面
```
 <div id="disqus_thread"></div>
    <script type="text/javascript">
        /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
        var disqus_shortname = 'pbking1'; // required: replace example with your forum shortname

        /* * * DON'T EDIT BELOW THIS LINE * * */
        (function() {
            var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
            dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
            (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
        })();
    </script>
    <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
    <a href="http://disqus.com" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus</span></a>
```

- 然后再在_config.yml里面加入
```
disqus_short_name: name
disqus_show_comment_count: true
```

###7.add license
- 1.首先`source\_includes\post`目录中添加license.html文件

```
{% if site.post_license %}

<DIV style="font-size:12px;BORDER-BOTTOM: #bbbbbb 1px solid; BORDER-LEFT: #bbbbbb 1px solid; BACKGROUND: #f6f6f6; HEIGHT: 120px; BORDER-TOP: #bbbbbb 1px solid; BORDER-RIGHT: #bbbbbb 1px solid" class=oec2003right> 
<DIV style="MARGIN-TOP: 10px; FLOAT: left; MARGIN-LEFT: 5px; MARGIN-RIGHT: 10px"> 
<IMG alt="" src=xxx.jpg" width=90 height=100></DIV> 
<DIV style="LINE-HEIGHT: 200%; MARGIN-TOP: 10px; COLOR: #000000"> 
作者： <A href="http://pbking1.github.io/">pb</A> <BR> 
出处： <A href="http://pbking1.github.io/">http://pbking1.github.io/</A> 
<BR>本文基于<a target="_blank" title="Creative Commons Attribution 2.5 China Mainland License" href="http://creativecommons.org/licenses/by/2.5/cn/"> 
署名 2.5 中国大陆</a>许可协议发布，欢迎转载，演绎或用于商业目的，但是必须保留本文的署名 
<a href="http://pbking1.github.io/">pb</a>。 </DIV></DIV> 
{% endif %}
```

- 2.在sass\custom\_styles.scss添加如下样式信息来控制版权信息的样式

```
.oec2003right 
{ 
    background: #C3D9FF; 
    height:120px; 
    border:1px solid #BBBBBB; 
}

.oec2003right a:link 
{ 
    color: #0057b6; 
    text-decoration: none; 
} 
.oec2003right a:visited 
{ 
    color: #0057b6; 
    text-decoration: none; 
} 
.oec2003right a:active,a:hover 
{ 
    color: #0057b6; 
    text-decoration: underline; 
}
```

- 3.修改文件`source\_layouts\post.html`
  - add 

```
- { % include post/license.html % }
```
  - int the meta class(去掉{和%之间的空格})

- 4.在_config.yml添加配置项用来控制是否显示页面的版权信息

```
 # Post License
 post_license: true
```


###8.add 3D tag cloud
- download the package first
- 1.Copy the `plugins/category_cloud.rb` to your `octopress/plugins/`;
- 2.Copy the `source/_includes/custom/asides/category_cloud.html` to your `octopress/source/_includes/custom/asides/`;
- 3.Add the `octopress/source/_includes/custom/asides/` in Step 2 to your `default_asides` in your `octopress/_config.yml` file;
- 4.Copy the `source/javascripts/tagcloud.swf` to your `source/javascripts/` folder.
