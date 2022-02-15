---
layout: post
current: post
cover:  assets/built/images/jekyll-logo.png
navigation: True
title: jekyll 기반의 GitHub Page 생성(5) - gulp를 이용한 CSS 경량화
date: 2022-02-10 10:00:00
tags: [jekyll]
class: post-template
subclass: 'post'
author: In8989
---

{% include jekyll-table-of-contents.html %}


### gulp를 이용한 CSS minified 
jekyll 소스 폴더의 루트에 __gulpfile.js__ 생성
{% raw %}
~~~ javascript
var gulp = require('gulp');

// gulp plugins and utils
var gutil = require('gulp-util');
var postcss = require('gulp-postcss');
var sourcemaps = require('gulp-sourcemaps');
var imagemin = require('gulp-imagemin');

// postcss plugins
var autoprefixer = require('autoprefixer');
var colorFunction = require('postcss-color-function');
var cssnano = require('cssnano');
var customProperties = require('postcss-custom-properties');
var easyimport = require('postcss-easy-import');

gulp.task('images', function() {
    return gulp.src('assets/images/*')
        .pipe(imagemin())
        .pipe(gulp.dest('assets/built/images/'))
});

gulp.task('css', function () {
    var processors = [
        easyimport,
        customProperties,
        colorFunction(),
        autoprefixer({browsers: ['last 2 versions']}),
        cssnano()
    ];

    return gulp.src('assets/css/*.css')
        .pipe(sourcemaps.init())
        .pipe(postcss(processors))
        .pipe(sourcemaps.write('.'))
        .pipe(gulp.dest('assets/built/'))
});
~~~
{% endraw %}

**npm install** 에 사용되는 __package.json__
~~~ json
{
    "name": "blog",
    "description": "",
    "version": "1.0.0",
    "engines": {
        "ghost": ">=1.2.0"
    },
    "license": "MIT",
    "devDependencies": {
        "gulp": "^4.0.2",
        "autoprefixer": "^7.2.6",
        "cssnano": "^3.10.0",
        "graceful-fs": "^4.1.11",
        "gulp-imagemin": "^4.1.0",
        "gulp-postcss": "^7.0.1",
        "gulp-sourcemaps": "^2.6.5",
        "gulp-util": "^3.0.8",
        "minimatch": "^3.0.4",
        "postcss-color-function": "^4.0.1",
        "postcss-custom-properties": "^6.3.1",
        "postcss-easy-import": "^3.0.0"
    },
    "config": {
        "posts_per_page": 25
    }
}
~~~
gulp 실행
~~~ shell
gulp css
~~~
__assets/css__ 디렉토리 안에 있는 파일들을 경량화하여 __assets/built__ 디렉토리에 생성  
실제 호스팅하는 사이트에서 사용할 css는 경량화된 파일들이 담당


###### 참고사이트
> 얼큰우동TV: [https://moon9342.github.io/](https://moon9342.github.io/){:target="_blank"}  
> Jekyll 문서: [https://jekyllrb-ko.github.io/](https://jekyllrb-ko.github.io/){:target="_blank"}
