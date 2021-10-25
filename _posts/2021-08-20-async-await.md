---
title: 자바스크립트 비동기 처리 (콜백, 프로미스, async await)
layout: post
categories:
- Javascript
author: Leeseokmin
---

먼저 자바스크립트는 싱글스레드이기 때문에 한 번에 하나의 작업만 수행할 수 있습니다.
이것을 해결하기 위해 비동기 처리가 생겼습니다.

컴퓨터 프로그래밍에서 비동기는 주 프로그램 흐름과 무관한 이벤트 발생 및 이러한 이벤트를 처리하는 방법을 뜻합니다.
작업을 동기적으로 처리한다면 이전 작업이 끝날 때까지 다른 작업을 할 수 없고, 실행 작업이 끝나야 다음 예정 작업을 할 수 있습니다.
이를 비동기적으로 처리 한다면 흐름이 멈추지 않고 동시에 여러가지 작업을 처리할 수 있습니다.

자바스크립트에는 콜백함수, Promise, async await 크게 3가지 비동기 방식이 존재합니다.

> 콜백(callback)이란?

* 콜백이란 다른 함수의 전달인자로 넘겨주는 함수를 말합니다.
* 콜백지옥이라는 단어도 몇 번 들어봤을 것입니다.

```
// Callback function
function a(callback) {
  callback()
}
function b() {
  console.log('b: callback')
}
a(b) // b: callback

// Callback hell
a(function(value){
  b(function(value2){
    c(function(value3){
      d(function(value4){
      })
    })
  })
})
```

콜백 함수를 하나만 썼을 때는 코드가 간결하지만, 비동기로 함수의 매개 변수에 다른 콜백 함수가 중첩되어 사용된다면 그 코드를 보기에도 어렵고 유지보수 비용도 많이 들어갑니다.

위 코드(Callback hell)에서 에러를 잡기 위해서는 각 함수마다 에러 처리를 사용해야 하는데 그렇게 되면 코드양이 어마어마해집니다.

> Promise

* Promise는 비동기 처리에 사용되는 객체입니다.
* Promise는 new Promise() 로 생설할 수 있으며, 종료 될 때 세 가지 행태를 가집니다.

  * Pending(대기): 이행하거나 거부되지 않은 초기 상태
  * Fulfilled(이행): 연산이 성공적으로 완료됨
  * Rejected(실패): 연산이 실패함 18000 10000 13600

![promise ](/assets/images/portfolio/promise.png){: .align-center}
[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise){:target="_blank"}

**Pending(대기)**

아래와 같이 new Promise() 메서드를 호출하면 대기(Pending) 상태가 됩니다.
메서드를 호출할 때 콜백 함수를 선언할 수 있고, resolve, reject 2개의 인자를 받으며,
비동기 처리가 성공하면 resolve가 호출되고, 실패하면 reject 가 호출됩니다.

```
const promise = new Promise((resolve, reject) => {
})
```

**Fulfilled(이행)**

콜백 함수의 인자 resolve를 아래와 같이 실행하면 이행(Fulfiled) 상태가 됩니다.

```
const getData = () => {
  return new Promise((resolve, reject) => {
    const data = 100;
    resolve(data);
  });
}

// resolve()의 결과 값 data를 resolvedData로 받을 수 있습니다.
getData().then(resolvedData => {
  console.log(resolvedData); // 100
});
```

**Rejected(실패)**

reject 인자를 아래와 같이 호출하면 실패 상태가 됩니다.

```
const getData = () => {
  return new Promise((resolve, reject) => {
    reject();
  });
}

// 실패한 이유를 catch로 받을 수 있습니다.
getData().then().catch(err =>
  console.log('실패한 이유 ' + err)
);
```

> async await

* ES7(ES2017)에서는 async/await 키워드가 추가되었습니다.
* async 를 함수와 같이 사용하면 결과를 직접 반환하는게 아니라 Promise를 반환하게 합니다. 또한 동기식 함수는 await사용을 위한 지원과 함께 실행되는 잠재적인 오버헤드를 피할 수 있습니다.

```
const asyncFunc = async () => {
  console.log('calling')
  await setTimeout(() => console.log('resolved'), 2000)
}

asyncFunc()
// 위와 같이 실행하면 calling이 찍히고 2초 뒤에 resolved가 찍히는 것을 볼 수 있습니다.

```