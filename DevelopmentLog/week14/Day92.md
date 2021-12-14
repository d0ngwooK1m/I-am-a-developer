# 항해 92일차

## 함수형 프로그래밍

목적: 함수로 이루어진 프로그램을 만들자
함수: 주변의 영향을 받지 않는 함수로 이루어진, 이 함수들을 조합할 수 있는 함수들로 이루어진 프로그램

```javascript
let b = 5;
cosnt add = (a) => {
  return a + b;
}

log(add(5));
log(add(5));
b = 10;
log(add(5));
```

## 일급 함수

## 고차 함수

값으로 함수를 사용하는 함수

## 클로저

함수 값을 기억하고 있는다??

## 이터레이터, 이터러블, 이터러블 프로토콜

이터레이터 => ES6에서 (for a of array) 구문이 가능하게 한 함수
기존 for문과 이터레이터의 차이점은? => Map 과 Set 등에서 기존 for문이 적용되지 않았던 것과 다르게 ES6 문법으로 통일성 있게 적용할 수 있다는 장점이 있다.

- 이터러블: 이터레이터를 리턴하는 [Symbol.iterator]() 를 가진 값
- 이터레이터: { value, done } 객체를 리턴하는 next() 를 가진 값
- 이터러블/이터레이터 프로토콜: 이터러블을 for...of, 전개 연산자 등과 함께 동작하도록한 규약

Map은 keys(), values(), entries() 등의 함수가 있다. 이 값은 이터레이터로 나온다.

## 사용자 정의 이터러블, 이터러블/이터레이터 프로토콜 정의

```javascript
const iterable = {
  [Symbol.iterator]() {
    let i = 3;
    return {
      next() {
        return i == 0 ? { done: true } : { value: i--, done: false };
      },
      [Symbol.iterator]() {
        return this;
      },
    };
  },
};

// for (let i = 0; i < arr.length; i++) {
//   log(arr[i]);
// }

for (const a of iterable) log(a);
```

리턴값으로 next() 함수와 자기 자신을 반환하는 함수가 object 형태로 존재한다.
well formed 이터레이터 => 이터레이터로 반환한 값을 다시 for...of로 사용하거나, 중간부터 반복문을 실시해도 문제 없도록 한다.

## this?

## 이큐브랩

추상화?

## 알고리즘

메모이제이션을 통해 문제를 빠르게 해결할 수 있다~
