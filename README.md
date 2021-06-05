# 사용 방법

## 코드 다운받기

현재 프로젝트를 다운받아서 본인의 깃허브에 올립니다. 다음 그림과 같이 Code 탭에서 zip 파일의 형태로 프로젝트를 다운받으실 수 있습니다.

![image](https://user-images.githubusercontent.com/84965194/120553964-1b485200-c434-11eb-9085-6d72425db213.png)

## 깃허브 프로젝트에서 페이지 옵션을 활성화

1. Settings 메뉴를 클릭합니다.
2. 이어서 왼쪽에 Pages 메뉴를 클릭합니다.
3. 우측에 Branch 선택하는 부분에서 master 를 클릭해줍니다. (기본값 None)

![image](https://user-images.githubusercontent.com/84965194/120397342-28513c80-c373-11eb-80fd-09e951d06d00.png)

## \_config.yml 파일에서 정보를 설정

```yml
# Site Settings
locale: "ko-KR" # 언어
title: "Blog" # 블로그 제목
title_separator: "&#124;"
subtitle: "This is my Blog" # 블로그 부제목
name: "Jiseong" # 저자 이름
description: "Jiseong's blog" # 블로그 설명
url: "https://hj-template.github.io/template-github" # 블로그 주소
baseurl: # 블로그용 프로젝트가 아니라 프로젝트 내부에 별도로 블로그 폴더가 있는 경우에 사용 (/blog)
repository: "hj-template/template-github" # <조직 or 사용자명>/프로젝트명
```

```yml
# Site Author
author:
  name: "Jiseong" # 저자 이름
  avatar: "/assets/images/profile.jpg" # 프로필 이미지 추가 후 경로 설정
  bio: "I am an **amazing** person." # 저자 설명
  location: "Republic of Korea" # 국가
  # email: "dgf5820@gmail.com" (밑에 있어서 중복됨)
  links:
    - label: "Email"
      icon: "fas fa-fw fa-envelope-square"
      url: "mailto:dgf5820@email.com"
    - label: "Website"
      icon: "fas fa-fw fa-link"
      # url: "https://your-website.com" 있으면 적으면 됨
    - label: "Twitter"
      icon: "fab fa-fw fa-twitter-square"
      # url: "https://twitter.com/" 있으면 적으면 됨
    - label: "Facebook"
      icon: "fab fa-fw fa-facebook-square"
      # url: "https://facebook.com/" 있으면 적으면 됨
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/"
    - label: "Instagram"
      icon: "fab fa-fw fa-instagram"
      # url: "https://instagram.com/" 있으면 적으면 됨
```

## 루비 설치

아래 링크에 접속해서 두꺼운 글씨로 표시되어있는 버전을 클릭하여 다운받아 설치합니다.
https://rubyinstaller.org/downloads/

![image](https://user-images.githubusercontent.com/84965194/120553752-d7ede380-c433-11eb-953d-c5b2107d79f9.png)

## 번들러 설치

터미널 창을 켜서 번들러를 설치합니다 (windows powershell / git bash ...)

```
$ gem install bundler
$ bundle
```

## 개인 컴퓨터에서 서버를 실행

원래는 포스팅 내용을 업로드 한 다음, 깃허브 블로그를 확인해야 하지만 이렇게 본인 컴퓨터에서 변경 내용을 실시간으로 확인할 수 있습니다.

```
$ jekyll serve –port 4000
```

## 포스팅!!

_posts 폴더 안에 md 확장자 파일로 하나씩 포스팅하시면 됩니다!

***예시***
파일명 : 2010-01-07-post-modified.md

```
---
title: "Post: Modified Date"
last_modified_at: 2016-03-09T16:20:02-05:00
categories:
  - Post Formats
tags:
  - Post Formats
  - readability
  - standard
---

This post has been updated and should show a modified date if used in a layout.

All children, except one, grow up. They soon know that they will grow up, and the way Wendy knew was this. One day when she was two years old she was playing in a garden, and she plucked another flower and ran with it to her mother. I suppose she must have looked rather delightful, for Mrs. Darling put her hand to her heart and cried, "Oh, why can't you remain like this for ever!" This was all that passed between them on the subject, but henceforth Wendy knew that she must grow up. You always know after you are two. Two is the beginning of the end.
```
