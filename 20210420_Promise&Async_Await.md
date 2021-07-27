# JS Promise, Asynchrony

해당 문서를 만들어 놓은지는 꽤 됐는데 정리를 오늘에서야 해본다.

이유는 훈이랑 지유가 async await 관련해서 대화하는데 1도 못알아들어서 ㅋㅋ


## Promise란?
프로미스는 비동기 작업을 더 편하게 할 수 있도록 ES6에서 추가된 기능

Promise 이전에는 비동기 처리를 위해서는 콜백함수로 처리를 해야했는데 그래서 콜백지옥이라는 말이 생겨났다카더라..

```js
function increaseAndPrint(n, callback) {
  setTimeout(() => {
    const increased = n + 1;
    console.log(increased);
    if (callback) {
      callback(increased);
    }
  }, 1000);
}

increaseAndPrint(0, n => {
  increaseAndPrint(n, n => {
    increaseAndPrint(n, n => {
      increaseAndPrint(n, n => {
        increaseAndPrint(n, n => {
          console.log('끝!');
        });
      });
    });
  });
});
// 출처 : 킹갓로퍼트님과 함께하는 모던 자바스크립트
```
이것이 콜백지옥

비동기적으로 처리해야하는 일이 많아질수록 코드가 계속 오르쪽으로 가버린다..

Promise를 사용하면 코드가 깊어지는걸 방지할 수 있다.

## Promise 문법
```js
const myPromise = new Promise((resolve, reject) => {
  //구현
})
```
비동기처리를 할때 요청이 항상 성공하는 것은 아니다.

성공했을땐 resolve 실패했을땐 reject를 호출하면 됨.

### 성공(resolve)과 그 후 처리

```js
const myPromise = new Promise((resolve, reject) => {
   resolve(value);
});
```
resolve 호출 시 특정 값(위 코드에서 value)을 파라미터로 넘겨주면 작업이 끝나고 사용 할 수 있다.

Promise의 작업이 끝났을때 바로 다른 작업을 해야한다면
```js
myPromise.then(value => {
  console.log(value);
  // 결과는 value의 값이 나오겠지?
});
```
해주면 된다.

### 실패(reject)와 그 후 처리
```js
const myPromise = new Promise((resolve, reject) => {
  reject(new Error());
});

myPromise.catch(error => {
  console.log(error);
});
```
[.catch]를 통해서


