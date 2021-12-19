# 항해 97일차

## 함수형 프로그래밍

지연 함수들의 특징:

값을 위에서 부터 하나씩 내려준다. 모든 배열들을 정리하고 갔던 기존의 방식과 다르다.

함수를 어떻게 조합해도 같은 결과가 나온다.  
[[mapping, mapping], [filtering, filtering], [mapping, mapping]] = [[mapping, filtering, mapping], [mapping, filtering, mapping]]

## 코어 자바스크립트

클로저: 상위 함수가 종료된 시점에도 다시 참조할 수 있는 변수가 존재하는 함수들의 모임

클로저가 발생하는 원리:

```javascript
const outer = () => {
  let variation = 0;

  const inner = () => {
    variation++;
    console.log(variation);
  };
  return inner;
};
outer();

(function () {
  var a = 0;
  var intervalId = null;
  var inner = function () {
    if (++a >= 10) {
      clearInterval(intervalId);
    }
    console.log(a);
  };
  intervalId = setInterval(inner, 1000);
})();
```

실행되지 않은 함수 자체를 리턴 시, 그 함수가 상위 변수를 참조하고 있다면 클로저가 된다.  
또한 리턴이 없어도 함수가 외부에 작동하게 되면 클로저가 된다.

클로저는 의도적으로 특정한 변수등을 지우지 않는 기능이라 사용이 끝나면 정리가 필요할 때도 있다.

클로저를 활용해 외부에서 데이터를 바꾸지 못하게 하는 데이터 은닉화도 적용이 가능하다.

함수의 일부만 받고 기다리는 커리함수도 클로저 기능으로 표현이 가능한 것이었다.(위의 변수등을 참조할 수 있게끔 함)  
다만 함수형 프로그램에서는 이터레이터를 사용하는 것이 다를 뿐이다.
