# 항해 21일차

## 리액트2 4주차 1강(4주차 오늘 배울 것)

## 리액트2 4주차 2강(무한 스크롤 준비하기)
핵심: 자료를 나눠서 필요할 때마다 불러온다. => 파이어베이스 쿼리 사용

## 리액트2 4주차 3강(무한 스크롤 만들기)
사용자 이용 측면이나, 구조 측면에서 스로틀 방식이 더 좋다.

## WIL
라이프 사이클:  
라이프 사이클은 JSX문법과 가상DOM을 사용하는 리액트에서 볼 수 있는 개념이다. 필요에 따라 DOM구조가 생기고, 바뀌기 때문에 가상DOM이 생성되고, 사라질 때 까지의 흐름을 나타낸 것이 라이프 사이클이다.  
라이프 사이클이 없다면 함수들은 원하지 않을 때 작동하여 오류를 일으킬 수 있다.
![life_cycle](/images/react_week2/1.PNG)  

클래스형 컴포넌트는 상태를 componentDidMount, componentDidUpdate, componentWillUnmount 함수를 통해 어느 시점에서 어떤 동작을 할 것인지 지정할 수 있으며,  
함수형 컴포넌트는 useEffect라는 위 세 함수가 합쳐진 듯한 리액트 훅을 사용하여 동작을 조정하며, useEffect 안에 componentDidMount, componentDidUpdate가 합쳐진 동작을, return에 함수를 준다면 componentWillUnmount의 역할을 한다.  

리액트 훅:  
리액트 훅은 클래스형 컴포넌트에서 사용할 수 없는 변수 지정이나 라이프 사이클을 통한 함수 넣기를 해결하기 위해 등장했다. 현재 강의에서는 useEffect, useState, useRef를 사용하며, useEffect는 함수 시점을 조절할 수 있고, useState와 useRef는 변수지정을 위해 사용된다. 여기서 useState는 라이프 사이클과 무관하게 사용가능하며, useRef는 라이프 사이클 시점에 따라 오류가 날 수도 있으니 조심해야한다(주로 인풋값을 얻고자 할 때 사용한다.)

