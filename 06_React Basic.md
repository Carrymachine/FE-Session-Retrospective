# 회고 양식 (배웠던 것 / 수업 피드백 / 본인 피드백)

## 이번 수업에 잘 된 것 

#### 수업에서 좋았던 것
- 사실 근 3달간 달려온 이유가 React를 배우기 위함이었기 때문에 설레고 좋았다
- 아무래도 훈쌤이 지금 당장 현업에서 쓰고있고 가장 잘 설명할 수 있는 부분이어서 설명이 어렵긴 했지만 
  좋은 얘기를 많이 들었다.
- 

#### 본인에게서 개선된 점
- 리액트를 시작하고 나서는 그래도 항상 관심있어했던 라이브러리고 재밌기도해서 (사실 김지유가 너무 똑똑해서 내가 수업에서 뒤쳐질까봐) 혼자서도 공부를 많이 한 것 같다.
- 몇 주간 혼자 공부하는 시간(주로 복습)을 늘리니까 확실히 머리속에도 오래남고 이렇게 오랜만에 회고록을 미리 작성해보는 것 같다.
- 앞으로도 개발자로 살아갈 수 있다는 가정하에 혼자서 공부하는 습관을 꾸준히 유지했으면 좋겠다.

## 이번 수업에 아쉬웠던 것

#### 배우면서 힘들었던 것
- 어려워

# React Concept Overview

## React / ReactDOM

React는 기존 DOM API를 사용한 UI 조정, 엘리먼트 추가 및 삭제 과정을
데이터의 변경(state, props)에 반응하도록 도와주며, 이를 통해 다양한 DOM 동작 제어 가능하다

React는 UI 요소의 집합을 컴포넌트로 표현하고 이 UI 요소는 React Element로 표현한다.
React Element 는 HTML과 유사한 문법을 지닌 JSX 마크업을 사용해 구현한다.

--------- 

위에서 언급한 컴포넌트의 집합이 ReactDOM
ReactDOM은 state, props 의 변경 감지 후 트리를 다시 그리며 각 컴포넌트의 렌더링 여부를 결정한다.

이전 렌더링에 사용된 트리와 새 렌더링에 사용될 트리를 비교하고,
실제로 DOM에서 어떤 부분을 변경해야 할 지 취합하는 과정이 **재조정(Reconciliation)**

이 비교&렌더링 과정은 직접 DOM 엘리먼트의 값을 비교하지 않고
JS 트리인 ReactDOM을 비교하기 때문에 Virtual DOM 이라고 부른다.

## State / Props

`State` = 컴포넌트 내부의 상태
`Props` = 컴포넌트 외부에서 주입받는 데이터

`State`를 조작하면 React는 리렌더링을 실행(컴포넌트 트리를 다시 그림)
각 컴포넌트의 `State/Props` 변경 여부를 확인하고, 렌더링이 필요할 경우 JSX 템플릿을 다시 생성한다.

## Class Component

클래스 컴포넌트는 React 초기부터 존재했고, 지금도 여러 레거시 코드로 찾아볼 수 있다.
현재는 Functional Component를 많이 사용하지만 언제 어디서 레거시를 유지보수해야할지 모르고
레거시를 알아야 지금 문법을 이해하는게 더 수월할 것이라고 생각해 공부했다.

Component 클래스를 구현하게 되고 기본적으로 render/lifecycle method, state 속성을 지원한다.
생성자에서 컴포넌트 외부 상태인 props 를 주입받는다.

클래스 컴포넌트의 state는 인스턴스 내부의 상태
setState 메서드를 사용해 새 값을 할당하고 렌더링을 실행할 수 있다.

또한 컴포넌트는 생명 주기를 가진다.

컴포넌트의
첫 렌더링 / State, Props 변경으로 인한 컴포넌트 업데이트 / 컴포넌트 제거 등을 통틀어
컴포넌트 라이프사이클이라고 부르고

실행 시점에 라이프사이클 메서드를 활용해 동작을 추가할 수 있다.

대표적인 라이프사이클 메소드 3개
`Component[Will/Did]Mount/ Component[Will/Did]Update / Component[Will/Did]Destroy`

## Class Component - this binding issue

클래스 컴포넌트에서 특정 버튼의 이벤트를 통해 state를 갱신하기 위해 `handleClick` 메서드에서 `this.setState` 를 실행하려 할 때,
this 의 컨텍스트(Component 인스턴스)가 유지되지 않는 현상을 발견할 수 있다.

이는 render 메서드에서 JSX가 넘겨받는 핸들러 함수가 

`this.handleClick()` 형태로 직접 실행되는 것이 아닌 `this.handleClick` 메서드의 참조만을 넘겨받기 때문인데

호출 시점의 `this.handleClick` 은 익명 함수이고, 실행 주체가 이벤트 핸들러를 실행해주는 Web API로 변경되므로

`this` 바인딩을 직접 해주지 않을 경우 `setState` 메서드를 `this` 에서 찾지 못하는 문제가 발생한다.

해결 방안:
1. 메서드 선언 시 Arrow function 을 사용해 render() 함수 내에서 사용된 `this.handleClick`의 Lexical this를 Component로 강제
2. `Function.bind(thisArg)` 를 사용해 메서드의 this 바인딩을 강제

## Class Component - props mutation issue in async function

비동기 함수에서 `this.props` 를 직접 참조할 경우, 비동기 함수의 실제 실행 시점의 props 값이 변조될 수 있다.

이는 render 메서드에서 props의 값을 변수에 모두 할당하고, 메서드 역시 render 시점에 모두 선언하는 것으로 해결할 수 있는데

이 방식의 경우 모든 커스텀 메서드가 render 스코프 안에서 선언되게 되므로
render 를 제외한 메서드가 필요하지 않게 되는 딜레마가 생긴다.

함수형 컴포넌트는 매 렌더링 시마다 위 패턴과 유사하게 모든 함수를 재생성하게 되므로, props 변조에 대응할 필요가 없다.

## Functional Component / Hooks

Functional Component는 기본적으로 상태를 가지지 못하고 JSX를 리턴하는 render함수와 같은 동작을 한다.(SFC)

그러나 React 16에서 Hooks가 추가되면서 
상태 관리와 라이프사이클 메서드 등을 기존 Class Component에서 사용하던 방식보다 훨씬 간단하게 사용할 수 있게 됐다.

주로 사용하는 Hooks 4개
`useState`, `useEffect`, `useMemo`, `useCallback`
각각 Functional Component 안의 상태관리, 라이프사이클 훅, 변수 재선언 방지, 함수 재선언방지 기능을 제공한다.

이것은 JS의 동작인 Closure를 통해 구현,
함수 내부의 변수가 외부 스코프로 return 되었을 경우 메모리에서 해제되지 않는 것을 활용해
Hooks의 내부값을 Functional Component의 렌더링을 실행하는 React 내부에 붙여둔다.

렌더링 시 붙여 둔 값과 현재 값을 비교해 렌더링 실행 여부를 결정
=> React 라이브러리에서 Hook 목록을 저장하는 배열을 소유

이러한 구현 상의 특징에 따라, Hooks 는 절대 순서와 실행 갯수가 변경되서는 안되고
이는 React 디버깅 과정에서 흔히 발견되는 실수다.

## Rendering Strategy

Class/Functional Component 모두 props 변경과 상관없이 무조건 렌더링을 실행

Class Component =  최적화를 위해 state, props의 변경점을 체크 > 렌더링 여부를 결정할 수 있는 `shouldComponentRender` Method를 작성할 수 있다.
Functional Component = 아래서 언급할 `React.memo(Component, equalityFn)` 함수의 두번째 Parameter를 조작하는 것으로 해결 가능하다.

보통의 경우 props 내의 속성이 변경되지 않았을 때만 레더링을 방지해도 충분한데
Class Component = Component 대신 Pure Component 클래스를 상속받는 것으로 해결 가능
Functional Component = 고차 함수인 React.memo를 사용해 직정 컴포넌트를 감싸주는 것으로 해결 가능

# What i did

### 2021.05.25 - React의 기원과 역사
### 2021.05.26 - 강훈쌤 멘탈바사삭치킨
### 2021.05.27 - 정규상 퇴사 + Farewell Party
### 2021.05.28 - 정규상 개인사
### 2021.05.29 - 토
### 2021.05.30 - 일
### 2021.05.31 - 강훈 회식
### 2021.06.01 - 정규상 회식
### 2021.06.02 - 강훈 12시간 무호흡 코딩 (업무)
### 2021.06.03 - 자습 (JSX)
### 2021.06.04 - 자습 (Stateless Functional Component)
### 2021.06.05 - 토 (김지유 강훈 정규상 술)
### 2021.06.06 - 일 (현충일)
### 2021.06.07 - Class Component, How to pass props (prop drilling)
### 2021.06.08 - Set VSCode development environment
### 2021.06.09 - TodoList(Class Component) Start
### 2021.06.10 - TodoList(Class Component) End / 피드백 (Class to Functional) 
### 2021.06.11 - TodoList - Class Component to Functional Component 마이그레이션
### 2021.06.12 - 토
### 2021.06.13 - 일
### 2021.06.14 - 강훈 강의 제작 미팅, 자습(TodoList 점검 및 Git CLI 사용법)
### 2021.06.15 - React Class Component - this binding 이슈
### 2021.06.16 - React Pagination Component Start
### 2021.06.17 - React Pagination Component End w/styled-components
### 2021.06.18 - React Pagination Component 피드백
### 2021.06.19 - 토
### 2021.06.20 - 일
### 2021.06.21 - 자습
### 2021.06.22 - 자습
### 2021.06.23 - freecodecamp ex1 (Random Quote) start
### 2021.06.24 - Random Quote 자습
### 2021.06.25 - 강훈 개인사정
### 2021.06.26 - 토
### 2021.06.27 - 일
### 2021.06.28 - Random Quote 구현 피드백
### 2021.06.29 - React Lifecycle Methods (willmount / willUpdate / willDestroy <> useEffect)
### 2021.06.30 - Random Quote 구현 피드백 2
### 2021.07.01 - 김지유 첫출근!!
### 2021.07.02 - 다같이 한강가서 술먹음
### 2021.07.03 - 토
### 2021.07.04 - 일
### 2021.07.05 - 강훈 휴가나온 동생 데리러 감
### 2021.07.06 - StudyArchive 초안 기획
### 2021.07.07 - 강훈 멘탈 파괴 + React Session 회고
