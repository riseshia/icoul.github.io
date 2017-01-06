---
layout: post
title: "bitnami WAMP 설치하기" 
category: mySQL
---

## bitnami WAMP에 대해서

WAMP는 bitnami에서 제공하는 일종의 패키지이다.  
TOMCAT, mySQL, PHP를 포함한 것으로 웹사이트를 만드는데 필요한 서버, 데이터베이스, 프로그래밍 언어를 하나로 통합하여 제공하는 아주 편리한 패키지이다.  
보통은 APM으로 작업하지만 왠지 APM사이트가 404가 뜨고 들어가지지 않는 관계로 WAMP로 작업하였다.  

## bitnami WAMP 설치하기

![친절한 스크린샷](/images/wamp_download.jpg)  
  
다운받는 방법은 심플하다 bitnami 사이트에 접속하여 wamp를 다운받기만 하면 된다.  
그 과정에서 아이디를 만들어서 더 많은 혜택을 제공받으라고 어쩌고 저쩌고 하는데  
좌측 하단 버튼을 통해 가볍게 무시하고 다운로드 받는다.  
  
이 후 별다른 세팅 없이 설치를 진행하면 된다.  
  
![친절한 스크린샷](/images/wamp_install_01.png)  
  
단, 이 때 설정하는 비밀번호는 향후 사용할 mySQL의 비밀번호이므로 꼭 기억해두자.  
기본 계정명은 root이다.  
  

설치가 끝나면 설치폴더에서 `manager-windows.exe` 파일을 실행시키고  
`Open phpMyAdmin`을 통해 phpMyAdmin에 접속해본다.  
이 때 유저명은 root, 비밀번호는 방금 설치 시 설정했던 비밀번호를 입력한다.  
  
  ![친절한 스크린샷](/images/wamp_install_02.png)  
  
이상과 같이 접속이 된다면 mySQL 설치는 끝난 것이다.