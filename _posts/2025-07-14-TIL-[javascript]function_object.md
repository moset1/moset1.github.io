---
title: "JavaScript 함수는 왜 객체일까?"
excerpt: "JavaScript의 함수, Lexical Environment를 연결하여 함수가 객체임을 이해해봅니다.."

categories:
  - Language
tags: ["JavaScript", "렉시컬 환경", "함수 객체"]

permalink: /language/js-function-object/

toc: true
toc_sticky: true

date: 2025-07-14
last_modified_at: 2025-07-14
---



# JavaScript에서 함수는 어떻게 객체일까?

JavaScript를 처음 접했을 때, 객체지향 언어가 아니라는 인상을 받았습니다.
Java처럼 클래스를 기반으로 하지 않고, 굳이 클래스를 만들지 않아도 `map`처럼 생긴 객체를 생성해서 데이터를 표현할 수 있었기 때문입니다.
또한, 함수도 독립적으로 정의할 수 있어서 클래스 기반 언어와는 많이 달라 보였습니다.

하지만 나중에 알게 된 사실은, JavaScript 역시 **객체지향 언어**이며, **프로토타입 기반 객체지향 언어**라는 점이었습니다.
즉, 클래스 기반 언어와는 작동 방식이 다르지만, 객체지향의 개념은 여전히 유지됩니다.
(프로토타입 기반 객체지향 언어에 대한 자세한 내용은 다음 글에서 다뤄보겠습니다.)

---

## JavaScript에서는 모든 것이 객체다

JavaScript에서는 함수도, 배열도 객체입니다.
그렇다면 함수가 객체라는 말은 무슨 뜻일까요?
일반적으로 '객체'라고 하면 클래스 기반 언어에서 **클래스의 인스턴스**를 떠올리게 됩니다.
클래스 이름이 있고, 그 안에 멤버 변수와 메서드가 있으며, `new` 연산자로 생성된 인스턴스가 곧 객체가 됩니다.

그런데 JavaScript에서는 함수가 곧 객체입니다.
객체라는 것은 **값**이라는 뜻이고, 값이기 때문에 다음과 같은 특징을 가질 수 있습니다:

* **변수에 할당할 수 있습니다.**
* **다른 함수의 인자로 전달할 수 있습니다.**
* **함수의 반환값으로 사용할 수 있습니다.**
* **프로퍼티를 가질 수 있습니다.**

---

## 함수는 값이다

```js
function sayHello() {
  console.log("Hello!");
}

sayHello.language = "English";
console.log(sayHello.language); // "English"
```

위 예시처럼 함수는 코드 블록일 뿐만 아니라, 객체처럼 프로퍼티를 가질 수 있습니다.
JavaScript에서는 함수도 일급 객체(First-Class Object)로 취급됩니다.

### 함수는 변수에 할당할 수 있습니다

```js
const greet = function () {
  console.log("Hi!");
};
```

### 함수는 인자로 전달될 수 있습니다

```js
function callTwice(callback) {
  callback();
  callback();
}

callTwice(() => console.log("Called!"));
```

이처럼 함수는 값으로서 전달될 수 있고, 그 결과 콜백 함수(callback)로도 자주 사용됩니다.

---

## 함수는 외부의 값을 어떻게 기억할까?

JavaScript의 함수는 단지 독립된 코드 블록이 아니라, **외부의 값을 기억할 수 있는 구조**를 가집니다.
이러한 특징은 렉시컬 환경(Lexical Environment)이라는 내부 구조 덕분입니다.

함수가 실행될 때:

1. 실행 컨텍스트(Execution Context)가 생성됩니다.
2. 내부에는 함수의 **지역 변수와 매개변수**가 저장되는 **렉시컬 환경**이 구성됩니다.
3. 이 환경은 `[[Environment]]`라는 내부 참조를 통해 **외부 환경과 연결**됩니다.

즉, 함수는 자신이 정의된 위치에서의 스코프(lexical scope)를 기억합니다.
이러한 구조 때문에, 함수는 외부 변수에 접근하거나 변경할 수 있게 됩니다.

---

