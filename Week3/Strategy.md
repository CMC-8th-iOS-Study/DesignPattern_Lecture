# 📕Strategy Pattern

Strategy Pattern은 클래스의 행위를 **캡슐화** 하여 **동적**으로 행위를 자유롭게 바꿀 수 있도록 돕는 패턴입니다.

<br>

Strategy Pattern의 구성요소는 3가지로 나뉩니다.

<img src="https://t1.daumcdn.net/cfile/tistory/9997303C5E0DC6830E">

###### ***<Strategy pattern의 다이어그램>***

>1. Strategy를 사용할 객체
>2. Strategy를 정의하는 프로토콜
>3. 2번의 프로토콜을 구현한 Strategy객체

두 개 이상의 유사한 동작이 필요하고, 이 동작이 유연하게 바뀌기를 원할 때 사용하면 좋습니다.

<br><br><br>

**Delegate패턴과 굉장히 유사하다. (구성요소만봐도 똑같음)**

<img src="https://t1.daumcdn.net/cfile/tistory/9997353A5E0DC6972C">

###### ***<Delegate pattern의 다이어그램>***

<br>

## 장/단점 ⭐

### 장점

- **런타임** 에서 객체 내부에서 사용되는 알고리즘을 변경 할 수 있습니다.
- 알고리즘을 사용하는 코드와 알고리즘을 구현하는 코드를 분리할 수 있습니다.
- **Open / Closed Principle(개방 폐쇄 원칙)을 준수**합니다. **Context(SuperClass)를 변경하지 않고도** 새로운 Strategy를 도입할 수 있습니다.

### 단점

- 알고리즘이 몇 개 없고 변경되는 일도 거의 없는 경우 전략 패턴의 도입이 오히려 복잡성을 증가시킬 수 있습니다.
- 클라이언트가 적절한 Strategy를 선택하기 위해서는 각각의 차이점을 알고 있어야 합니다.
**(각각의 알고리즘군 특성을 잘 알아야함)**
- Strategy, Context간 통신 오버헤드가 발생합니다.
**(같은 행동군 안에서 다른 행동을 하기위해선 행동 클래스를 변경해줘야함. 이 변경 과정이 오버헤드)**

<br>

<hr>

<br>

### 📌사용 예시

먼저 Strategy 인터페이스 역할을 할 프로토콜을 하나 정의해줍니다.
(행동군)

```swift
// 행동군 을 집합화!
protocol FindRouteBehavior { 
    // 길찾기 (자동차, 도보, 자전거)
    func findRoute() 
}

protocol SearchBehavior {
    // 검색. (도로명, 지번)
    func search() 
}
```

이번에는 Strategy 프로토콜을 채택하는 알고리즘들을 만들어주면 됩니다.<br>
네비게이션으로 자동차, 도보, 자전거 경로를 찾는 Strategy 프로토콜을 채택한 3개의 클래스를 만들어줍니다.

```swift
// Concrete Strategy
class CarRoute: FindRouteBehavior {
    func findRoute() {
        print("자동차 경로 찾기 완료!")
    }
}

// Concrete Strategy
class WalkRoute: FindRouteBehavior {
    func findRoute() {
        print("도보 경로 찾기 완료!")
    }
}

// Concrete Strategy
class BikeRoute: FindRouteBehavior {
    func findRoute() {
        print("자전거 경로 찾기 완료!")
    }
}

class LoadName: SearchBehavior {
    func search() {
        print("도로명으로 주소 검색!\n")
    }
}

class NumberName: SearchBehavior {
    func search() {
        print("지번으로 주소 검색!\n")
    }
}
```

그런 뒤 만든 알고리즘들을 교체해가며 사용할 Context를 구현합니다.

```swift
// Context
class Navigation {
    private var routeBehavior: FindRouteBehavior? // 길찾기 (자동차, 자전거, 도보) 행동군/알고리즘 군
    private var searchBehavior: SearchBehavior? // 주소 검색 (도로명, 지번) 행동군/알고리즘 군
    
    func findRoute() {
        self.routeBehavior?.findRoute()
    }
    func searchAddress() {
        self.searchBehavior?.search()
    }
    
    func setRouteBehavior(behavior: FindRouteBehavior) {
        self.routeBehavior = behavior
    }
    func setSearchBehavior(behavior: SearchBehavior) {
        self.searchBehavior = behavior
    }
}
```

**실행 부분**

```swift
func main(){
    let navigation: Navigation = Navigation()
    
        // 초기 세팅
    navigation.setRouteBehavior(behavior: CarRoute())
    navigation.setSearchBehavior(behavior: LoadName())
    
    navigation.findRoute()
    navigation.searchAddress()
    
        // 요구사항의 변화가 생겼을 경우, 다른 행동 패턴을 대입
    navigation.setRouteBehavior(behavior: BikeRoute())
    navigation.setSearchBehavior(behavior: NumberName())
    
    navigation.findRoute()
    navigation.searchAddress()
}
```


Strategy 객체를 참조하고 있는 Context 클래스를 만들었다면 끝입니다.

실제로 사용을 해보면, 다음과 같습니다.

<img width="536" alt="스크린샷 2021-10-22 오후 6 26 03" src="https://user-images.githubusercontent.com/55231029/138430059-5b9d5da6-9a6d-401f-9f00-23d507a8af16.png">


<!-- <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FClOpR%2Fbtq8wmVKNlT%2FZwpKZHayXtFqKOzUgAmuIk%2Fimg.png" width="50%">

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbajEwH%2Fbtq8ujlFIEt%2FeICBC5WiORWHAnJtyOaQZ1%2Fimg.png" width="250"> -->

위의 결과를 보면 계속해서 Strategy 객체를 변경하며 다른 알고리즘을 사용하는 것을 볼 수 있습니다.

<br>
<br>
<br>

---

# 부록

## 디자인 원칙

### **애플리케이션에서 달라지는 부분을 찾아내고, 달라지지 않는 부분으로부터 분리시킨다.**

- 바뀌는 부분을 따로 뽑아서 캡슐화. 
바뀌지 않는 부분에는 영향을 미치지 않은 채로 바뀌는 부분만 유지 보수하기 용이하다.

### 구현이 아닌 인터페이스에 맞춰서 프로그래밍 한다.

- '인터페이스에 맞춰서 프로그래밍 한다.' 라는 말은 즉, "상위 형식에 맞춰 프로그래밍 한다." 라는 말과 동일하다.
- 다형성을 이용해 상위 추상 클래스나 인터페이스와 같은 **상위 형식** 으로 선언 후  
실행시에 구체적으로 구현된 객체를 대입해주면 된다.

### 상속보다는 구성을 활용한다.

- 예를 들어 Duck이라는 슈퍼 클래스,  그의 서브 클래스들에서 행동을 직접 구현하기보단
특정 역할군(클래스) 을 묶어 역할군 마다 인터페이스를 상속, 역할군(클래스) 에서 구체적인 행동을 구현
- "A(Duck) 에는 B(Behavior) 가 있다." 관계를 구성이라 표현.
행동 클래스를 상속받는 대신 변수(프로퍼티)를 사용함으로서 행동을 부여받는다.

```swift
class Duck {
	var flyBehavior: FlyBehavior
	var quackBehavior: QuackBehavior

	func ....
}
```


