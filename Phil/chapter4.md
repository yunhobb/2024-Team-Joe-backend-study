# item 15 

## 클래스와 멤버의 접근 권한을 최소화하라 

### 모든 클래스와 멤버의 접근성을 가능한 한 좁혀야 한다. 

```
- private: 멤버를 선언한 톱 클래스에서만 접근 가능
- package-private: 멤버가 소속된 모든 패키지에서 접근 가능
- protected: package-private + 멤버를 선언한 클래스의 하위 클래스에서도 접근 가능
- public: 모든 곳에서 접근 가능
```

### public 클래스의 인스턴스 필드는 되도록 public이 아니어야 한다. 그 필드에 담을 수 있는 값을 제한할 힘을 잃기 때문. 
### public static final 배열 필드나 이 필드를 반환하는 접근자 메서드를 제공해서는 안된다. 길이가 0이 아닌 배열은 모두 변경 가능하니 주의가 필요함. 

# item 16 

## public 클래스에서는 public 필드가 아닌 접근자 메서드를 사용하라 

### 인스턴스 필드들을 모아놓는 일 외에는 아무 목적 없는 퇴보한 클래스 

```
class Point {
    public double x;
    public double y;
}

이런 클래스는 필드를 모두 private으로 바꾸고 public 접근자를 추가한다. Public 클래스라면 접근자를 제공함으로써 클래스 내부 표현 방식을 언제든 바꿀 수 있음. 
public 클래스가 아니라 package-private zmffotm ghrdms private 중첩 클래스라면 데이터 필드를 노출한다 해도 하등의 문제가 없다. 
```

# item 17 

## 변경 가능성을 최소화하라 

### 클래스를 불변으로 만드는 다섯 가지 규칙 

```
1. 객체의 상태를 변경하는 메서드(변경자)를 제공하지 않는다. 
2. 클래스를 확장할 수 없도록 한다. 
3. 모든 필드를 final로 선언한다. 
4. 모든 필드를 private으로 선언한다. 
5. 자신 외에는 내부의 가변 컴포넌트에 접근할 수 없도록 한다. 
```

### 불변 클래스 장점 
```
- 불변 객체는 단순하다. 
- 불변 객체는 근본적으로 스레드 안전하여 따로 동기화할 필요 없다. 
- 불변 객체는 안심하고 공유할 수 있다. 
- 불변 객체는 자유롭게 공유할 수 있음은 물론, 불변 객체끼리는 내부 데이터를 공유할 수 있다. 
- 객체를 만들 때 다른 불변 객체들을 구성요소로 사용하면 이점이 많다. 
- 불변 객체는 그 자체로 실패 원자성을 제공한다. 
```

### 불변 클래스 단점 
```
- 값이 다르면 반드시 독립된 객체로 만들어야 한다. 
클래스가 꼭 필요한 경ㅇ가 아니라면 불변이어야 한다. 불변으로 만들 수 없는 클래스라도 변경할 수 있는 부분을 최소한으로 줄이자. 
```

# item 18 

## 상속보다는 컴포지션을 사용하라 

### 상속받은 클래스 
```
문제: 
- 상위 클래스의 메서드 동작을 다시 구현하는 방식은 어렵고 시간도 더 들고, 오류를 내거나 성능을 떨어뜨릴 수 있음. 
- 보안의 문제가 생길 수 있음. 

결론: 
따라서 상속은 반드시 하위 클래스가 상위 클래스의 '진짜' 아휘 타입인 상황에서만 쓰여야 한다. 상속은 상위 클래스와 하위 클래스가 순수한 is-a 관계일 때만 써야 한다. 

해결책: 
컴포지션과 전달을 사용하자. 래퍼 클래스는 하위 클래스보다 견고하고 강력하다. 
```

# item 19 

## 상속을 고려해 설계하고 문서화하라. 그러지 않았다면 상속을 금지하라 

### 상속을 고려한 설계와 문서화 

```
- 상속용 클래스는 재정의할 수 있는 메서드들을 내부적으로 어떻게 이용하는지(자기사용) 문서로 남겨야 한다. 
- 클래스의 내부 동작 과정 중간에 끼어들 수 있는 훅을 잘 선별하여 protected메서드 형태로 공개해야 할 수도 있다. 
- 상속용으로 설계한 클래스는 배포 전에 반드시 하위 클래스를 만들어 검증해야 한다. 
- 상속용 클래스의 생성자는 직접적으로든 간접적으로든 재정의 가능 메서드를 호출해서는 안된다. 상위 클래스의 생성자가 하위 클래스의 생성자보다 먼저 실행되기 때문에 하위 클래스에서 재정의한 메서드가 하위 클래스의 생성자보다 먼저 호출된다. 
```

### 상속을 금지하는 방법 

```
1. 클래스를 final로 선언하는 방법
2. 모든 생성자를 private이나 package-private으로 선언하고 public 정적 팩터리를 만들어주는 방법 
```

# item 20 

## 추상 클래스보다는 인터페이스를 우선하라 

### 다중 구현 메커니즘 
```
1. 인터페이스 
2. 추상 클래스 

제일 큰 차이는 추상 클래스가 정의한 타입을 구현하는 클래스는 반드시 추상 클래스의 하위 클래스가 되어야 한다는 점. 하지만 인터페이스가 선언한 메서드를 모두 정의하고 그 일반 규약을 잘 지킨 클래스라면 다른 어떤 클래스를 상속했든 같은 타입으로 취급된다. 
```

### 인터페이스 
```
1. 기존 클래스에도 손쉽게 새로운 인터페이스를 구현해넣을 수 있다. 
2. 인터페이스는 믹스인 정의에 안성맞춤이다. 
3. 인터페이스로는 계층구조가 없는 타입 프레임워크를 만들 수 있다. 
4. 래퍼 클래스 관용구와 함께 사용하면 인터페이스는 기능을 향상시키는 안전하고 강력한 수단이 된다. 
```

# item 21 

## 인터페이스는 구현하는 쪽을 생각해 설계하라 

### 디폴트 메서드 

```
- 디폴트 메서드는 (컴파일에 성공하더라도) 기존 구현체에 런타임 오류를 일으킬 수 있다. 
- 인터페이스를 선계할 때 디폴트 메서드라는 도구가 생겼더라도 주의해야 한다. 
```

# item 22 

## 인터페이스는 타입을 정의하는 용도로만 사용하라 

### 상수 인터페이스 

```
상수 인터페이스: 메서드 없이, 상수를 뜻하는 static final 필드로만 가득 찬 인터페이스를 말한다.

설명: 상수 인터페이스 안티패턴은 인터페이스를 잘못 사용한 예. 상수 인터페이스를 구현하는 것은 내부 구현을 클래스의 API로 노출하는 행위이다. 
```

# item 23 

## 태그 달린 클래스보다는 클래스 계층구조를 활용하라 

### 태그 달린 클래스 단점 

```
1. 장황하고, 오류를 내기 쉽고, 비효율적이다. 
2. 클래스 계층구조를 어설프게 흉내낸 아류일 뿐이다. 
```

### 태크 달린 클래스를 클래스 계층구조로 바꾸는 방법 
```
1. 계층구조의 루트가 될 추상 클래스를 정의하고, 태그 값에 따라 동작이 달라지는 메서드들을 루트 클래스의 추상 메서드로 선언한다. 
2. 태그 값에 상관없이 동작이 일정한 메서드들을 루트 클래스에 일반 메서드로 추가한다. 
3. 모든 하위 클래스에서 공통으로 사용하는 데이터 필드들도 전부 루트 클래스로 올린다. 
4. 루트 클래스를 확장한 구체 클래스를 의미별로 하나씩 정의한다. 
5. 각 하위 클래스에는 각자의 의미에 해당하는 데이터 필드들을 넣는다. 
6. 루트 클래스가 정의한 추상 메서드를 각자의 의미에 맞게 구현한다. 
```

# item 24 

## 멤버 클래스는 되도록이면 static으로 만들라 

### 중첩 클래스: 정적 멤버 클래스, 비정적 멤버 클래스, 익명 클래스, 지역 클래스

```
메서드 밖에서도 사용해야 하거나 메서드 안에 정의하기엔 너무 길다면 멤버 클래스로 만든다. 멤버 클래스의 인스턴스 각각이 바깥 인스턴스를 참조한다면 비정적으로, 그렇지 않으면 정적으로 만들자. 중첩 클래스가 한 메서드 안에서만 쓰이면서 그 인스턴스를 생성하는 지점이 단 한 곳이고 해당 타입으로 쓰기에 적합한 클래스나 인터페이스가 이미 있다면 익명 클래스로 맘ㄴ들고, 그렇지 않으면 지역 클래스로 만들자. 
```

# item 25 

## 톱 레벨 클래스는 한 파일에 하나만 담으라 

### 톱 레벨 클래스를 소스 파일 하나에 여러 개 선언하면 컴파일 오류가 나고 동작이 의도와 다르게 될 수 있다. 