---
layout: post
current: post
cover:  assets/built/images/jekyll-logo.png
navigation: True
title: jekyll 기반의 GitHub Page 생성(1) - 환경설정
date: 2022-02-10 10:00:00
tags: [jekyll]
class: post-template
subclass: 'post'
author: In8989
---

{% include jekyll-table-of-contents.html %}

### jekyll 설치
1. [Ruby+Devkit 3.0.3-1 (x64)](https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-3.0.3-1/rubyinstaller-devkit-3.0.3-1-x64.exe) 설치

    Run 'ridk install' to setup.... 체크된 상태로 finish 클릭   
    열리는 커맨드 창에서 base installation 선택

2. bundler 설치하기
~~~ shell
gem install bundler
~~~
3. Jekyll 설치하기

    Jekyll 테마 다운로드 후 원하는 경로에 압축해제 ( C:\blogmaker )  
    해당 경로에서 필요한 gem 설치하기  
    ~~~ shell
    bundler install
    ~~~
   
    로컬 서버 실행, 컴파일
    ~~~ shell
    bundler exec jekyll serve
    ~~~
   
    실행 시 에러 발생 추가하라는 문구가 나옴  
    blogmaker 폴더에 있는 Gemfile을 열어서 __gem 'wdm', '>= 0.1.0'__ 추가
    ~~~ shell
    bundler add webrick
    ~~~

4. 환경변수 설정 ( 윈도우 10 )

    퍼블리싱을 위해서 환경변수 값 추가  
    변수 이름: JEKYLL_ENV  
    변수 값: production
    
    정적페이지를 만들어주는 jekyll 폴더를 blogmaker 라고 만들었다.



###### 참고사이트
> 얼큰우동TV: [https://moon9342.github.io/](https://moon9342.github.io/){:target="_blank"}  
> Jekyll 문서: [https://jekyllrb-ko.github.io/](https://jekyllrb-ko.github.io/){:target="_blank"}
