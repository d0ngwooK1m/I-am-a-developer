# 항해 95일차

## 알고리즘

## 함수형 프로그래밍

## 코어 자바스크립트

this: this 어떤 것을 가리키는 요소. 근데 위치나 형태에 따라 가리키는 것이 달라진다.

```javascript
var obj1 = {
  outer: function () {
    console.log(this);
    //obj1
    var self = this;
    var innerFunc = function () {
      console.log(self);
      //window
    };
    innerFunc();

    var obj2 = {
      innerMethod: innerFunc,
    };
    obj2.innerMethod();
    //obj2
  },
};
obj1.outer();
```

실행컨텍스트가 생기면서 바인딩에 묶여있는 부분이 this가 가리키는 곳이 된다.  
obj1.outer()는 바인딩에 obj1이 묶여있으므로 this가 obj1을 가리킨다.  
innerFunc()는 어디에도 바인딩 되어있지 않기 때문에 this가 전역객체인 window를 가리킨다.
obj2.innerMethod()는 obj2에 바인딩 되어있기 때문에 this가 obj2를 가리킨다.  
innerFunc를 obj1에 바인딩 시키는 방법은 바깥에서 self 변수를 통해 가리키는 것과 화살표 함수를 사용하는 방법이 있다.

콜백함수에서 this는 사용하는 메서드마다 다르다. ex) setTimeOut, forEach, addEventListener...

생성자 함수 내부에서는 보통 함수와 다르게 this는 생성자 함수 자체를 가리킨다.

call, apply 메서드를 통해 this의 다양한 활용을 할수있다. 개인적으로 함수형 프로그래밍과 스프레드 문법으로 대체 가능하다고 생각한다.
