---
title: Gulp.js基础入门教程
categories:
- 前端
- Gulp
tags:
- 前端
- Gulp
date: 2016-02-04 23:25:29
---
# 安装 Node

>去 [nodejs.org](http://nodejs.org) 根据系统选择性按照教程安装Node。

# 创建项目

* 创建项目文件夹

* 进入项目文件夹

* 初始化项目

   使用npm命令:`npm init`,根据提示完成。


# 安装 Gulp

>进入项目文件夹,使用Node的包管理命令npm进行安装.

* 全局安装

``` shell
npm install -g gulp
```

* 项目依赖中安装

``` shell
npm install --save-dev gulp
```

# 创建Gulp配置文件

* 在项目根目录新建配置文件`gulpfile.js`

# 设置配置信息

>以常见的Gulp插件为例,如下：
>1. js代码校验(gulp-jshint)
>2. 合并js文件(gulp-concat)
>3. 压缩js代码(gulp-uglify)
>4. sass的编译(gulp-sass)
>5. less的编译(gulp-less)
>6. 压缩css(gulp-minify-css)
>7. 重命名(gulp-rename)

这些插件的安装命令如下:

``` shell
npm install gulp-jshint gulp-concat gulp-uglify gulp-sass gulp-less gulp-minify-css gulp-rename --save-dev
```

## 完整配置文件:

``` js
// 引入 gulp
var gulp = require('gulp');

// 引入组件
var jshint = require('gulp-jshint');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var sass = require('gulp-sass');
var less = require('gulp-less');
var minifycss = require('gulp-minify-css');
var rename = require('gulp-rename');

// 检查js脚本
gulp.task('lint', function() {
    gulp.src('./src/js/*.js')
        .pipe(jshint())
        .pipe(jshint.reporter('default'));
});

// 合并,压缩js文件
gulp.task('scripts', function() {
    gulp.src('./src/js/*.js')
        //合并js文件
        .pipe(concat('all.js'))
        //给文件添加.min后缀
        .pipe(rename({ suffix: '.min' }))
        //压缩脚本文件
        .pipe(uglify())
        .pipe(gulp.dest('./dist/js'));
});

// 编译sass
gulp.task('sass', function() {
    gulp.src('./src/scss/*.scss')
        .pipe(sass())
        .pipe(gulp.dest('./css'));
});

// 编译less
gulp.task('sass', function() {
    gulp.src('./src/less/*.less')
        .pipe(less())
        .pipe(gulp.dest('./css'));
});

// 压缩css
gulp.task('style', function() {
    gulp.src('./src/css/*.css')
        .pipe(gulp.dest('./dist/style'))
        .pipe(rename('all.min.css'))
        .pipe(minifycss())
        .pipe(gulp.dest('./dist/style'));
});

// 默认任务
gulp.task('default', function(){
    gulp.run('lint', 'sass', 'scripts');

    // 监听文件变化
    gulp.watch('./src/js/*.js', function(){
        gulp.run('lint', 'scripts');
    });
    gulp.watch('./src/sass/*.scss', function(){
        gulp.run('sass');
    });
    gulp.watch('./src/less/*.less', function(){
        gulp.run('less');
    });
    gulp.watch('./src/css/*.css', function(){
        gulp.run('style');
    });
});
```
