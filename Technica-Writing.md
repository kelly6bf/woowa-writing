# 객체지향 생활 체조 시작하기
## 객체지향 생활 체조란?
**객체지향 생활 체조**는 ‘소트웍스 앤솔러지'라는 책에서 처음 제시한, 객체지향 프로그래밍을 잘 하기 위한 9가지 원칙입니다. 객체지향 프로그래밍의 본질을 더 잘 따라갈 수 있도록 유도하고, 가독성 높으면서 유연하고 유지보수가 쉬운 코드를 작성하기 위한 일종의 가이드라인이라고 볼 수 있습니다.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeb83FBy2qPwy1Un5o5GBHZCAXR9xK8T0uyi2eEkoCIBZz9mJe6nzOqEdTflMLZ255aHW4Dk9ntcZ8fPC0WfHYCdyfDtE2BOtPqpa_QsFk7L7nttlODJuaiGTSarYjDTQMk_bQwXwaFg8-PwBve4JgwUzD-?key=O_FxyUbZ_0aKjkAwvR6zMQ)

## 객체지향 생활 체조 원칙이 주는 이점
앞서 소개한것 처럼 객체지향 생활 체조 원칙을 잘 준수한다면 다음과 같은 이점들을 얻을 수 있습니다.

### 1. 코드 가독성 향상
객체지향 생활 체조의 여러 원칙들은 코드의 가독성을 높이는 데 크게 기여합니다. 예를 들어, 한 메서드에서 들여쓰기를 한 단계만 사용하고, else를 피하는 등의 원칙은 코드의 논리 흐름을 명확하게 만들어줍니다.

### 2. 응집도 증가
객체지향 생활 체조는 클래스와 메서드가 각각 한 가지의 책임만 가지도록 유도합니다. 이를 통해, 응집도가 높아지며, 클래스나 메서드가 특정 기능을 담당하게 됩니다. 예를 들어, “3개 이상의 인스턴스 변수를 가지지 않는다"라는 규칙은 클래스가 너무 많은 책임을 가지지 않도록 유도합니다.

### 3. 테스트 용이성 증가
각 메서드가 단일 책임을 가지며, 한 메서드의 책임이 작아지면 해당 메서드를 테스트하기가 훨씬 쉬워집니다. 예를 들어, “한 메서드에 들여쓰기를 한 단계만 사용하기"라는 원칙을 따르면, 복잡한 로직이 여러 작은 메서드로 분리되기 때문에, 각 메서드에 대한 단위 테스트(Unit Test)를 작성하기가 용이해집니다.

### 4. 변경 용이성
객체지향 생활 체조는 객체를 작게 유지하고, 각 메서드를 단일 책임 원칙(SRP)을 따르도록 권장합니다. 이로인해, 특정 객체의 로직을 변경할 때 다른 객체들에 변경 파급 효과를 덜 미치게 할 수 있습니다.

### 5. 확장성 증가
객체지향 생활 체조는 확장성을 고려하여 코드를 설계하는 데 도움을 줍니다. 예를 들어, “한 줄에 점을 하나만 찍는다"라는 원칙은 특정 객체가 내부적으로 다른 객체에 대한 의존성을 줄일 수 있도록 유도합니다. 이를 통해 코드의 변경과 확장성을 높일 수 있습니다.

---
# 객체지향 생활 체조 원칙 살펴보기
이제 본격적으로 9가지의 원칙들을 하나씩 살펴보겠습니다.

## 1. 한 메서드에는 오직 한 단계의 들여 쓰기만 한다.
### 목적
들여쓰기의 단계가 많아지면 메서드의 코드 복잡도가 자연스럽게 증가하고, 코드의 흐름을 파악하기 어려워집니다. 이 원칙은 메서드의 코드 복잡도를 낮추고, 책임을 명확하게 나누는 것을 유도합니다. 즉, 하나의 메서드가 한 가지 역할만 수행하게 하여 **단일 책임 원칙(SRP)**을 준수하는것을 목적으로 합니다.

### 원칙이 적용되지 않았을 때 문제점
```java
public int calculate(final int[] numbers) {
    int sum = 0;

    for (int number : numbers) {    // 첫 번째 들여쓰기
        if (number > 0) {    // 두 번째 들여쓰기  
            sum += number;
        }
    }

    return sum;
}
```

메서드 안에 중첩된 제어문이 여러 개 포함되면, 코드의 흐름을 이해하기 어려워집니다. 조건문이 많아질수록 메서드의 의도가 불명확해지고, 코드의 유지보수 역시 그만큼 어려워집니다.

### 원칙을 적용하여 개선
```java
public int calculateSum(final int[] numbers) {
    return sumPositiveNumbers(numbers);
}

private int sumPositiveNumbers(final int[] numbers) {
    int sum = 0;

    for (int number : numbers) {
        sum = addIfPositive(sum, number);  // 들여쓰기 한 단계만 적용
    }

    return sum;
}

private int addIfPositive(final int sum, final int number) {
    // 별도의 메서드로 분리하여 조건 로직 단순화
    if (number <= 0) {
        return sum;
    }
    
    return sum + number;
}
```

메서드를 작게 분리하여 각 메서드가 명확한 역할을 수행하도록 코드를 개선하였습니다. 덕분에 코드의 가독성이 높아지고, 특정 기능을 수정할 때 필요한 기능을 담당하는 메서드를 독립적으로 수정할 수 있습니다.

참고로 위 코드는 다음과 같이 **람다 & 스트림**을 사용해 개선할 수도 있습니다.
```java
public int calculateSum(final int[] numbers) {
    return sumPositiveNumbers(numbers);
}

private int sumPositiveNumbers(final int[] numbers) {
    return Arrays.stream(numbers)
                 .filter(number -> number > 0)  // 양수인 경우만 필터링
                 .sum();  // 양수들의 합 계산
}
```

### 주의할 점
메서드가 너무 간단하여 분리할 필요가 없는 경우. 예를 들어, 한두 줄로 끝나는 간단한 조건문을 모두 분리하면 코드가 오히려 더 복잡해질 수 있습니다. 메서드를 분리할 때는 코드의 의도가 명확해지는지를 판단 기준으로 삼고, 단순히 원칙을 따르기 위해 무작정 분리하지 않아야 합니다.

## 2. else 예약어를 쓰지 않는다.
### 목적
`else`문은 대부분의 상황에서 코드의 흐름을 복잡하게 만들고, 의도를 명확히 파악하기 어렵게 만듭니다. 이 원칙은 `else`문을 지양 하여 코드의 논리 흐름을 쉽게 이해할 수 있도록 유도합니다.

### 원칙이 적용되지 않았을 때 문제점
```java
public String getGrade(final int score) {
    if (score >= 90) {
        return "A";
    } else if (score >= 80) {
        return "B";
    } else if (score >= 70) {
        return "C";
    } else {
        return "D";
    }
}
```

`else if`문과 `else`문이 반복적으로 사용되어 코드의 논리 흐름을 쉽게 파악하기 어렵고, 조건문을 해석해야 하는 비용이 증가합니다.

### 원칙을 적용하여 개선
```java
public String getGrade(final int score) {
    if (score >= 90) {
        return "A";
    }

    if (score >= 80) {
        return "B";
    }

    if (score >= 70) {
        return "C";
    }

    return "D";
}
```

`else`문을 모두 제거하고, 각 조건을 명확하게 표현하여 논리의 흐름이 단순해졌습니다. 코드를 읽는 사람은 이전 코드보다 더 수월하게 조건문을 따라갈 수 있으며, 특정 조건에 대한 변경이 필요할 때 수정하기가 더 용이합니다.

### 주의할 점
조건문이 너무 많아지고,` if-else` 분기가 필요한 복잡한 상황이라면 무조건적인 `else`문 제거가 오히려 코드의 길이를 늘려 더 복잡해질 수 있습니다.

복잡한 분기 로직이 필요할 때는 무조건 적인 `else`문 제거보다는 적절한 **디자인 패턴(전략 패턴)**을 사용하여 코드를 개선하는것이 더 나은 선택지가 될 수 있습니다.

## 3. 모든 원시값과 문자열을 포장한다.
### 목적
원시값은 특별한 의미(행위)를 담지 못하고, 여러 로직에 사용되는 과정에서 실수를 유발할 가능성이 높습니다. 이 원칙은 원시값을 도메인 개념에 맞는 객체로 포장하여 의미를 명확히 하고, 로직의 안정성을 높이는 것을 유도합니다.

원시값 대신 **VO(Value Object)**를 사용하여 명확한 코드의 의미를 전달하고, 해당 값에 대한 검증과 관련된 기능을 한곳에 모으는 것을 목적으로 합니다. 이로인해 특정 VO 로직의 테스트 작성 용이성도 높아집니다.

### 원칙이 적용되지 않았을 때 문제점
```java
public class User {

    private final String name;
    private final int age;

    public User(final String name, final int age) {
        this.name = name;
        this.age = age;
    }
}
```

이름과 나이에 대한 별도의 검증 로직을 `User`객체 내부에 작성해야하기 때문에 `User` 객체의 코드량이 늘어나며 테스트 코드의 길이 역시 늘어납니다. 또한 `age`와 `name`이라는 변수 이름을 제외하고는 의미를 명확하게 전달할 방법이 없으며, 로직이 뒤섞인다면 더욱 이해하기 어려워집니다.

### 원칙을 적용하여 개선
```java
public class User {

    private final UserName name;
    private final Age age;

    public User(final UserName name, final Age age) {
        this.name = name;
        this.age = age;
    }
}

public class UserName {

    private final String value;

    public UserName(final String value) {
        if (value == null || value.isBlank()) {
            throw new IllegalArgumentException("사용자 이름은 null 혹은 공백일 수 없습니다.");
        }

        this.value = value;
    }
}

public class Age {

    private final int value;

    public Age(final int value) {
        if (value <= 0) {
            throw new IllegalArgumentException("사용자 나이는 음수일 수 없습니다.");
        }

        this.value = value;
    }
}
```

이름과 나이를 별도의 값 객체로 만들어 값의 유효성 검증을 각 클래스에서 수행하도록 책임을 위임하였습니다. 이를 통해 데이터의 일관성이 보장되고, 잘못된 값이 들어오는 것을 방지할 수 있습니다.

### 주의할 점
너무 단순한 값이나 자주 바뀌지 않는 값에 대해 포장할 때는 코드가 과도하게 복잡해질 수 있습니다. 따라서 중요한 **도메인 개념**(ex: 사용자 이름, 이메일 주소 등)에만 적용하고, 단순히 수치 계산에 사용되는 값들은 포장하지 않아도 괜찮습니다.

## 4. 한 줄에 하나의 점만 찍는다.
### 목적
이 원칙은 **디미터 법칙**을 준수하도록 하기 위헤 제안되었으며, 객체 간의 결합도를 낮추고 캡슐화를 강화하는 데 목적이 있습니다. 여러 단계의 객체 참조(a.b.c.d)가 발생하면 메서드가 너무 많은 세부 사항을 알고 있다는 신호입니다. 즉, 객체가 자신의 내부 구조를 외부에 노출하게 되어 캡슐화(encapsulation)가 깨지고, 코드의 변경 시 파급 효과가 커질 수 있습니다.

이 원칙을 지킴으로써 각 객체가 다른 객체의 세부 구현을 모른 채로도 상호작용할 수 있도록 하여 코드의 응집도를 높이도록 유도합니다.

참고로 **람다 & 스트림**의 메서드 체이닝 문법은 이 원칙에 관련되어 있지 않습니다.

### 원칙이 적용되지 않았을 때 문제점
```java
public class Order {

    private final Customer customer;

    public Order(final Customer customer) {
        this.customer = customer;
    }

    public String getCustomerStreetName() {
        return customer.getAddress().getStreet().getName();  // 여러 단계의 객체 접근
    }
}

class Customer {

    private final Address address;

    public Address getAddress() {
        return address;
    }
}

class Address {

    private final Street street;

    public Street getStreet() {
        return street;
    }
}

class Street {

    private final String name;

    public String getName() {
        return name;
    }
}
```

`Order` 클래스는 `Customer`, `Address`, `Street` 클래스의 세부 구조에 대한 지식을 모두 가지고 있습니다.

만약 `Address` 클래스의 구조가 바뀐다면, `Order` 클래스도 수정해야 합니다. 예를 들어, `Address` 클래스가 더 이상 `Street`클래스를 포함하지 않게 되면 `Order` 클래스가 깨지게 됩니다.

또 한 코드가 여러 객체의 내부를 탐색하므로 결합도가 높고, 객체 간 의존성이 커집니다.

### 원칙을 적용하여 개선
```java
public class Order {

    private final Customer customer;

    public Order(final Customer customer) {
        this.customer = customer;
    }

    public String getCustomerStreetName() {
        return customer.getStreetName();  // Customer에게 메시지를 보내서 정보 요청
    }
}

class Customer {

    private final Address address;

    public Customer(final Address address) {
        this.address = address;
    }

    public String getStreetName() {
        return address.getStreetName();  // 내부 구조를 노출하지 않고 필요한 정보만 제공
    }
}

class Address {

    private final Street street;

    public Address(final Street street) {
        this.street = street;
    }

    public String getStreetName() {
        return street.getName();  // Address가 내부적으로 처리
    }
}

class Street {

    private final String name;

    public Street(final String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

**디미터 법칙**을 적용하여, 직접 접근 대신 메시지 전달 방식을 사용하도록 코드를 개선합니다.

`Order` 클래스는 이제 `Customer` 클래스의 구조에 대해서만 알고 있으며, `Address`나 `Street`의 내부 구조를 알 필요가 없어졌습니다.

덕분에 객체간의 결합도가 낮아지고, `Address`나 `Street` 클래스의 구조가 바뀌어도 `Customer` 클래스만 수정하면 되므로 유지보수성이 향상됩니다.

또한, **캡슐화**가 강화되어 각 클래스의 내부 구현이 외부에 노출되지 않게 됩니다.

### 주의할 점
너무 단순한 데이터 클래스(DTO, VO)와의 상호작용에서 이 원칙을 지키기 위해 과도하게 캡슐화를 적용하면 오히려 코드의 복잡도가 높아질 수 있습니다. 그리고 작은 프로젝트나 임시적으로 작성된 코드에서는 지나치게 규칙을 따르는 것이 오히려 개발 속도를 떨어뜨릴 수 있습니다.

디미터 법칙을 적용할 때는 **어떤 객체가 핵심적인 역할을 수행하는지**를 파악하고, 해당 객체의 책임을 명확히 하도록 설계합니다.

## 5. 줄여쓰지 않는다. (축약 금지)
### 목적
변수명, 메서드명, 클래스명 등을 줄여서 작성하면 의미가 불분명해지고, 코드를 읽는 사람이 그 의도를 쉽게 이해할 수 없게 되버립니다. 이 원칙은 축약된 이름 대신, 명확하고 읽기 쉬운 이름을 사용하여 코드의 가독성을 높이는 것이 목적입니다.

**의미 있는 이름**을 사용하여 코드가 무엇을 하는지 쉽게 이해할 수 있도록 합니다. 줄임말이나 약어를 피하고, 구체적이고 직관적인 이름을 사용하여 코드의 의도를 드러내도록 유도합니다.

### 원칙이 적용되지 않았을 때 문제점
```java
public class Emp {

    private final String nm;  // 직원의 이름
    private final int sal;    // 직원의 급여

    public Emp(final String nm, final int sal) {
        this.nm = nm;
        this.sal = sal;
    }

    public String getNm() {
        return nm;
    }

    public int getSal() {
        return sal;
    }
}
```

`Emp`, `nm`, `sal` 등과 같은 축약된 이름은 코드를 읽는 사람이 바로 그 의미를 이해하기 어렵습니다. 이는 코드의 의도를 파악하기 위한 추가적인 설명이 요구되고, 코드 가독성을 크게 떨어뜨립니다.

다른 개발자가 코드를 수정하거나 유지보수할 때 이 변수나 클래스가 무엇을 의미하는지 추측해야 하는 문제가 발생할 수 있습니다.

### 원칙을 적용하여 개선
```java
public class Employee {

    private final String name;  // 명확한 이름 사용
    private final int salary;

    public Employee(final String name, final int salary) {
        this.name = name;
        this.salary = salary;
    }

    public String getName() {
        return name;
    }

    public int getSalary() {
        return salary;
    }
}
```

축약된 이름 대신 `Employee`, `name`, `salary`와 같이 의미가 명확한 이름을 사용하여 가독성을 높였습니다. 덕분에 클래스와 변수의 이름을 통해 해당 코드가 무엇을 의미하는지 명확히 이해할 수 있게 되었습니다. 또한, 코드를 읽는 사람이 주석이나 추가적인 설명 없이도 쉽게 이해할 수 있습니다.

### 주의할 점
통용적으로 사용되는 약어는 굳이 풀어쓰지 않아도 괜찮습니다. 개발자들 사이에서 흔히 쓰이는 약어들은 이미 널리 통용되고 쉽게 이해할 수 있기 때문에, 오히려 풀어서 사용하면 코드가 불필요하게 길어지고 가독성이 떨어질 수 있습니다. (ex: DB, URL, SSL, 등)

변수나 메서드 이름은 팀 컨벤션으로 정하는게 가장 좋습니다. 작명하기 전 팀 내 코딩 컨벤션이나 표준 명명 규칙을 확인하고, 널리 사용되는 약어는 컨벤션이 허락하는 선에서 그대로 사용하되, 모호하거나 생소한 약어는 명확한 이름으로 변경합니다.

## 6. 모든 엔티티를 작게 유지한다.
### 목적
클래스나 메서드가 너무 크다는건 여러 책임을 동시에 가지고 있다는 신호일 수 있습니다. 이는 응집도가 떨어지면서 SRP를 위반하고 있을 가능성이 높습니다.

이 원칙은 클래스와 메서드를 작게 나누어 하나의 역할만 가지도록 유도하여 유지보수가 용이하고 테스트 작성이 쉬운 코드를 작성하도록 유도합니다. 즉, 코드의 응집도를 높이고, 결합도를 낮추도록 하는 것이 목적입니다.

### 원칙이 적용되지 않았을 때 문제점
```java
public class OrderProcessor {

    public void processOrder(final String orderDetails) {
        validateOrder(orderDetails);
        saveOrder(orderDetails);
        sendConfirmationEmail(orderDetails);
    }

    private void validateOrder(final String orderDetails) {
        // 주문 검증 로직
    }

    private void saveOrder(final String orderDetails) {
        // 주문 저장 로직
    }

    private void sendConfirmationEmail(final String orderDetails) {
        // 이메일 전송 로직
    }
}
```

`OrderProcessor` 클래스는 검증, 저장, 이메일 전송 등 많은 기능을 담당하고 있습니다. 이는 곧 여러 책임을 동시에 가지고 있다는 의미입니다. 이로 인해 클래스의 역할은 모호해지고, 하나의 메서드를 수정할 때 다른 메서드에 그 파급효과가 퍼질 가능성이 매우 높아집니다.

### 원칙을 적용하여 개선
```java
public class OrderProcessor {

    private final OrderValidator validator;
    private final OrderRepository repository;
    private final EmailService emailService;

    public OrderProcessor(final OrderValidator validator, final OrderRepository repository, final EmailService emailService) {
        this.validator = validator;
        this.repository = repository;
        this.emailService = emailService;
    }

    public void processOrder(final String orderDetails) {
        if (validator.isValid(orderDetails)) {
            repository.save(orderDetails);
            emailService.sendConfirmationEmail(orderDetails);
        }
    }
}

class OrderValidator {
    public boolean isValid(final String orderDetails) {
        // 주문 검증 로직
        return true;
    }
}

class OrderRepository {
    public void save(final String orderDetails) {
        // 주문 저장 로직
    }
}

class EmailService {
    public void sendConfirmationEmail(final String orderDetails) {
        // 이메일 전송 로직
    }
}
```

`OrderProcessor`의 책임을 각각 `OrderValidator`, `OrderRepository`, `EmailService`로 나누어 하나의 클래스가 하나의 책임을 가지고 역할을 수행하도록 코드를 개선하였습니다.

`OrderProcessor` 클래스는 이제 각 클래스를 조합하여 전체 주문 프로세스를 관리하는 역할만 수행하며, 각 개별 로직은 분리되어 응집도가 높아지고 테스트 코드를 작성하기 매우 쉬워졌습니다.

또한, 독립적인 각 클래스들은 내부 로직이 변경되더라도 다른 클래스에 영향을 크게 끼치지 않으므로 유지보수성과 확장성 역시 크게 높아졌습니다.

### 주의할 점
너무 과도하게 클래스나 메서드를 분리하면 그만큼 관리할 엔티티가 늘어나고, 코드를 읽는 사람의 입장에서 탐색해야할 엔티티 개수가 굉장히 많아지므로 오히려 코드를 읽기 어렵게 만들 수 있습니다.

각 클래스나 메서드가 여러 책임을 가져 테스트 코드 작성이나 코드 변경이 어렵다고 판단될 때 엔티티를 분리하는 것이 가장 좋은 타이밍입니다.

## 7. 3개 이상의 인스턴스 변수를 가진 클래스를 사용하지 않는다.
### 목적
하나의 클래스에 너무 많은 인스턴스 변수가 존재한다면, 그 클래스는 여러 책임을 동시에 수행하고 있을 가능성이 높습니다. 이는 **단일 책임 원칙(SRP)**을 위반하게 되며, 클래스가 너무 많은 데이터를 다루기 때문에 코드가 복잡해질 수 있습니다.

이 원칙은 인스턴스 변수의 개수를 제한하여 각 클래스가 **명확한 책임**을 가져 응집도를 높이고 결합도를 낮추도록 유도하는 것이 목적입니다.

### 원칙이 적용되지 않았을 때 문제점
```java
public class Order {

    private final String productName;
    private final int productPrice;
    private final String customerName;
    private final String customerEmail;

    public Order(final String productName, final int productPrice, final String customerName, final String customerEmail) {
        this.productName = productName;
        this.productPrice = productPrice;
        this.customerName = customerName;
        this.customerEmail = customerEmail;
    }

    public String getProductName() {
        return productName;
    }

    public int getProductPrice() {
        return productPrice;
    }

    public String getCustomerName() {
        return customerName;
    }

    public String getCustomerEmail() {
        return customerEmail;
    }
}
```

`Order` 클래스는 총 4개의 인스턴스 변수를 가지고 있어 여러 가지 데이터를 동시에 다루고 있습니다. 이로 인해 클래스의 책임이 명확하지 않으며, 데이터가 많아질수록 클래스가 더 복잡해집니다.

만약 고객 정보나 제품 정보가 변경된다면 `Order` 클래스를 직접 수정해야 하고, 코드의 유지보수성이 떨어집니다.

### 원칙을 적용하여 개선
```java
public class Order {

    private final Product product;         // 제품 정보 객체로 분리
    private final Customer customer;       // 고객 정보 객체로 분리

    public Order(final Product product, final Customer customer) {
        this.product = product;
        this.customer = customer;
    }

    public Product getProduct() {
        return product;
    }

    public Customer getCustomer() {
        return customer;
    }
}

class Product {

    private final String name;
    private final int price;

    public Product(final String name, final int price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public int getPrice() {
        return price;
    }
}

class Customer {

    private final String name;
    private final String email;

    public Customer(final String name, final String email) {
        this.name = name;
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public String getEmail() {
        return email;
    }
}
```

`Product`와 `Customer` 클래스를 분리하여 `Order` 클래스의 인스턴스 변수를 2개로 줄였습니다. 이제 각 클래스가 자신의 역할에 집중할 수 있도록 책임이 분리되어 코드의 응집도가 높아졌습니다.

만약 제품 정보나 고객 정보가 변경되더라도 다른 클래스에 아무런 영향을 주지 않고 쉽게 각 클래스를 변경할 수 있게 되었습니다.

### 주의할 점
모든 클래스의 인스턴스 변수를 3개 이하로 강제적으로 줄이려고 하면, 오히려 클래스의 수가 과도하게 많아져 코드의 복잡도가 올라갈 수 있습니다.

특히 **DTO(Data Transfer Object)**와 같이 단순히 데이터를 전달하는 용도의 객체에서는 이 규칙을 너무 엄격하게 적용하는게 오히려 비효율적일 수 있습니다.

클래스의 응집도가 높은지를 먼저 판단한 후, 응집도가 낮고 너무 많은 책임을 가지고 있을 때만 책임을 분리하여 인스턴스 변수를 줄입니다. 따라서 원칙 그대로 **인스턴스 변수 2개 이하**라는 개수에 집착하는게 아닌, **클래스가 하나의 명확한 역할을 가지는가**를 판단 기준으로 삼아야 합니다.

## 8. 일급 컬렉션을 사용한다.
### 목적
`List`, `Set`, `Map` 등의 컬렉션을 사용할 때, 이 컬렉션이 직접 노출되면 컬렉션을 사용하는 곳마다 관련된 로직이 중복되거나, 컬렉션의 상태가 외부에서 변경될 위험이 존재합니다. 

**일급 컬렉션**은 컬렉션을 포장한 객체로, 컬렉션과 관련된 모든 로직을 한곳에 모아 응집도를 높이고 캡슐화를 강화하기 위해 제안되었습니다.

컬렉션을 일급 컬렉션으로 포장하여 컬렉션 내부의 상태를 안전하게 보호하고, 컬렉션과 관련된 로직을 한곳에서 관리하여 코드의 **응집도**와 **재사용성**을 높이도록 유도하는게 목적입니다.

### 원칙이 적용되지 않았을 때 문제점
```java
public class Team {

    private final List<Member> members;  // 컬렉션이 직접 노출됨

    public Team(final List<Member> members) {
        this.members = members;
    }

    public List<Member> getMembers() {
        return members;  // 컬렉션을 직접 반환하여 외부에서 수정 가능
    }

    public void addMember(Member member) {
        members.add(member);
    }
}

class Member {

    private final String name;

    public Member(final String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

`Team` 클래스가 컬렉션(`members`)을 외부에 직접 노출하여 외부에서 컬렉션을 변경할 여지가 있습니다. 만약 `getMembers()`를 호출한 후, `members` 리스트에 직접 접근하면 요소를 제거하거나 추가할 수 있어 객체의 상태가 예기치 않게 변경될 수 있습니다.

또한, 컬렉션과 관련된 로직(`add`, `remove` 등)이 여러 곳에 분산되면 코드의 응집도가 낮아지고, 컬렉션 상태를 일관되게 유지하기가 어렵습니다.

### 원칙을 적용하여 개선
```java
public class Team {

    private final Members members;  // 일급 컬렉션으로 포장

    public Team(final List<Member> members) {
        this.members = new Members(members);
    }

    public Members getMembers() {
        return members;
    }
}

class Members {  // 일급 컬렉션

    private final List<Member> members;

    public Members(final List<Member> members) {
        this.members = new ArrayList<>(members);  // 외부 리스트를 내부적으로 복사하여 안전하게 관리
    }

    public void addMember(final Member member) {
        members.add(member);
    }

    public List<Member> getMembers() {
        return Collections.unmodifiableList(members);  // 외부에 불변 리스트 제공
    }
}
```

컬렉션을 `Members` 일급 컬렉션으로 포장하여 컬렉션과 관련된 로직을 `Members` 클래스에 응집시켰습니다. 

외부에 컬렉션의 상태를 변경할 수 없도록 `getMembers()`가 불변 리스트를 반환하므로 객체의 상태가 **캡슐화**되었습니다.

또한 컬렉션의 상태 변경(`addMember` 등)은 일급 컬렉션 내에서만 관리되므로 **컬렉션 상태의 일관성**이 보장됩니다.

### 주의할 점
단순한 데이터 전달 용도의 DTO나, 컬렉션의 상태를 일시적으로 사용하는 경우에는 일급 컬렉션으로 만드는게 오히려 코드의 복잡성을 불필요하게 높일 수 있습니다.

컬렉션의 상태를 관리하거나 변경하는 로직이 많을 경우에만 일급 컬렉션을 활용합니다. 만약 단순히 데이터를 담기 위한 용도라면 굳이 일급 컬렉션으로 포장할 필요가 없을 수 있습니다.

## 9. Getter/Setter/Property를 무분별하게 사용하지 않는다.
### 목적
`Getter`, `Setter`를 무분별하게 사용하면 객체의 상태가 외부에서 쉽게 변경될 수 있어 **객체의 캡슐화가 깨지게 됩니다.** 이 원칙은 **객체가 자신의 상태를 스스로 관리**하고, 외부에서 객체의 상태를 직접 조작하지 않도록 유도합니다.

객체지향 설계의 기본 원칙인 **캡슐화(encapsulation)**를 지키고, 객체가 자신의 책임을 명확하게 잘 수행하는 코드를 설계하도록 유도하는 것이 목적입니다. `Getter`와 `Setter`를 무분별하게 사용하면 **객체가 단순히 데이터를 저장하고 전달하는 DTO처럼 동작**하게 되어 객체지향의 본질적인 개념이 사라질 수 있습니다.

**Property**는 객체의 **내부 상태**를 외부에서 쉽게 접근하고 수정할 수 있도록 만든 속성을 의미합니다. 자바에서는 Property가 직접적으로 언어적인 기능으로 제공되지 않지만, `Getter`와 `Setter` 메서드를 통해 사실상 Property처럼 사용할 수 있습니다. 따라서 아래 예제 코드는 `Getter`와 `Setter`예시만 다룹니다.

### 원칙이 적용되지 않았을 때 문제점
```java
public class User {

    private final String name;
    private final int age;

    // Getter
    public String getName() {
        return name;
    }

    // Setter
    public void setName(final String name) {
        this.name = name;
    }

    // Getter
    public int getAge() {
        return age;
    }

    // Setter
    public void setAge(int age) {
        this.age = age;
    }
}
```

`setName` & `setAge` 메서드를 통해 외부에서 객체의 상태를 마음대로 변경할 수 있으므로, 객체의 내부 상태를 안전하게 보호하지 못합니다. 이는 **캡슐화 위반** 입니다.

객체가 자신이 관리해야 할 데이터를 외부에 쉽게 노출하기 때문에, 객체가 **자율적으로 상태를 관리하는 것**이 아닌, 외부에서 제어하는 **수동적인 객체**가 되버립니다. 즉, 객체의 책임이 모호해집니다.

객체의 데이터가 외부에서 변경될 수 있기 때문에, 객체가 원래의 목적에 맞는 책임을 수행하지 못하고, 객체의 데이터와 행동이 분리되어 **응집도가 떨어집**니다.

### 원칙을 적용하여 개선
```java
public class User {

    private final String name;
    private final int age;

    public User(final String name, final int age) {
        this.name = name;
        this.age = age;
    }

    // 이름을 변경하는 메서드
    public void changeName(final String newName) {
        if (newName == null || newName.isBlank()) {
            throw new IllegalArgumentException("Name cannot be null or empty");
        }
        this.name = newName;
    }

    // 나이를 변경하는 메서드
    public void haveBirthday() {
        this.age += 1;
    }

    // 나이에 대한 정보 제공 (단순히 상태를 전달하는 게터가 아닌 의미 있는 동작)
    public boolean isAdult() {
        return age >= 18;
    }
}
```

`User` 객체가 스스로 자신의 상태를 관리하고, 상태 변경에 대한 규칙을 객체 내부에서 정의하므로 **캡슐화가 강화**되었습니다.

`changeName` 메서드는 단순히 `setName`처럼 상태를 외부값 그대로 변경하는 것이 아니라, **이름이 올바른지 유효성을 검증**하는 로직을 포함하는등 능동적인 역할을 가지고 있습니다.

`haveBirthday`와 같은 **의미 있는 행동**을 통해 객체의 상태가 변화하도록 설계하여 **객체지향의 설계 원칙**을 준수하였습니다.

`isAdult` 메서드는 단순히 나이를 반환하는 `Getter`가 아니라, 객체의 상태에 따라 능동적으로 특정한 상태를 반환하는 메서드입니다.

### 주의할 점
단순한 데이터 전달 객체(DTO)와 같은 경우에는 `Getter`와 `Setter`를 사용하는 것이 더 효율적일 수 있습니다. **DTO**는 주로 데이터를 전달하거나, 계층 간의 데이터 교환을 위해 사용되므로, 이때는 `Getter`와 `Setter`를 통해 필드에 접근해도 무방합니다.

또한 원시값과 문자열을 래핑한 객체 역시 `Getter`를 통해 데이터를 반환하도록 로직을 작성해야하는 상황이 존재합니다.

**비즈니스 로직이 포함된 도메인 객체**에서는 `Getter`와 `Setter`를 줄이고, 해당 필드와 관련된 의미 있는 메서드를 만들어 **객체가 자신의 상태를 스스로 관리**하도록 설계합니다. 반대로 **단순 데이터 전송 혹은 관리**가 목적인 DTO와 Wrapping 객체는 예외적으로 `Getter`와 `Setter`를 허용하여, 필요한 데이터를 효율적으로 전달하도록 합니다.

이 원칙은 무조건적으로 모든 `Getter`와 `Setter`를 금지하라는 것이 아닙니다. 중요한 것은 **객체가 자신의 상태를 안전하게 관리하도록 설계**하고, 외부에서 객체의 상태를 직접 조작하지 못하게 하는 것이 주요 목적입니다.

---
# 객체지향 생활 체조 주의점
객체지향 생활 체조가 높은 품질의 코드를 작성하는데 많은 도움을 준다는건 사실이나 반드시 모든 상황에서 정답이 될 수는 없습니다. 단순히 원칙을 지키는 것만으로는 좋은 코드가 완성되지 않기 때문에, 여러 상황을 고려해서 적절하게 활용하는 것이 매우 중요합니다. 아래는 객체지향 생활 체조 원칙을 적용할 때 생각해볼만한 주의점들 입니다.

## 1. 원칙을 맹목적으로 따르려 하지 말 것
객체지향 생활 체조의 원칙들은 코드 품질을 높이기 위해 제안된 좋은 가이드라인이지만, 모든 원칙을 무조건적으로 적용하다 보면 오히려 코드를 과도하게 분리하게 되거나, 불필요한 클래스와 메서드가 많아져서 코드의 복잡성이 증가할 수 있습니다.

## 2. 과도한 분리와 추상화 방지
“모든 원시값과 문자열을 포장한다"와 같은 원칙은 원시값(Primitive Type)을 단순하게 사용하는 것을 방지하여 의미를 명확하게 하기 위해 제안된 것입니다. 하지만, 무조건 모든 숫자나 문자열들을 객체로 포장한다면 클래스의 수가 지나치게 많아져 코드가 과도하게 복잡해지고 관리할 영역만 늘어나버릴 수 있습니다.

## 3. 코드의 목적과 의도를 분명히 할 것
객체지향 생활 체조의 규칙을 따르다 보면 메서드를 지나치게 적은 단위로 분리하게 되는 경우가 있습니다. 특히 "한 메서드에 들여쓰기를 한 단계만 사용한다"는 규칙을 지키려고 메서드를 잘개 쪼개다 보면, 오히려 메서드의 의도가 명확하지 않고, 메서드 간의 호출 관계를 추적하기가 어려워질 수 있습니다.

## 4. 적절한 캡슐화와 역할 분리
"Getter/Setter/Property를 무분별하게 사용하지 않는다."는 객체의 내부 상태를 외부에서 조작하지 못하도록 **캡슐화(encapsulation)**를 강화하기 위해 제안된 원칙입니다. 하지만, 무조건적으로 `Getter`와 `Setter`를 제거하려고 하면 객체 간의 협력을 어렵게 만들거나 객체의 유연성을 떨어뜨릴 수 있습니다. 또한 오히려 불필요한 메서드를 작성하게 되어 코드의 가독성이 오히려 떨어질 수 있습니다.

---
# 마무리
어떤 기술, 전략이든 세상에 **은탄환(Silver bullet)**은 존재하지 않습니다. 왜 이러한 원칙이 필요한지 생각하지 않고 무작정 코드에 적용하려고 한다면 오히려 원했던 방향과 다르게 코드가 더욱 망가질 수 있습니다.

객체지향 프로그래밍의 본질이 무엇인지, 왜 객체지향적인 코드를 작성하려고 하는 것인지, 나아가 정말 객체지향적인 코드가 정답인지를 먼저 생각한 후 위에서 살펴본 원칙을 적절하게 적용한다면 우린 전보다 더 나은 코드를 작성할 수 있을 것입니다.
