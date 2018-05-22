---
title: gulp实现静态资源版本控制的试验
date: 2018-05-22 15:47:47
type: "tags"
tags: [gulp]
---
   > 最近有个很小的需求大概就两三个页面，但对兼容性及自适应有要求，考虑到这么小的项目没必要用webpack就选择了好久没使用了的gulp进行自动化构建。
   gulp的功能虽然没webpack强大但是胜在小而美，api简单很好上手。


   >**这次主要想试验的是给这个小项目的页面自动生成带有版本号的项目资源**

 ---

 * 试验必备的插件：gulp-rev（给静态文件增加hash值） 、gulp-rev-collector（静态资源的路径替换）

 简单粗暴的直接上代码(gulpfile.js)：

 ```
var gulp = require('gulp');
var rev = require('gulp-rev');
var rename = require('gulp-rename');
var contact = require('gulp-concat');
var cssMin = require('gulp-minify-css');
var uglify = require('gulp-uglify');
var del = require('del');
var gulpSequence = require('gulp-sequence');
revCollector = require('gulp-rev-collector');

var cssSrc = './css/*.css', jsSrc = './js/*.js';

// 压缩css
gulp.task('cssmin', function () {
  return gulp.src(cssSrc)
      .pipe(cssMin())
      .pipe(contact('main.css'))
      .pipe(rename({suffix: '-min'}))
      .pipe(rev())
      .pipe(gulp.dest('./dist/css'))
      .pipe(rev.manifest())
      .pipe(gulp.dest('./dist/json/css/'));
})

// 压缩js
gulp.task('jsmin', function () {
  return gulp.src(jsSrc)
      .pipe(uglify())
      .pipe(rev())
      .pipe(gulp.dest('./dist/js'))
      .pipe(rev.manifest())
      .pipe(gulp.dest('./dist/json/js/'));
})

//Html替换css、js文件版本
gulp.task('revHtml', function () {
  return gulp.src(['./dist/json/*/*.json', '*.html'])
      .pipe(revCollector({
        replaceReved: true,
      }))
      .pipe(gulp.dest('./dist'));
});

// 清空
gulp.task('clean', clean);

function clean() {
  return del(['./dist/*']);
}

// 监控文件变化并自动执行压缩
gulp.task('watch', function () {
  gulp.watch('./css/*.css', ['build'])
  gulp.watch('./js/*.js', ['build'])
})


// 压缩合并
gulp.task('build', function () {
  gulpSequence('clean', 'cssmin', 'jsmin', 'revHtml')()
});

 ```

