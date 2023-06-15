---
layout: post
title: 비동기처리(async, await란 무엇인가)
subtitle: FitNation 동적 웹사이트 프로젝트 회고 3
# cover-img: /assets/img/path.jpg
# thumbnail-img: /assets/img/thumb.png
# share-img: /assets/img/path.jpg
tags: [web, node.js, project]
---

로그인을 구현하며, api를 통해 클라이언트가 입력한 id, 비밀번호가 데이터베이스 내에 존재하는 지 확인하는 작업이 필요했습니다. \
놀랍게도 비동기 처리 asyncHandler, await를 해 주지 않으면 데이터 베이스에 해당 email이 존재하는 지 확인하는 함수 findOne이 null값만을 반환했습니다.

코드는 다음과 같습니다.
```javascript
const asyncHandler = require('express-async-handler') //비동기 처리를 하지 않으면 로그인 진행 불가함  findOne이 항상 null 값을 반환함
//express-async handler를 통해 try~ catch문 없이 비동기 처리를 간단하게 해 줄 수 있다.


app.post('/api/login/', asyncHandler(async (req, res) => {
    const {email,password} = req.body //무슨 값인지 받아오기
    const found = await Users.findOne({email}) //DB에서 해당 이메일/패스워드 찾기
    //await를 이용, Users.findOne()이 해결될 때까지 기다린 후
    //아래 if else문이 작동된다.

    if(found && (await password === found.password)){
        res.json({
            _id: found.id,
            name: found.name,
            username: found.username,
            email: found.email,
            role: found.role
        })
    
    }
    else{
        res.status(400)
        throw new Error('잘못된 아이디/비밀번호 입니다.')
    }
}))
```
그 이유가 궁금해 비동기처리와 동기처리의 차이점에 대해 알아보고자 합니다.

**동기적 처리(Synchronous)**는 시간 순서대로 task를 처리합니다. 작업을 동기적으로 처리할 경우 앞의 작업이 끝날 때 까지 다른 작업을 처리할 수 없습니다.

반면 **비동기처리(Asynchronous)**를 사용할 경우, 동시에 여러 task를 처리할 수 있습니다. 앞의 작업을 기다리며 다른 함수 호출도 가능합니다. 아래에 위치한 코드가 위에 위치한 코드보다 먼저 실행될 수 있습니다.

**async/await**키워드는 비동기 처리를 하기 위한 방법 중 하나입니다.\
async함수 안에서만 await를 사용할 수 있습니다. \
await는 연산 앞에, async는 함수 앞에 붙여줍니다.\
await 키워드를 이용하면 promise로 부터 결과값을 얻을 때 까지 기다려줍니다. (기존 비동기 처리는 기다리지 않고 다음 라인으로 넘어감)

**Promise란?**\
현재 얻을 수는 없지만 가까운 미래에는 얻을 수 있는 데이터에 접근하기 위한 방법을 제공합니다. Promise 타입의 결과값이 리턴되면, 이 결과값으로 다음에 수행할 작업을 진행합니다.

위 코드에서 Users.findOne(email) 앞에 await키워드를 사용해 줌으로서 **다음 라인으로 자동적으로 넘어가지 않고 값을 반환할 때까지 기다린 다음** if~ else구문이 작동되었습니다.
await 키워드를 사용하지 않을 경우 found에 null값이 반환된 채 if else구문으로 들어가 항상 else - 잘못된 아이디/비밀번호입니다 라는 문구만이 생성됩니다.