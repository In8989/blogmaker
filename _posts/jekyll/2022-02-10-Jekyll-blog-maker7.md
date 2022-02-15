---
layout: post
current: post
cover:  assets/built/images/jekyll-logo.png
navigation: True
title: jekyll 기반의 GitHub Page 생성(7) - lunr.js를 이용한 검색 기능
date: 2022-02-10 10:00:00
tags: [jekyll]
class: post-template
subclass: 'post'
author: In8989
---

{% include jekyll-table-of-contents.html %}


### lunr.js를 이용한 검색 기능
Jasper2 theme가 가지고 있는 subscribe 화면을 수정해서 search 기능을 구현하기
1. **_includes/site-nav.html**  파일에서 subscribe 글자를 search 로 수정

2. **_includes/default.html** 을 열어서 검색화면으로 수정

   {% raw %}
    ~~~ html
    <!-- The big email subscribe modal content -->
    {% if site.subscribers %}
    <div id="subscribe" class="subscribe-overlay">
        <a class="subscribe-overlay-close" href="#"></a>
        <div class="subscribe-overlay-content">
            {% if site.logo %}
            <img class="subscribe-overlay-logo"
                 src="{{ site.baseurl }}{{ site.logo }}"
                 alt="{{ site.title }}" />
            {% endif %}
            <h1 class="subscribe-overlay-title">Search {{ site.title }}</h1>
            <p class="subscribe-overlay-description">
                lunr.js를 이용한 posts 검색 </p>
            {% include subscribe-form.html placeholder="keyword" %}
        </div>
    </div>
    {% endif %}
    ~~~
   {% endraw %}

3. **_includes/subscribe-form.html** 수정

    검색어 입력 시 search.html에 검색 결과 출력하는 코드
    
    {% raw %}
    ~~~ html
    <span id="searchform" method="post" action="/subscribe/" class="">
        <input class="confirm" type="hidden" name="confirm"  />
        <input class="location" type="hidden" name="location"  />
        <input class="referrer" type="hidden" name="referrer"  />
    
        <div class="form-group">
            <input class="subscribe-email" onkeyup="myFunc()" 
                   id="searchtext" type="text" name="searchtext"  
                   placeholder="Search..." />
        </div>
        <script type="text/javascript">
            function myFunc() {
                if(event.keyCode == 13) {
                    var url = encodeURIComponent($("#searchtext").val());
                    location.href = "/search.html?query=" + url;
                }
            }
        </script>
    </span>
    ~~~
    {% endraw %}

4. root에 **search.html** 생성 ( 결과페이지 )

   {% raw %}
    ~~~ html
    ---
    layout: page
    current: search
    title: Search Result
    navigation: true
    logo:
    class: page-template
    subclass: 'post page'
    ---
    
    <form action="/search" method="get" hidden="hidden">
        <label for="search-box"></label>
        <input type="text" id="search-box" name="query">
    </form>
    
    <ul class="mylist" id="search-results"></ul>
    
    <script>
        window.store = {
        {% for post in site.posts %}
        "{{ post.url | slugify }}": {
            "title": "{{ post.title | xml_escape }}",
                "author": "{{ post.author | xml_escape }}",
                "category": "{{ post.category | xml_escape }}",
                "content": {{ post.content | strip_html | strip_newlines | jsonify }},
            "url": "{{ post.url | xml_escape }}"
        }
        {% unless forloop.last %},{% endunless %}
        {% endfor %}
        };
    </script>
    <script src="assets/js/lunr.js"></script>
    <script src="assets/js/search.js"></script>

    ~~~
   {% endraw %}

5. __assets/js__ 에 __lunr.js__와 __search.js__ 복사
   
   [lunr.js]({{ site.baseurl }}assets/js/lunr.js){:target="_blank"} 내용 복사해서 저장  
   __search.js__
   
    {% raw %}
    ~~~ javascript
    (function() {
        function displaySearchResults(results, store) {
            var searchResults = document.getElementById('search-results');
    
            if (results.length) { // Are there any results?
                var appendString = '';
    
                for (var i = 0; i < results.length; i++) {  // Iterate over the results
                    var item = store[results[i].ref];
                    appendString += '<li><a href="' + item.url + '"><h6>' + item.title + '</h6></a>';
                    appendString += '<p>' + item.content.substring(0, 150) + '...</p></li>';
                }
    
                searchResults.innerHTML = appendString;
            } else {
                searchResults.innerHTML = '<li>검색 결과가 없습니다.</li>';
            }
        }
    
        function getQueryVariable(variable) {
            var query = window.location.search.substring(1);
            var vars = query.split('&');
    
            for (var i = 0; i < vars.length; i++) {
                var pair = vars[i].split('=');
    
                if (pair[0] === variable) {
                    return decodeURIComponent(pair[1].replace(/\+/g, '%20'));
                }
            }
        }
    
        function trimmerEnKo(token) {
            return token
                .replace(/^[^\w가-힣]+/, '')
                .replace(/[^\w가-힣]+$/, '');
        };
    
        var searchTerm = getQueryVariable('query');
    
        if (searchTerm) {
            document.getElementById('search-box').setAttribute("value", searchTerm);
    
            // Initalize lunr with the fields it will be searching on. I've given title
            // a boost of 10 to indicate matches on this field are more important.
            var idx = lunr(function () {
                this.pipeline.reset();
                this.pipeline.add(
                    trimmerEnKo,
                    lunr.stopWordFilter,
                    lunr.stemmer
                );
                this.field('id');
                this.field('title', { boost: 10 });
                this.field('author');
                this.field('category');
                this.field('content');
            });
    
            for (var key in window.store) { // Add the data to lunr
                idx.add({
                    'id': key,
                    'title': window.store[key].title,
                    'author': window.store[key].author,
                    'category': window.store[key].category,
                    'content': window.store[key].content
                });
    
                var results = idx.search(searchTerm); // Get lunr to perform a search
                displaySearchResults(results, window.store); // We'll write this in the next section
            }
        }
    })();
    ~~~
    {% endraw %}



###### 참고사이트
> 얼큰우동TV: [https://moon9342.github.io/](https://moon9342.github.io/){:target="_blank"}  
> Jekyll 문서: [https://jekyllrb-ko.github.io/](https://jekyllrb-ko.github.io/){:target="_blank"}
