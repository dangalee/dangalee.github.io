---
layout: post
title: 서버호스팅, node.js, react.js, mongodb 간단히 정리하기
subtitle: FitNation 동적 웹사이트 프로젝트 회고 1
# cover-img: /assets/img/path.jpg
# thumbnail-img: /assets/img/thumb.png
# share-img: /assets/img/path.jpg
tags: [web, node.js, react.js, project, mongodb]
---

<details>
<summary>동적 웹사이트 프로젝트 회고 (열어보기) </summary>

<!-- summary 아래 한칸 공백 두어야함 -->

22년 가을 처음으로 동적웹사이트 프로젝트를 진행했다. <br>
당시 웹 프로젝트에 대해 아무것도 아는 것이 없었던 나는, 기능 하나를 구현하는 것에도 쩔쩔맸다.
물론, javascript 문법, react, node.js, mongodb등 기본적인 언어와 플랫폼의 개념조차 알지 못했다.
<br>
<br>
부끄럽지만, 팀원에게 호스팅이 뭐냐고 물어본 적도 있었다.
<br>
<br>
프로젝트는 아쉽게도 일부 기능만 구현된 채 마무리 되었고, 수업의 일환으로 제출하여야 했던 터라 
남은 기능들은 html과 css를 이용하여 급히 디자인만 했다.
<br>
<br>
당시 프로젝트를 진행하면서 시간 투자를 많이 못한 점, 기본 개념들을 제대로 익히지 못하고 넘어갔던 점,
그리고 애초에 너무 많은 것을 구현하려고 계획했던 점이 아쉬웠다.
<br>
<br>
나 이외에 다른 팀원도 어려움을 겪었기에, 기능들을 나눠서 혼자서 진행하는 것 대신, 4명이 힘을 합해 
하나의 기능씩 완성해도 좋았을 것 같다.
<br>
<br>
프로젝트 주제는 '운동 관리 웹사이트 (Wellness Tracking)"이었다. 사용자는 고객, 트레이너, 그리고 관리자 
총 3가지 유형이 있었다. <br>
대표적인 기능은 회원가입/로그인, 검색 기능(+ 필터링 기능), 라이브스트리밍, 프로그램 업로드, 
방문 기록 확인, 캘린더 등이다.
<br>
<br>
졸업해서 시간 여유가 있는 지금, 이 프로젝트를 혼자 다시 한번 구축해보고자 한다. 
<br>
</details>


**서버호스팅이란?**

서버호스팅이란, 서버를 빌려주는 것을 의미한다.
웹 프로젝트를 개발하고, 일정 비용을 지불하여 이러한 서버호스팅 업체를 통해 서버를 빌려올 수 있다.

모든 컴퓨터는 서버의 역할을 할 수 있고, 흔히 우리가 개발을 하며 로컬 호스팅하는 것이 바로 내 컴퓨터에서 서버 환경을 구성하는 것이다.\
node.js의 경우, express 라이브러리 내의 listen 메소드를 이용하여, 포트번호를 설정하여 내 프로젝트를 특정 서버 환경에 띄울 수 있다.

각기 다른 프로젝트는 각기 다른 서버 환경 (다른 포트번호)가 필요하다. \
이때, 포트번호 앞에 오는 ip주소 (ex. 127.0.0.1)는 항상 동일하다.

하지만, 여러 사람들이 웹 사이트를 방문한다면 서버호스팅 업체를 이용할 필요가 있다. \
개인이 컴퓨터를 계속 켜놓고 관리를 하기 어렵고, 많은 이용객이 있을 시 서버 환경이 불안정해 질 수도 있기 때문이다.
서버를 호스팅할 수 있는 서비스에는 대표적으로 AWS(아마존 웹 서비스) github-page가 있다.\
필자의 블로그 역시 github-page를 통해 배포된 프로젝트이다.

**Node.js**

크롬에서 만든 V8 Javascript엔진으로 빌드 된 자바스크립트 실행 환경이다.\
Javascript란, 기존 html보다 더 다이내믹한 기능들을 구현할 수 있는 프로그래밍 언어이다.

- Non-blocking IO : 이전 작업이 끝나지 않더라도 빠른 순서대로 요청을 처리하며, 일반 서버 대비 요청이 많거나 오래 걸리는 요소가 있어도 서버가 멈추지 않고 작동한다.
- 이와 같은 특징 때문에, SNS나 채팅 서비스 등 수많은 요청이 한 번에 들어오는 서비스 처리에 유리하다.
- react와 함께 사용 시, 한 가지 언어로 전체 웹 페이지를 만들 수 있다.

**React.js**

참고: [React.js란?](https://velog.io/@jini_eun/React-React.js%EB%9E%80-%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC)
React는 웹 프레임워크로, 자바스크립트 라이브러리의 하나로서 사용자 인터페이스(UI)를 만들기 위해 사용된다.

- 컴포넌트 기반 구조: 한 페이지에서 컴포넌트를 조립해서 화면을 구성한다. 컴포넌트 단위로 쪼개져 있어, 전체 코드를 파악하기 용이하다. 컴포넌트를 재 사용하여 코드를 반복해 작성하는 과정을 줄일 수 있다. 이로 인해 코드의 유지 보수 및 관리가 용이하다.
- 웹 사이트 디자인에 편리한 라이브러리를 제공한다.: material-ui와 같은 자바스크립트 라이브러리를 이용하여 디자인 된 테이블을 쉽게 구축할 수 있다.

**Mongodb**

Nosql 비관계형 데이터베이스 관리 시스템으로, node.js처럼 독립적인 서버 프로그램이다. mongodb는 Json과 같은 문서 형식으로 데이터를 저장하여 접근성과 가시성 그리고 읽기 성능이 좋습니다.
mongodb는 모든 쿼리문에 대해 json을 바이너리 형태로 인코딩 한 BSON(Binary-json)을 반환합니다. BSON은 JSON보다 공간을 더 많이 차지하지만, Binary형태이기에 컴퓨터가 더 빨리 읽고 처리할 수 있다.

node.js와 mongodb를 연동하기 위해서는, 외부 모듈이 있어야 한다.
ODM (object data mapping) 라이브러리 중 하나인 mongoose가 대표적이다.

**Restful API**
Rest = Representational state transfer api는 소프트웨어 아키텍처 스타일이다.\
Rest 스타일에는 다음과 같은 규칙이 있다.\
- HTTP URL을 통해서 자원(resource)를 명시할 것
- HTTP 메소드인 get, post, put, delete를 통해 해당 자원에 대한 CRUD(기본적인 데이터 처리 기능인 Create, Read, Update 그리고 Delete)를 적용하는 것

웹개발에서 rest api는 클라이언트와 서버 간의 통신을 원활하게 하는 역할을 담당한다.

예제

server.js
```
const express = require('express');
const bodyParser = require('body-parser');
const app = express();
const port = process.env.PORT || 5000; //5000번 포트로 서버 열기
//노드js 안의 익스프레스 라이브러리를 활용하여 서버 환경 설정해주기

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({extended:true}));

//response응답, 데이터 보내기
app.get('/api/customers', (req, res) => {
    res.send([
        {
            'id' : 1,
            'name': '홍길동',
            'image': 'https://placeimg.com/64/64/1',
            'birthday': '880222',
            'job': '학생'
          },
          {
            'id' : 2,
            'name': '이순신',
            'image': 'https://placeimg.com/64/64/2',
            'birthday': '880222',
            'job': '학생'
          },
          {
            'id' : 3,
            'name': '대조영',
            'image': 'https://placeimg.com/64/64/3',
            'birthday': '880222',
            'job': '학생'
          }

    ])
});
//서버가 동작 중이면 동작 중이라고 출력
app.listen(port, () => console.log(`Listening on port ${port}`))
```

app.js
```
import logo from './logo.svg';
import './App.css';
import './muiStyle.css';
import React, {Component} from 'react'; //component사용 시 import 필수
import Paper from '@mui/material/Paper';
import Customer from './components/Customer';
import Table from '@mui/material/Table';
import TableRow from '@mui/material/TableRow';
import TableBody from '@mui/material/TableBody';
import TableCell from '@mui/material/TableCell';
//material ui에 가면 더 많은 테이블들에 대한 코드 정보가 있습니다.
import TableHead from '@mui/material/TableHead';
// import {withStyles} from '@mui/styles' react 18에서 사용불가
//App js를 통해 메인 자바스크립트 관리가 가능합니다.
//Index.js를 통해, root를 통해 index.html에서 아래 내용이 등장합니다.



//map 함수를 활용하여 반복, 코드 길이를 줄일 수 있다. key를 사용해야 합니다.
//f12를 눌러서 크롬 브라우저에서 에러 확인 가능


class App extends Component {

  state = {
    //component 내에서 변경 가능
    customers : []
  }
  componentDidMount() {
    this.callApi()
    .then(res => this.setState({customers:res}))
    .catch(err => console.log(err));
  
  }
  //비동기적으로 업무 수행
  callApi = async () => {
    const response = await fetch('api/customers'); //api에서 데이터를 받아와서
    const body = await response.json(); //고객 목록이 json형태로 body변수에 들어감
    return body;//body반환하여, componentdidmount함수에 전달
  }
  render(){
    // const {classes} = this.props;
   return (
    <Paper className = "root">
        {/* const에 정의된 customer에 대하여 알아서 반복해준다. */}
        <Table className = "table">
          <TableHead>
            <TableRow>
            <TableCell>번호</TableCell>
            <TableCell>이미지</TableCell>
            <TableCell>이름</TableCell>
            <TableCell>생년월일</TableCell>
            <TableCell>직업</TableCell>
            </TableRow>
          </TableHead>
        <TableBody>
          {this.state.customers ? this.state.customers.map(c =>
            {return( 
              <Customer 
                key = {c.id}
                id = {c.id}
                image = {c.image}
                name = {c.name}
                birthday = {c.birthday}
                job = {c.job}
                />
            )} ) : ""}
  
        </TableBody>

        </Table>
      </Paper>
    
    );
  }
}


export default App;
    /*
    package.json outside of client 폴더
        클라이언트 폴더에서 클라이언트 모듈 생성
    루트 폴드에서는 서버 모듈을 생성하도록 명시
    서버와 클라이언트 즉 백엔드와 프론트엔드를 동시에 시작할 수 있도록 한다.
    */
```