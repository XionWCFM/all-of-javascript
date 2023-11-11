# class

클래스의 기본 예제를 먼저 보자

```tsx
class Color {
    constructor(r = 0 , g = 0 , b = 0) {
        this.r = r;
        this.g = g
        this.b = b
    }

    get rgb() {
        return ''
    }
}
```

여기서 조금 놀라웠던 것은 extends 키워드가 타입스크립트에서만 지원되는게 아니라

자바스크립트에서도 지원되는 기능이었다는 것이다.

사실 생각해보면 당연한건데.. 당연하다고 생각을 안하고 있었다


# super

super()는 서브클래스 생성자에서 마치 객체를 생성하는 함수 인것처럼 super를 호출하고

슈퍼클래스가 객체의 초기화를 수행하도록 하는 키워드이다.

# 클래스 선언과 클래스 표현식

```tsx
class Class1 {}

let Color = class {}

let C = class Color {}

```

당연히 클래스 선언식만 써왔는데 함수처럼 클래스도 저런형태로 할당할 수 있다.

