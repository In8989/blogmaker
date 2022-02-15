---
layout: post
current: post
cover:  assets/built/images/github.png
navigation: True
title: GitHub(1) - 자주쓰는 명령어
date: 2022-02-10 10:00:00
tags: [command]
class: post-template
subclass: 'post'
author: In8989
---

{% include github-table-of-contents.html %}

### GitHub 자주쓰는 명령어

* __remote__  
  원격 저장소를 관리하는 명령어
    ~~~ shell
    # 저장소 주소 등록
    git remote add origin 저장소주소
    # 저장소 주소 확인
    git remote -v
    # 주소 수정
    git remote set-url origin 저장소주소
    ~~~

* __push__  
  원격 저장소(origin)에 로컬 브랜치(master)의 commit을 저장
    ~~~ shell
    git push origin master
    ~~~

* __pull__  
  클라이언트로 내려받는 명령어 ( origin의 내용을 master로 복사 )
    ~~~ shell
    git pull origin master
    ~~~

* __clone__   
  서버의 프로젝트를 내려받는 명령어
    ~~~ shell
    git clone 저장소주소
    ~~~

* __reset__   
  이전 상태로 되돌리기
    ~~~ shell
    # commit 후의 Unmodifed에서 commit 직전의 Staged 상태로
    git reset --soft
    # Unmodified에서 commit 전의 Modified 상태로 ( 기본 옵셥 )
    git reset --mixed
    # Unmodified에서 commit 전의 Unmodified로
    git reset --hard
    
    # HEAD가 현재 commit의 위치
    # ~1 은 commit 1개 전으로 되돌아가기
    git reset HEAD~1
    ~~~

* __revert__   
  reset과 똑같이 되돌아가면서 내용을 새 commit으로 만들어서 저장
    ~~~ shell
    # 현재 HEAD를 취소하고 이전 HEAD로 돌아간다
    git revert HEAD
    ~~~


###### 참고사이트
> ZeroCho TV: [https://www.zerocho.com/](https://www.zerocho.com/){:target="_blank"}
