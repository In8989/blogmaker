---
layout: post
current: post
cover:  assets/built/images/github.png
navigation: True
title: GitHub(2) - 브랜치(Branch) 관리
date: 2022-02-10 10:00:00
tags: [command]
class: post-template
subclass: 'post'
author: In8989
---

{% include github-table-of-contents.html %}

### GitHub 브랜치(Branch) 관리

* __branch__   
    ~~~ shell
    # branch 만들기
    git branch 브랜치명
    # 브랜치 확인하기 ( 현재 HEAD가 있는 브랜치 앞에 * 로 표시 됨 )
    git branch
  
    # branch 선택하기 ( 선택한 branch로 HEAD 옮기기 )
    # 파일에 사용하면 Modified -> Unmodifed 상태로 변경
    # 브랜치에 사용하는 경우 브랜치간 전환
    git checkout 브랜치명
    ~~~

* __merge__ 와 __rebase__  
    병합하는 기능은 같지만 commit log의 형태가 다르다
    ~~~ shell
    # HEAD가 있는 곳으로 병합
    git merge 브랜치명

    # HEAD가 있는 곳으로 병합
    git rebase 브랜치명
    ~~~

###### 참고사이트
> ZeroCho TV: [https://www.zerocho.com/](https://www.zerocho.com/){:target="_blank"}
