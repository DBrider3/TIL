# 5. 패키지

## 패키지 - 시작
기능이 점점 추가되어서 프로그램이 아주 커지게 된다면 어떻게 하면 좋을까?
매우 많은 클래스가 등장하면서 관련 있는 기능들을 분류해서 관리하고 싶을 것이다.
컴퓨터는 보통 파일을 분류하기 위해 폴더, 디렉토리라는 개념을 제공한다. 자바도 이런 개념을 제공하는데, 이것이 바로 패키지이다.
패키지(package)는 이름 그래도 물건을 운송하기 위한 포장 용기나 그 포장 묶음을 뜻한다.

### 패키지 사용
```java
package pack;

public class Data {
	public Data() {
		System.out.println("패키지 pack Data 생성")
	}
}
```
- **패키지를 사용하는 경우 항상 코드 첫줄에 `package pack` 과 같이 패키지 이름을 적어주어야 한다.**
- 여기서는 `pack`패키지에 `Data`클래스를 만들었다.
- 이후에 `Data`인스턴스가 생성되면 생성자를 통해 정보를 출력한다.

## 패키지 규칙
### 패키지 규칙
- 패키지 이름과 위치는 폴더(디렉토리) 위치와 같아야 한다. (필수)
- 패키지 이름은 모두 **소문자**를 사용한다. (관례)
- 패키지 이름의 앞 부분에는 일반적으로 회사의 도메인 이름을 거꾸로 사용한다. 예를 들어, `com.company.myapp`과 같이 사용한다 (관례)
	- 이 부분은 필수는 아니다. 하지만 수 많은 외부 라이브러리가 함께 사용되면 같은 패키지에 같은 클래스 이름이 존재할 수도 있다. 이렇게 도메인 이름을 거꾸로 사용하면 이런 문제를 방지할 수 있다.
	- 내가 오픈소스나 라이브러리를 만들어서 외부에 제공한다면 꼭 지키는 것이 좋다.
	- 내가 만든 애플리케이션을 다른 곳에 공유하지 않고, 직접 배포한다면 보통 문제가 되지 않는다. 
### 패키지와 계층 구조
패키지는 보통 다음과 같이 계층 구조를 이룬다.
- `a`
	- `b`
	- `c`
이렇게 하면 다음과 같이 총 3개의 패키지가 존재한다.
`a`, `a.b`, `a.c`
계층 구조상 `a`패키지 하위에 `a.b`패키지와 `a.c`패키지가 있다.
그런데 이것은 우리 눈에 보기에 계층 구조를 이룰 뿐이다. `a`패키지와 `a.b`, `a.c`패키지는 서로 완전히 다른 패키지이다.
따라서 `a`패키지의 클래스에서 `a.b`패키지의 클래스가 필요하면 `import`해서 사용해야 한다. 반대도 물론 마찬가지이다.

**정리**
패키지가 계층 구조를 이루더라도 모든 패키지는 서로 다른 패키지이다.
물론 사람이 이해하기 쉽게 계층 구조를 잘 활용해서 패키지를 분류하는 것은 좋다. 참고로 카테고리는 보통 큰 분류에서 세세한 분류로 점점 나누어진다. 패키지도 마찬가지이다.

## 패키지 활용
실제 패키지가 어떤 식으로 사용되는지 예제를 통해서 알아보기.
**전체 구조도**
- `com.helloshop`
	- `user`
		- `User`
		- `UserService`
	- `product`
		- `Product`
		- `ProductService`
	- `order`
		- `Order`
		- `OrderService`
		- `OrderHistory`
**com.helloshop.user 패키지**
```java
package com.helloshop.user;

public class User {
	String userId;
	String name;
}
```

```java
package com.helloshop.user;

public class UserService {
}
```

**com.helloshop.product 패키지**
```java
package com.helloshop.product;

public class Product {
	String productId;
	int price;
}
```

```java
package com.helloshop.product;

public class ProductService {
}
```

**com.helloshop.order 패키지**
```java
package com.helloshop.order;

import com.helloshop.product.Product;
import com.helloshop.user.User;

public class Order {

	User user;
	Product product;

	public Order(User user, Product product) {
		this.user = user;
		this.product = product;
	}
}
```

다른 패키지의 기능이 필요하면 `import`를 사용하면 된다.
생성자를 보면 `public`이 붙어있다. `public` 이 붙어있어야 다른 패키지에서 생성자를 호출할 수 있다.

```java
package com.helloshop.order;

import com.helloshop.product.Product;
import com.helloshop.user.User;

public class OrderService {
	public void order() {
		User user = new User();
		Product product = new Product();
		Order order = new Order(user, product);
	}
}
```

```java
package com.helloshop.order;

public class OrderHistory {
}
```

패키지를 구성할 때 서로 관련된 클래스는 하나의 패키지에 모으고, 관련이 적은 클래스는 다른 패키지로 분리하는 것이 좋다.