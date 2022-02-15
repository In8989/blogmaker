---
layout: post
current: post
cover:  assets/built/images/github.png
navigation: True
title: GitHub(3) - 유용한 명령어
date: 2022-02-10 10:00:00
tags: [command]
class: post-template
subclass: 'post'
author: In8989
---

{% include github-table-of-contents.html %}

### 유용한 명령어

* __cherry-pick__ 와 __tag__  
  
    ~~~ shell
    # 원하는 commit 한 개 가져오기
    # github에 있는 commit 고유값 ( git log로 확인가능 )
    git cherry-pick 고유값
    
    # commit 에 태그 추가
    git tag -a 태그명
    # commit 에 태그 삭제
    git tag -d 태그명
    
    # cherry-pick, tag 사용하기
    git cherry-pick 태그명

    ~~~

* __fetch__  
    __git pull__ 은 __git fetch + git merge__ 의 기능을 수행  
    
    ~~~ shell
    # 서버의 변경점을 별개의 브랜치로 만드는 것
    # FETCH_HEAD라는 별개의 브랜치에서 변경점을 확인 가능
    git fetch
    ~~~

* __stash__ 와 __unstash__

    ~~~ shell
    # 현재 변경사항 저장, git status 내역 비워짐
    git stash
    # stash 리스트 보기
    git stash list
    # 최근에 저장한 stash 복구
    git stash apply
    ~~~

* __--assume-unchanged__
    수정을 막아야 될 경우, 해당 파일의 추적을 막음  
    ~~~ shell
    # commit한 파일의 수정사항을 반영되지 않게 함
    git update-index --assume-unchanged 파일경로
    # 다시 추적
    git update-index --no-assume-unchanged 파일경로
    # 한 번에 추적
    git update-index --really-refresh
    ~~~


###### 참고사이트
> ZeroCho TV: [https://www.zerocho.com/](https://www.zerocho.com/){:target="_blank"}
