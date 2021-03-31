## FreeCodeCamp Basick JavaScript #75 - Counting Card
FreeCodeCamp - JavaScript를 공부하던 중 Counting Card라는 예제를 풀게됐는데
제한시간안에 풀지 못해서 다시 풀던 중 개인적으로 변형해봤다.

#### 본 문제의 요구사항
- 2,3,4,5,6 을 뽑으면 전역변수 count를 +1
- 7,8,9 -> count 변화 없음
- 'A','J','Q','K' -> count -1
- function cc(card){} 함수를 작성
- cc(3); cc(7); cc('Q'); cc(8); cc('A'); 실행 시 "-1 Hold" 출력
- cc(2); cc(3); cc(4); cc(5); cc(6); 실행 시 "5 Bet" 출력

