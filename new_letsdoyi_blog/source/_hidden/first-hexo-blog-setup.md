---
title: 첫 블로그 셋업, hello world
date: 2019-04-27 23:57:04
tags:
  - hexo
  - blog
categories:
  - Playground
---

꼬박 2일이 걸린 것 같다 🤯
많은 시행착오를 거쳐 블로그를 셋업했다
처음 써보는 Terminal commands과 Git 에 대해 조금씩 적응하고 있다
다음 번에는 blog setup 에 대한 상세한 내용(Hexo 설치, 깃허브 연결 및 배포, 테마 적용)들에 대해 정리해보겠다

<!-- more -->

Terminal commands와 Git에 대한 이해도 레벨업!

- Terminal로 Hexo 설치하는 과정에서 에러가 발생 (MacAir)

  ```terminal
  npm install -g hexo-cli //hexo 공식 설치방법
  //npm WARN checkPermissions Missing write access to /usr/local/lib/node_modules/npm//에러발생

  ```

  해결, 관리자 권한으로 설치

  ```terminal
  sudo npm install -g hexo-cli //해결, 관리자 권한(sudo)으로 설치
  ```

- Git Hub와 연결, Repository 생성
