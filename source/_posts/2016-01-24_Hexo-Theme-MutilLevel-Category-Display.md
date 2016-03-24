---
title: Hexo主题实现多级分类显示
categories:
- 前端
- Hexo
tags:
- 前端
- Hexo
date: 2016-01-24 21:46:07
---

# 前言

  最近在搞一个博客，是托管在[github][0]和[gitcafe][1]上的，利用[Hexo][2]生成的。
  之后，发现一个问题，显示的分类都是一级的。而我想要的是：能显示`多级分类`,层次分明`的那样。

# 问题

  >基本主题自带的分类显示都是一级的，如何显示多级?

# 解决方案

  所以，研究了一下，找到了理想的方法，方法如下:

  1. 利用系统的[list_categories([categories], [options])][4]辅助函数生成分类列表;

  2. 利用css实现样式.

# 示例

  说明：我使用的是[jacman][3]主题，以这个主题为例说明。

  1. 在主题文件夹下找到`layout/_widget/category.ejs`文件,内容如下:

  ``` html
  <% if (site.categories.length){ %>
  <div class="categorieslist">
  	<p class="asidetitle"><%= __('categories') %></p>
  		<ul>
  		<% site.categories.sort('name').each(function(item){ %>
  		  <% if(item.posts.length){ %>
  			<li><a href="<%- config.root %><%- item.path %>" title="<%= item.name %>"><%= item.name %><sup><%= item.posts.length %></sup></a></li>
  		  <% } %>
  		<% }); %>
  		</ul>
  </div>
  <% } %>
  ```
  2. 修改内容,利用上面提到的`list_categories([categories], [options])`辅助函数:

  ``` html
  <% if (site.categories.length){ %>
  <div class="category-block">
    <h3 class="asidetitle"><%= __('categories') %></h3>
       <%- list_categories(site.categories) %>
  </div>
  <% } %>
  ```

  3. 修改样式文件
  * 在主题文件夹下找到`source/css/_partial/aside.styl`文件,其他的也可能是`source/css/_partial/sidebar.styl`。反正，能在页面显示即可。

  * 添加新的样式，我的如下：

  ``` css
  //categories
  .category-block>ul>li
    border-bottom 1px solid #ccc
  .category-block li
    margin-bottom 8px
  .category-list
    @media mini
      width 45%
      float left
      margin 0 5% 0 0
    @media tablet
      width 100%
      float none
      margin .5em 0 0
    .categoriy-list-item
      padding .5em 5%
    .category-list-count
      top -.5em
      padding-left .3em
      font-size 75%
      line-height 0
      position relative
      vertical-align baseline
    ul, ol, dl
      list-style none
    ul, ol, dl
      background-color #f9f9fa
      margin-left 20px
      li
        border-bottom 1px dashed #ccc
    .category-list-child
      border-top 1px dashed #ccc
      margin-bottom 8px
  ```

  想实现不同的样式，自己可以修改。

# 效果图

  ![效果图][5]

  [0]:https://github.com
  [1]:https://gitcafe.com
  [2]:https://hexo.io
  [3]:https://github.com/wuchong/jacman
  [4]:https://hexo.io/zh-cn/docs/helpers.html
  [5]:/static/images/20160124214658.png
