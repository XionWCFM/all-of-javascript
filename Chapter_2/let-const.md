# let const

이 장을 통하여 let ,const가 어떻게 진정한 블록 스코프를 제공하는지 알 수 있습니다.

# 바인딩 : 변수 , 상수 , 기타 식별자의 작동 방식

const는 범위 / 보유할 수 있는 값의 종류 등의 관점에서는 ㅣet과 동일하게 동작합니다.

이것은 내부적으로 변수와 상수는 사양에서 식별자 바인딩이라고 볼 수 있기 때문인데요

```tsx
let x = 42
```

이 행위는 x라는 식별자에 대한 바인딩을 만들고 해당 바인딩의 저장소 슬롯에 값 42를 저장하는 것이며

이 경우에는 변경 가능한 바인딩인 것입니다.

만약 상수를 만들때에는 변경할 수 없는 바인딩이 됩니다.

식별자의 바인딩에는 이름과 값이 있습니다.

또한 객체 속성과 마찬가지로 컨테이너에 있으며 환경 객체라고 부릅니다.


# 외부 환경의 설정

코드 실행이 블록 스코프 식별자가 있는 블록에 들어가면

블록에 대한 환경 객체는 블로긍ㄹ 외부 환경으로 포함하는 코드에 대한 환경 객체를 가져옵니다.

함수가 호출되면 호출을 위한 환경 객체는 함수가 생성된 환경([[Environment]]) 내부 슬롯을 의미합니다.

# ClousuresInLoopsWithLet

```tsx
function closuresInLoopsWithLet() {
    for(let counter = 1  ; counter <=3 ; ++counter>) {
        setTimeout(function(){
            console.log(counter)
        },10)
    }
}
```
이 코드를 실행한다고 생각해봅시다.

자바스크립트 엔진은 각 루프 반복에 대해 각각 별도의 counter 변수가 있는

새로운 환경 객체를 생성하기 때문에

각 타이머 콜백을 다른 카운터 변수가 감싸게 됩니다.

그래서 출력결과는 1,2,3이 되는것이지요


다음은 이 코드를 엔진 관점에서 바라보았을 때의 작동 순서입니다.

1. 호출에 대한 환경 객체를 만듭니다.(이를 책에서는 CallEnvObject라고 정합니다.)

2. ClousresInLoopsWithLet 함수에 저장된 환경에 대한 CallEnvObject의 외부 환경 참조를 설정합니다.

3. for의 초기화 부분에서 let으로 선언된 변수 목록을 기억하며 for문 처리를 시작합니다.

4. CallEnvObject를 외부 환경으로 사용하며 루프의 초기화 부분에 대한 새 환경 객체를 만들고 값이 1인 카운터에 대한 바인딩을 만듭니다.

5. CallEnvObject를 외부 환경 객체로 사용하여 첫 번째 반복에 대해 새 환경 객체를 만듭니다.

6. 3 단계의 목록을 참조하여 LoopEnvObject1의 카운터에 대한 바인딩을 작성하고 값을 1로 설정합니다.

7. LoopEnvObject1을 현재 환경 객체로 설정합니다.

카운터 <=3이 참이니까 타이머 함수를 만들고 LoopEnvObject1에 대한 참조를 제공합니다.


이렇듯 각각의 타이머 함수에 대해 다른 실행환경이 제공되기 때문에

우리는 var로 선언한 for loop와 let으로 선언한 for loop가 다르게 동작한다는 것을 이해할 수 있습니다.


# 성능에 대한 영향

이 부분이 재밌는 포인트인데 한창 var가 let보다 빠르다 성능을 생각하면 var를 써야한다. 같은 글들과

지금은 최적화가 진행되어 var, let의 차이는 미미하다 없는 수준이다

라는 글들이 많아서 혼란스러웠던 기억이 있었기 때문입니다.


루프에서 블록 변수를 사용하고 이를보유하고 체인을 설정하고 복사할 새 환경 객체를 만들고 반복 바인딩 값을 복사해야하면

루프 속도가 느려지지 않을까?

라는 의문은 초기에는 정답이었으나 이후 최적화가 진행되었다고하네요

