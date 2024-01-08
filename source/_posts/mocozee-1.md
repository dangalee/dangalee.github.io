---
title: FE 개발일기 [1] 개발 환경
date: 2024-01-08 15:15:36
tags:
---

#### Goal 💡

- Visual studio code란?
- 설치한 VScode Extension 정리하기

[1] Visual studio code란?

> Visual Studio Code, also commonly referred to as VS Code,[12] is a source-code editor developed by Microsoft for Windows, Linux and macOS.[13] Features include support for debugging, syntax highlighting, intelligent code completion, snippets, code refactoring, and embedded Git. Users can change the theme, keyboard shortcuts, preferences, and install extensions that add functionality.

> In the Stack Overflow 2023 Developer Survey, Visual Studio Code was ranked the most popular developer environment tool among 86,544 respondents, with 73.71% reporting that they use it. The survey also found Visual Studio Code to be used more by those learning to code than by professional developers (78% vs. 74%)
> [출처: Wikipedia]

Visual Studio code는 Microsoft에서 개발한 소스 코드 편집 도구로 Windows, Linux 그리고 MacOS 운영체제를 지원합니다. 디버깅, Syntax highlighting, 코드 완성, Snippets(재사용 가능한 코드 부분), 코드 리팩토링 그리고 Git 연동을 지원합니다. 사용자는 테마, 키보드, shortcuts, preferences, 그리고 extensions를 설정할 수 있습니다.

2023년 stack overflow 설문에서 visual studio code는 86,544명의 답변 중 73.71%의 사용률로 가장 인기 있는 개발 환경 도구로 랭킹되었습니다. 특히 Visual Studio code는 전문적인 개발자들보다 코드를 배우는 사용자들이 더 많이 사용한 것으로 나타났습니다.

[2] 설치한 VScode Extension 정리하기

1. <span style='background-color:#f6f8fa'> prettier </span>
   코드 포맷터 (code formatter)로 개발자가 작성한 코드를 Prettier 내의 자체 코드 스타일로 변환합니다. 개발자들 끼리 코드 스타일을 따로 논의할 필요가 없고, 추후 코드 유지 보수에도 용이하다는 장점이 있습니다.

   설정은 VSCode Settings 내 default formatter를 통해 가능합니다.

2. <span style='background-color:#fff5b1'> eslint </span>
   eslint는 es(ecma script 약자, javascript의 표준)와 lint (에러가 있는 코드에 표시를 달아 놓음)를 합친 것입니다. 즉, eslint는 자바스크립트 문법에서 에러를 표시해주는 도구입니다.

   eslint는 코드 검사 기능을 제공하여 에러를 잡아낼 뿐 아니라, 코드 스타일 가이드에 맞지 않는 부분을 찾아냅니다. 이를 통해 개발자는 일관성 있고 양질의 코드를 작성할 수 있습니다.

   또한, eslint는 다양한 플러그인을 제공합니다. 예를 들어, eslint-plugin-react를 통해 react관련 규칙을 추가할 수 있습니다.

3. <span style='background-color:#F7DDBE'> javascript (es6) code sn(snippets) </span>
   Vscode를 위한 자바스크립트 ES6 syntax에 해당하는 코드 스니펫이 포함되어 있습니다. 이를 통해 반복되는 코드 작성을 줄일 수 있습니다.

4. <span style='background-color:#dcffe4'> html css support </span>
   html 요소의 class에서 css 선택자 요소를 쓸 때 자동 완성 기능을 지원합니다. Bootstrap과 같은 거대한 css 프레임워크를 사용할 때 유용합니다.

5. <span style='background-color:#f5f0ff'> live server </span>
   로컬 호스트 서버 시작을 통해 코드 산출물을 보다 즉각적으로 볼 수 있도록 돕는 도구입니다.
