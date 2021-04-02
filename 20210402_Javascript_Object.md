# JS Object 이해, 정리

객체는 일반적으로 여러 데이터와 함수로 이루어지는데 객체 안에 있을 때는 보통 Property, Method라고 부름

관련된 데이터와 함수의 집합으로 즉, 현실의 사물을 프로그래밍으로 구현하는 것.

### 객체의 선언
```js
var object = {
  name: "objectName",
  age: "objectAge",
};
```

### 객체의 속성(Property)
선언된 객체를 보면 
```js
name: "objectName",
age: "objectAge",
```
콤마로 구분되는 이것을 객체의 Property 라고 부름


### 객체의 키(Key), 값(Value)
```js
name: "objectName",
age: "objectAge",
```
여기서 객체의 Key는 name,age / Value는 "ObjectName", "objectAge"

Key는 String만 가능하며 따옴표가 없어도 상관X

```js
user name: "Kyusang",   // Syntax Error
"user name": "GU",      
+name: "Hoon",          // Syntax Error
"+name": "Not Friend"
```
다만 Key가 띄어쓰기 혹은 특수문자를 포함하고 있을 경우 따옴표로 감싸줘야함


### 객체의 Key, Value Reference
객체의 Key 즉 속성 이름과 Value 속성 값에 접근하는 방법은 2가지가 있음

.을 사용하는 방법 / [] 를 사용하는 방법

```js
object.name;    // "objectName"
objecet[name];  // "objectName"
```
같은 값을 출력하는데 표현 방식이 다른 이유는 무엇일까?

위에서 설명했듯 Key가 일반적인 String일 경우 . 사용
띄어쓰기 특수문자 등이 들어간 Key 혹은 변수일 경우 [] 사용



