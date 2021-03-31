## FreeCodeCamp Basick JavaScript #75 - Counting Card
FreeCodeCamp - JavaScript를 공부하던 중 Counting Card라는 예제를 풀게됐는데
제한시간 안에 풀지 못해서 다시 풀던 중 문제를 변형하고 풀이해봤다.

### 문제 내용
Blackjack의 카드카운팅을 러프하게 구현

#### 본 문제 요구사항
- 2,3,4,5,6 을 뽑으면 전역변수 count를 +1
- 7,8,9 -> count 변화 없음
- 'A','J','Q','K' -> count -1
- function cc(card){} 함수를 작성
- cc(3); cc(7); cc('Q'); cc(8); cc('A'); 실행 시 "-1 Hold" 출력
- cc(2); cc(3); cc(4); cc(5); cc(6); 실행 시 "5 Bet" 출력

#### 본 문제 풀이
```js
var count = 0;

function cc(card) {
  // Only change code below this line
  var text = "Bet";

  if ( card <= 6 ) {
    count++;
  } else if (card >= 10 || typeof card === "string") {
    count--;
  }

  if ( count <= 0) {
    text = "Hold";
  }

  return count + " " + text;
  // Only change code above this line
}

cc(2); cc(3); cc(7); cc('K'); cc('A');
// -copyright GUKIM all rights reserved.
```

### 문제 변형

#### 변형 문제 요구사항
<고정 규칙>
- 2,3,4,5,6 을 뽑으면 전역변수 count를 +1
- 7,8,9 -> count 변화 없음
- 'A','J','Q','K' -> count -1

- 카드를 Deck["A",2,3,4,5,6,7,8,9,10,"J","Q","K"]으로 구성
- Blackjack의 딜러와 플레이어의 역할을 구현하기위해 Banker와 Player Class 생성
- Banker는 카드를 섞고(Shuffle) 플레이어에게 Deck의 맨 앞 카드를 줘야함(Give)
- Player는 받은 카드(hand)를 보고 **고정규칙**에 따라 베팅(betOrHold)


#### 변형 문제 풀이
```js
var count = 0; // 베팅, 홀드의 기준 값
var cardSet = [`A`,2,3,4,5,6,7,8,9,10,`J`,`Q`,`K`]; // Deck 구성
var hand = []; // Banker가 Player에게 나눠준 카드 저장

class cardBanker { // 뱅커 클래스
  constructor(cardDeck, cardGive) {
    this.deck = cardDeck;
    this.give = cardGive;
  }

  cardShuffle() { // cardSet 섞기
    this.deck.sort(() => Math.random() - 0.5);
  }

  cardGive() { // Player에게 카드 배분
    this.give.push(this.deck.shift());
  }
}

class cardPlayer { // 플레이어 클래스
  constructor(card) {
    this.hand = card;
  }

  betOrHold(i) { // 베팅과 홀드 
    typeof this.hand[i] == "string" || this.hand[i] >= 10 ?
    count-- : 
    (this.hand[i] < 7 && this.hand[i] > 1 ? count++ : count + 0);
  }
  
  result() { // 결과
    if (count >= 0){ return console.log(count+"Bet")}
    else return console.log(count+"Hold");
  }
}
/*
**진행 순서**
1. 인스턴스 생성
2. 덱 섞기
3. 섞인 덱 보여줌
4. 카드 배분
5. 플레이어 손패 확인
6. 베팅
7. 결과
8. 5회 반복
*/


// 인스턴스 생성

let banker = new cardBanker(cardSet,hand);
let player = new cardPlayer(hand);

banker.cardShuffle(); // 카드 섞기

for(var i = 0; i < 5; i++) 
{
  console.log(cardSet); // 카드 카운팅
  
  banker.cardGive(); // 카드 배분
  
  console.log(hand); // 손패 확인
  
  player.betOrHold(i); // 베팅
  
  player.result(); // 결과
}
```

#### 기존 풀이의 아쉬운 점
1. 전역 변수를 어떻게 처리해야할지 모르겠음 (전역 변수를 쓰는게 좋은게 아니라는 것만 알고 있었음)

1-1.플레이어가 여러명이면 각각 카운팅 해야하는데 전역변수를 사용해서 결과가 똑같이 나옴

2. 아직도 고쳐지지 않은 클래스,변수,함수 

3. 카드를 받는 주체는 Player인데 배분한 카드의 정보는 Banker가 담고 있었음

4. 삼항연산자를 복잡하게 사용함

5. 불필요한 else 사용


