# 로그인 조건 코딩테스트

심심해서 프로그래머스에서 코딩테스트로 올라온 것 중 간단한 것들은 해봤다.

```js
function solution(new_id) {
    let answer = '';
    let removeSpecialChar = /[!@#*]/g;
    let removeLoopDot = /\.+(?=\.)/g;
    answer = new_id.toLowerCase().replace(removeSpecialChar,"").replace(removeLoopDot,"");
    
    
    return answer;
}

solution("...!@BaT#*..y.abcdefghijklm");
```
