---
layout: post
title: beautiful-jekyll 테마 사용방법
# subtitle: Summarization of https://github.com/daattali/beautiful-jekyll README.md
# cover-img: /assets/img/path.jpg
# thumbnail-img: /assets/img/thumb.png
# share-img: /assets/img/path.jpg
tags: [introduction, review]
---

공부한 내용들을 블로그로 기록하기 위해 블로그를 생성했다. \
html, css와 익숙해질 겸, jekyll의 테마와 github을 사용하여 만들어보기로 결정했다.

### 1. Github Pages 만드는 과정

Step 01: Github repository를 생성한다. 이때 repository의 이름은 반드시 **(username).github.io** 형식이어야 한다.

Step 02. Clone repository to local directory. 
visual studio code를 설치하고, github 주소를 복사해서 ide내에 clone한다. visual studio code와 같은 idE를 이용하면 코드를 한 눈에 볼 수 있을 뿐더러 commit & push 과정이 단순해진다.

Step 03: Jekyll을 이용하기 위하여 Ruby, RubyGems, GCC and Make 설치한다. 참조: [Jekyll Installation](https://jekyllrb.com/docs/installation/)

Step 04: Visual studio code 내에서 terminal을 열어 **gem install jeckyll bundler**를 입력하여 jekyll를 설치한다.

Step 05: terminal 내에서 **jekyll new ./**를 입력하여 jekyll을 생성한다.

Step 06: terminal 내에서 **bundle install** 입력, bundle 설치한다.

Step 07: [beautiful-jekyll 테마 다운로드](https://github.com/daattali/beautiful-jekyll) 에 접속하여 화면 우상단의 <>code 버튼을 누르면 zip 파일을 다운로드 받을 수 있다. 이 후, 압축을 풀어 안에 있는 모든 파일을 github.io local directory에 덮어쓰기 해 준다.

Step 08: local hosting으로 사이트가 잘 출력되는지 확인한다. \ 마찬가지로 terminal 내에서 **bundle exec jekyll serve**를 입력해준다. 과정 중 dependency관련 error가 나오는 경우, 빠져있는 dependencies를 추가로 설치하여 디버깅해준다. 이 때 command는 gem install (dependency_name)이다.

Step 09:  http://127.0.0.1:4000 와 같은 서버 주소를 통해 테마가 잘 적용되었는지 확인해본다.

Step 10: Commit & Push 후 (username).github.io 에 접속, 사이트가 잘 hosting 되는지 확인해본다.

### 2. post 추가 방법

모든 포스트들은 _posts안에 저장되어 있으며, Year-Month-Day-title.md 형식으로 지정해야 한다. html도 사용할 수 있지만 md(마크다운)이 더 빠르고 간단하다. 

#### 참조한 마크다운 Guides

[마크다운 작성법](https://gist.github.com/ihoneymon/652be052a0727ad59601)\
[sample blog post](_posts\2020-02-28-test-markdown.md)\
[hyperlink](https://anvilproject.org/guides/content/creating-links)

모든 md 혹은 html파일은 http://(username).gthub.io/파일명으로 접근할 수 있다.
ex. 이 포스트는 https://dangalee.github.io/2023-05-07-jekyll-theme 로 확인 가능하다.

모든 포스트들은 template적용을 위해 front matter로 시작해야 한다.
> "---" \
> "---" \
> 두 줄 "---" 사이에는 title, subtitle, tags, cover-img, thumbnail-img, comments 등과 같은 변수들을 지정할 수 있다.

tags: 포스트의 category 지정 가능 ex. [personal, travel] \
cover-img, thumbnail-img: 이미지 등록 ex. /(위치)/(사진명).jpg \
comments: 댓글 허용 여부, 그러나 댓글 기능은 comments providers - facebook, disqus, statisman, utterances, giscus, commentbox를 _config.yml에서 허용해야 사용 가능







