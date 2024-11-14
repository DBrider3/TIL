# 8. final

## final 변수와 상수
`final`키워드는 이름 그대로 끝! 이라는 뜻이다.
변수에 `final`키워드가 붙으면 더는 값을 변경할 수 없다.

참고로 `final`은 `class`, `method`를 포함한 여러 곳에 붙을 수 있다.

### 지역변수
- `final`을 지역 변수에 설정할 경우 최초 한번만 할당할 수 있다. 이후에 변수의 값을 변경하려면 컴파일 오류!
- 매개변수에 `final`이 붙으면 메서드 내부에서 매개변수의 값을 변경할 수 없다. 

### final - 필드 (멤버 변수)
```java
package final1;

// final 필드 - 생성자 초기화
public class ConstructInit {
  final int value;

  public ConstructInit(int value) {
    this.value = value;
  }
}
```
- `final`을 필드에 사용할 경우 해당 필드는 생성자를 통해서 한번만 초기화 될 수 있다.

```java
package final1;

//final 필드 - 필드 초기화
  public class FieldInit {
    static final int CONST_VALUE = 10;
    final int value = 10;
}
```
- `final`필드를 필드에서 초기화하면 이미 값이 설정되었기 때문에 생성자를 통해서도 초기화 할 수 없다. `value`필드를 참고하자.
- `static`변수에도 `final`을 선언할 수 있다.


