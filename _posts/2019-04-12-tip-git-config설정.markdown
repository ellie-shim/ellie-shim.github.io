---
layout: post
title: "컴퓨터를 바꾸고 잔디가 심어지지 않을 때..gitconfig 초기 설정"
subtitle: "git config"
categories: tip
tags: tip
comments: true
---

## 우울

윈도우를 쓰다가 맥북으로 넘어온지 한달 반이 지났다.
ssh를 새로 연결하는데 어떻게 하는지 몰라서 검색검색검색 하면서 연결을 성공했다.

그리고... 새로운 organization을 파서 시옷즈들과 토이 프로젝트를 진행했는데 잔디가 잘 심어지기에 문제없는 줄 알았다.

그리고 토이 프로젝트를 잠시 멈추고 포폴사이트와 블로그를 작성하는데 커밋과 푸쉬가 잘 진행됐다.

근 한달 간 잔디를 심기 위해 열심히 커밋을 날렸다. 그런데 지금 확인해보니 잔디가 하나도 심어지지 않는 것,,,,,ㅠㅠ,,ㅠㅠ,ㅠㅠ,,ㅠㅠ,,,흑흑엉ㅇ엉흫ㄱ흑엉엉흑흑엉엉흑흑엉엉흑흑엉엉 나의 한달 나의 커밋

왜 나는 잔디가 잘 심어지고 있는지 미리미리 확인하지 않았는가? (처음엔 반영에 시간이 좀 걸리나보다 싶었다)

그래서 약간 우울했다가 알아보니까.

## gitconfig 초기 설정

gitconfig에 초기설정을 해주어야했던 것이다......

몰라..몰랐어...전에 노트북 쓸 때도 이런걸 설정해주었었나...?흑흑엉엉흑흑엉엉

1. Github에서 `settings - Emails`에 있는 Primary 이메일을 확인 후

1. .gitconfig 파일에 해당 이메일과 github 이름을 적어주면 된다.

```
$ git config --global user.name "ellie-shim"
$ git config --global user.email ellie.shim.s@gmail.com
```

1. 잘 등록됐는지 확인도 해보자.

```
$ git config user.name
ellie-shim
$ git config user.email
ellie.shim.s@gmail.com
```

잘 됐다..이제 커밋을 해보자...쥬ㄹ르르르르륵...내 잔디 돌려줘 엉엉

## 또 다른 문제

푸쉬도 잘 되고 잔디도 잘 심어지는데 문제는, 커밋 내역을 눌렀더니

```
No commits found for "ellie-shim"(using ellie.shim.s@gmail.com"
```

라는 문구가 뜬다..

로컬에서 폴더를 지우고 다시 클론 받아보았다. 잘될깡
