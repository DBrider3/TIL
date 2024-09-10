# 6. 스코프, 형변환

# 스코프 존재 이유

```java
package scope;

public class Scope3_1 {
    public static void main(String[] args) {
        int m = 10;
        int temp = 0;
        if (m > 0) {
            temp = m * 2;
            System.out.println("temp = " + temp);
        }
        System.out.println("m = " + m);
    }
}
```

- 비효울적인 메모리 사용
    - `temp`는 `if`코드 블록에서만 필요하지만, `main()`코드 블록이 종료될 때 까지 메모리에 유지된다. 따라서 불필요한 메모리가 낭비된다. 만약 `if` 코드 블록 안에 `temp`를 선언했다면 자바를 구현하는 곳에서 `if`코드 블록의 종료 시점에 이 변수를 메모리에서 제거해서 더 효율적으로 메모리를 사용할 수 있다.
- 코드 복잡성 증가
    - 좋은 코드는 군더더기 없는 단순한 코드이다. `temp`는 `if`코드 블록에서만 필요하고, 여기서만 사용하면 된다. 만약 `if`코드 블록 안에 `temp`를 선언했다면 `if`가 끝나고 나면 `temp`를 전혀 생각하지 않아도 된다. 머리속에서 생각할 변수를 하나 줄일 수 있다. 그런데 지금 작성한 코드는 `if`코드 블록이 끝나도 `main()`어디서나 `temp`를 여전히 접근할 수 있다. 누군가 이 코드를 유지보수 할 때 `m`은 물론이고 `temp`까지 계속 신경써야 한다. 스코프가 불필요하게 넓은 것이다. 지금은 코드가 매우 단순해서 이해하는데 어려움이 없겠지만 실무에서는 코드가 매우 복잡한 경우가 많다.
- 정리
    - 변수는 꼭 필요한 범위로 한정해서 사용하는 것이 좋다. 변수의 스코프는 꼭 필요한 곳으로 한정해서 사용하자. 메모리를 효율적으로 사용하고 더 유지보수하기 좋은 코드를 만들 수 있다.
    - **좋은 프로그램은 무한한 자유가 있는 프로그램이 아니라 적절한 제약이 있는 프로그램이다.**

# 자동 형변환

자연스럽게 작은 그릇에서 큰 그릇으로 옮기는게 당연하다. 자바에서도 마찬가지이다. 

그래서 작은 범위 숫자 타입에서 큰 범위 숫자 타입으로의 대입은 개발자가 직접 형변환을 하지 않아도 된다. 

# 명시적 형변환

하지만 큰 범위에서 작은 범위 대입은 명시적 형변환이 필요하다.

형(타입)을 바꾼다고해서 형변환이라고 한다. 영어로는 캐스팅이라 한다. 

### 캐스팅 용어

“캐스팅”은 영어 단어 “cast”에서 유래되었다. “cast”는 금속이나 다른 물질을 녹여서 특정한 형태나 모양으로 만드는 과정을 의미한다.

### 형변환과 오버플로우

```java
maxIntOver = 2147483648L; //int 최고값 + 1 

intValue = (int) maxIntOver; //변수 값 읽기 

intValue = (int) 2147483648L; //형변환 시도 

intValue = -2147483648;
```

결과를 보면 `-2147483648` 이라는 전혀 다른 숫자가 보인다. `int`형은 `2147483648L`를 표현할 수 있는 방법이 없다. 이렇게 기존 범위를 초과해서 표현하게 되면 전혀 다른 숫자가 표현되는데, 이런 현상을 오버플로우라고 한다.

보통 오버플로우가 발생하면 마치 시계가 한바퀴 돈 것 처럼 다시 처음부터 시작한다. 참고로 `-2147483648` 숫자는 `int`의 가장 작은 숫자이다.

**중요한 것은 오버플로우가 발생하는 것 자체가 문제다! 이 상황 자체가 발생하지 않도록 막아야 한다.** 

# 계산과 형변환

```java
package casting;

public class Casting4 {

    public static void main(String[] args) {
        int div1 = 3 / 2;
        System.out.println("div1 = " + div1); //1
        
        double div2 = 3 / 2;
        System.out.println("div2 = " + div2); //1.0
        
        double div3 = 3.0 / 2;
        System.out.println("div3 = " + div3); //1.5
        
        double div4 = (double) 3 / 2;
        System.out.println("div4 = " + div4); //1.5
        
        int a = 3;
        int b = 2;
        double result = (double) a / b;
        System.out.println("result = " + result); //1.5
	}
}
```

중요한것은 

**서로 다른 타입의 계산은 큰 범위로 자동 형변환이 일어난다.**

```java
double div2 = 3 / 2; //int / int
double div2 = 1; //int / int이므로 int타입으로 결과가 나온다.
double div2 = (double) 1; //int -> double에 대입해야 한다. 자동 형변환 발생
double div2 = 1.0; // 1(int) -> 1.0(double)로 형변환 되었다.
```

```java
double div3 = 3.0 / 2; //double / int
double div3 = 3.0 / (double) 2; //double / int이므로, double / double로 형변환이 발생한
다.
double div3 = 3.0 / 2.0; //double / double -> double이 된다.
double div3 = 1.5; ```
```