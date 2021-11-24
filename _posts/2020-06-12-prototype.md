---
title: 자바스크립트에서 프로토타입(Prototype) 이란?
layout: post
categories:
- Javascript
author: Leeseokmin
---

![자바스크립트](/assets/images/portfolio/js-logo.png){: .align-center}

> 프로토타입(Prototype)

자바스크립트는 프로토타입 기반 언어라고 불립니다.
기본 데이터 타입을 제외한 모든 것이 객체이기 때문입니다.
객체가 만들어지기 위해서는 자신을 만드는데 사용된 원형인 프로토타입 객체를 이용하여 객체를 만드는데 이때 만들어진 객체 안에 _proto_ 속성이 자신을 만들어낸 원형을 의미하는 프로토타입 객체를 참조하는 숨겨진 링크가 있습니다. 이 숨겨진 링크를 프로토타입이라고 정의합니다.
ECMA6 표준에서는 Class 문법이 추가 되었지만, 자바스크립트가 클래스 기반으로 바뀌었다는 것은 아닙니다.

```
let person = {
    type : '인간',
    getType : function(){
        return this.type;
    },
    getName : function(){
        return this.name;
    }
};

let hong = Object.create(person);
hong.name = '길동';

let yang = Object.create(person);
yang.name = '서주'

console.log(hong.getType());  // 인간
console.log(hong.getName());  // 길동
console.log(yang.getName());  // 서주

```
장점
- 코드의 재사용
- 생성자 빌려쓰고, 지정해주기
- 프로토타입 공유