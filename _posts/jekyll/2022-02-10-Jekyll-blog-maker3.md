---
layout: post
current: post
cover:  assets/built/images/jekyll-logo.png
navigation: True
title: jekyll 기반의 GitHub Page 생성(3) - 작성글 목록 보기
date: 2022-02-10 10:00:00
tags: [jekyll]
class: post-template
subclass: 'post'
author: In8989
---

{% include jekyll-table-of-contents.html %}

### 작성글 전체 보기  
jekyll 소스 폴더의 루트에 __archive.md__ 생성
{% raw %}
~~~ markdown
---
layout: page
current: archive
title: All Posts
navigation: true
logo:
class: page-template
subclass: 'post page'
---

<div class="well article">
{%for post in site.posts %}
    {% unless post.next %}
        <h2>{{ post.date | date: '%Y' }}</h2>
        <ul>
    {% else %}
        {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
        {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
        {% if year != nyear %}
            </ul>
            <h3>{{ post.date | date: '%Y' }}</h3>
            <ul>
        {% endif %}
    {% endunless %}
    <li><span class="post-date">
        {% assign date_format = site.date_format.archive %}
        {{ post.date | date: '%Y-%m-%d' }} </span><a href=".{{ post.url }}" target="_blank">{{ post.title }}</a></li>
{% endfor %}
</ul>
</div>
~~~
{% endraw %}
### 작성글 태그별 전체 보기
jekyll 소스 폴더의 루트에 __author_archive.md__ 생성
{% raw %}
~~~ markdown
---
layout: page
current: archive
title: All Tags
navigation: true
logo:
class: page-template
subclass: 'post page'
---

<div id="post-index" class="well article">
{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
{% assign tags_list = site_tags | split:',' | sort %}

<ul class="entry-meta inline-list">
  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tags_list[item] | strip_newlines }}{% endcapture %}
  	<li><a href="#{{ this_word }}" class="tag"><span class="term alltags">{{ this_word }}</span> <span class="count alltags">{{ site.tags[this_word].size }}</span></a></li>
  {% endunless %}{% endfor %}
</ul>

{% for item in (0..site.tags.size) %}{% unless forloop.last %}
{% capture this_word %}{{ tags_list[item] | strip_newlines }}{% endcapture %}
<article>
<h2 id="{{ this_word }}" class="tag-heading">{{ this_word | upcase }}</h2>
<ul>
{% for post in site.tags[this_word] %}{% if post.title != null %}
<li class="entry-title"><a href="{{ post.url }}" target="_blank" title="{{ post.title }}">{{ post.title }}</a></li>
{% endif %}{% endfor %}
</ul>
</article>
{% endunless %}{% endfor %}
</div>
~~~
{% endraw %}
### 글 상단 목차 만들기
**_includes/jekyll-table-of-contents.html** 파일 생성
{% raw %}
~~~ html
<span class="table-of-contents-list">무료 개인 블로그 만들기</span>
<ul class="table-of-contents-list">
    <li><a href="./jekyll-blog-maker1">jekyll 기반의 GitHub Page 생성(1) - 환경설정</a></li>
    <li><a href="./jekyll-blog-maker2">jekyll 기반의 GitHub Page 생성(2) - 디렉토리 설명</a></li>
    <li><a href="./jekyll-blog-maker3">jekyll 기반의 GitHub Page 생성(3) - 작성글 목록 보기</a></li>
</ul>
<hr>
~~~
{% endraw %}
목차가 필요한 글에 include 한다

{% raw %}
~~~ markdown
{% include jekyll-table-of-contents.html %}
~~~
{% endraw %}



###### 참고사이트
> 얼큰우동TV: [https://moon9342.github.io/](https://moon9342.github.io/){:target="_blank"}  
> Jekyll 문서: [https://jekyllrb-ko.github.io/](https://jekyllrb-ko.github.io/){:target="_blank"}
