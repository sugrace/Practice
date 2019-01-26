

*사용모듈 request,cheerio
1)request,Promsie  모듈 사용을통한 비동기 공부
참고[https://qkraudghgh.github.io/node/2016/10/23/node-async.html]

reqeust(요청)는 말그대로 목적지 서버에 request(요청)을 보내고 그에 해당 하는 response 를 받아온다.
우리는 response를 받은 내용을 바탕으로 무언가 작업을 해야한다 하지만 request는 네트워크에 요청을 하고 응답을 받아오기때문에 걸리는시간을 예측 하기 어렵다.(네트워크 상황, request를 처리하는 데이터량이 다른것 등)
이러한 상황에서 우리는 Promise를 사용하여 응답을 모두 받은후에 작업을 처리할수있게된다.


여기서 request를 실행하는 부분은 비동기적인것이고
(request 함수가 실행되면 reqeust를 네트워크에 요청하고
Node.js 의 Event Loop 는 Event Queue 에서 다음작업을 꺼내서 수행하게된다)

예를들어,
const url = "https://www.naver.com";
 request(url, function(){
   //콜백 함수 코드1

})
 request(url, function(){
   //콜백 함수 코드2

})
 request(url, function(){
   //콜백 함수 코드3

})
console.log("끝");
이란 코드가 있을때

3개의 request Event가 차례로 Event Queue
에들어가서 Event Loop 에 의해 실행 되게 되지만, 
request 에대한 response 가 도착하여 콜백 함수가 실행되는순서는 (콜백함수코드1이 먼저실행되는지) 네트워크 환경에따라 다를수있기때문에 보장 받지못한다.
또한 이러한 코드는 콜백함수가 실행되기도전에
console.log("끝")이라는 코드가 먼저 실행되고 
request 들이 끝나는 순서대로 콜백함수가 실행된다.

우리는 3개의 request에대한응답을 모두 받고 console.log("끝") 을 실행하고싶기때문에 
promise를 사용하여 비동기적인 request 들을 동기적으로 
수행할수있게 해주는것이다.


app5.js는 과제1의 완성된 코드인데 이코드의 시작점은 37번째줄이다.getdata().then(콜백함수 ) 
은 getdata()가 반환하는 Promise 가 reslove 하게되면 (promise 객체안에서 resolve()가수행이되면  )
.then() 안의 콜백함수가 호출됩니다.
*) new Promise() 하게되면 Promise를 생성하고 Promise 객체를반환한다. 따라서 return new Promise()하면 Promise를 반환한다.


87번째 줄에 Promise.all(My_Promise).then(실행되는 콜백함수) 는
My_Promise 배열안에  모든 Promise 들이 resolve()후 fulfilled(이행)상태가 된다면 then() 안의 콜백함수를 호출한다.

2)cheerio 의 사용법


jquery 링크
https://www.youtube.com/watch?v=EQ48ZpnN3ug&list=PLrCCNh6y7w2g6U7RX_v-TOefyRPiO32jT

cheerio 링크
[참고]http://onemooon.tistory.com/entry/NODE-JS-cheerio-%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4%EC%84%9C-html-%EC%9D%84-%ED%8C%8C%EC%8B%B1%ED%95%B4%EB%B3%B4%EC%9E%90







