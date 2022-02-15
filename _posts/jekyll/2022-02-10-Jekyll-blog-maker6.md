---
layout: post
current: post
cover:  assets/built/images/jekyll-logo.png
navigation: True
title: jekyll 기반의 GitHub Page 생성(6) - rouge를 이용한 코드 가독성 높이기
date: 2022-02-10 10:00:00
tags: [jekyll]
class: post-template
subclass: 'post'
author: In8989
---

{% include jekyll-table-of-contents.html %}


### rouge를 이용한 코드 가독성 높이기 ( syntax highlighting )
~~~ shell
gem install rouge
~~~
rougify명령을 이용하면 우리가 원하는 스타일의 css 파일을 생성
> 어떤 테마가 있는지 확인하기
> ~~~ shell
> rougify help style
> ~~~
> monokai.sublime 테마로 설치
> ~~~ shell
> rougify style monokai.sublime > assets/css/syntax.css
> ~~~

**_layouts/default.html** 에 생성된 css파일에 대한 링크 추가
~~~ html
<!--  syntax.css  -->
<link rel="stylesheet" href="{{ site.baseurl }}assets/built/syntax.css">
~~~
gulp를 이용해 css task 실행하기  
> 다른 css 파일은 경량화가 잘 되는데 생성한 syntax.css 파일에 에러가 발생한다.
> 경량화 하지 않고 __assets/built/__ 폴더에 넣어 사용하였다.

###### 참고사이트
> 얼큰우동TV: [https://moon9342.github.io/](https://moon9342.github.io/){:target="_blank"}  
> Jekyll 문서: [https://jekyllrb-ko.github.io/](https://jekyllrb-ko.github.io/){:target="_blank"}
