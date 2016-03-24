---
title: 多说使用ua-parser-js显示浏览器和系统信息
categories:
- 前端
- 工具
- 多说
tags:
- 前端
- 工具
- 多说
date: 2016-01-27 23:55:31
---

# 前言

  昨天博客接入了评论系统，使用的是国内的[多说][1]。

  之前看到过有些利用该评论系统的有浏览器和系统信息的显示，感觉很不错。

  所以，也想有这样的效果。

# 问题

  多说如何显示浏览器和系统的信息?

# 解决方法

  经过查找，利用[UAParser.js][2]可以实现。

# 步骤

  ## 1. 添加样式

  ``` css
  span.this_ua {background-color: #ccc!important;border-radius: 4px;padding: 0 5px!important;margin: 0 1px!important;border: 1px solid #BBB!important;color: #fff;}
  .this_ua.platform.Windows{background-color: #39b3d7!important;border-color: #46b8da!important;}
  .this_ua.platform.Linux {background-color: #3A3A3A!important;border-color: #1F1F1F!important;}
  .this_ua.platform.Android {background-color: #00C47D!important;border-color: #01B171!important;}
  .this_ua.browser.Chrome{background-color: #5cb85c!important;border-color: #4cae4c!important;}
  .this_ua.browser.Firefox{background-color: #f0ad4e!important;border-color: #eea236!important;}
  .this_ua.browser.IE{background-color: #428bca!important;border-color: #357ebd!important;}
  .this_ua.browser.Opera{background-color: #d9534f!important;border-color: #d43f3a!important;}
  ```

  可以新建一个css文件，在页面中添加引用。

  如自定义显示颜色css请加.this_ua.platform.相关名称（注意大小写）。

  ## 2. 添加js代码

  这段代码最好放在多说js代码之后，可以放在多说js的下面。

  下面两段代码根据需要选择。

  正常加载使用这段代码：

  ``` javascript
  <script type="text/javascript">
    if (typeof DUOSHUO !== 'undefined')hookDUOSHUO_tp();
    else $('[src="http://static.duoshuo.com/embed.js"]')[0].onload=hookDUOSHUO_tp;
    function hookDUOSHUO_tp(){
        var _D_post=DUOSHUO.templates.post
        DUOSHUO.templates.post=function (e,t){
            var rs=_D_post(e,t);
            if(e.agent&&/^Mozilla/.test(e.agent))rs=rs.replace(/<\/div><p>/,show_ua(e.agent)+'</div><p>');
            return rs;
        }
    }
    function show_ua(string){
        $.ua.set(string);
        var sua=$.ua;
        if(sua.os.version=='x86_64')sua.os.version='x64';
        return '<span class="this_ua browser '+sua.browser.name+'">'+sua.browser.name+' | '+sua.browser.version+'</span>'+'<span class="this_ua platform '+sua.os.name+'">'+sua.os.name+' '+sua.os.version+'</span>';
    }
    </script>
  ```

  无刷新加载的请使用下面代码:

  ``` javascript
  <script type="text/javascript">
    if (typeof DUOSHUO !== 'undefined')hookDUOSHUO_tp();
    else $('[src="http://static.duoshuo.com/embed.js"]')[0].onload=hookDUOSHUO_tp;
    var hookDUOSHUO_bl=false;
    function hookDUOSHUO_tp(){
        if(hookDUOSHUO_bl)return;
        else hookDUOSHUO_bl=true;
        var _D_post=DUOSHUO.templates.post;
        DUOSHUO.templates.post=function (e,t){
            var rs=_D_post(e,t);
            if(e.agent&&/^Mozilla/.test(e.agent))rs=rs.replace(/<\/div><p>/,show_ua(e.agent)+'</div><p>');
            return rs;
        }
    }
    function show_ua(string){
        $.ua.set(string);
        var sua=$.ua;
        if(sua.os.version=='x86_64')sua.os.version='x64';
        return '<span class="this_ua browser '+sua.browser.name+'">'+sua.browser.name+' | '+sua.browser.version+'</span>'+'<span class="this_ua platform '+sua.os.name+'">'+sua.os.name+' '+sua.os.version+'</span>';
    }
    </script>
  ```

  ## 3. 引入ua-parser.js库

  ``` html
  <script src="http://faisalman.github.io/ua-parser-js/src/ua-parser.js"></script>
  ```

  可以将库文件下载到本地添加到主题中。

  要先引入jquery库文件。

  引入的`ua-parser.js`库文件必须在多说`embed.js`之后。

  推荐加载多说js代码中：

  ``` javascript
  <script type="text/javascript">
    var duoshuoQuery = {short_name:"<%= theme.duoshuo_shortname %>"};
    (function() {
      var ds = document.createElement('script');
      ds.type = 'text/javascript';ds.async = true;
      ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
      ds.charset = 'UTF-8';
      (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(ds);
      ds = document.createElement('script');
      ds.type = 'text/javascript';ds.async = true;
      ds.src = 'http://faisalman.github.io/ua-parser-js/src/ua-parser.js';
      ds.charset = 'UTF-8';
      (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(ds);
    })();
  </script >
  ```

# 效果图

  ![效果图][4]



[1]:http://duoshuo.com/
[2]:https://github.com/faisalman/ua-parser-js
[3]:http://faisalman.github.io/ua-parser-js/src/ua-parser.js
[4]:/static/images/20160128002958.png
