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

<hr>

<br>

### 📌사용 예시

먼저 Strategy 인터페이스 역할을 할 프로토콜을 하나 정의해줍니다.

```
// Strategy
protocol Strategy {
    func algorithmExecute()
}
```

이번에는 Strategy 프로토콜을 채택하는 알고리즘들을 만들어주면 됩니다.<br>
네비게이션으로 자동차, 도보, 자전거 경로를 찾는 Strategy 프로토콜을 채택한 3개의 클래스를 만들어줍니다.

```
// Concrete Strategy
class CarRoute: Strategy {
    func algorithmExecute() {
        print("자동차 경로 찾기 완료!\n")
    }
}

// Concrete Strategy
class WalkRoute: Strategy {
    func algorithmExecute() {
        print("도보 경로 찾기 완료!\n")
    }
}

// Concrete Strategy
class BikeRoute: Strategy {
    func algorithmExecute() {
        print("자전거 경로 찾기 완료!\n")
    }
}
```

그런 뒤 만든 알고리즘들을 교체해가며 사용할 Context를 구현합니다.

```
// Context
class Navigation {
    private var routeAlgorithm: Strategy?
    
    func execute() {
        self.routeAlgorithm?.algorithmExecute()
    }
    
    func setStrategy(strategy: Strategy) {
        self.routeAlgorithm = strategy
    }
}
```

Strategy 객체를 참조하고 있는 Context 클래스를 만들었다면 끝입니다.

실제로 사용을 해보면, 다음과 같습니다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FClOpR%2Fbtq8wmVKNlT%2FZwpKZHayXtFqKOzUgAmuIk%2Fimg.png" width="50%">

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbajEwH%2Fbtq8ujlFIEt%2FeICBC5WiORWHAnJtyOaQZ1%2Fimg.png" width="250">

위의 결과를 보면 계속해서 Strategy 객체를 변경하며 다른 알고리즘을 사용하는 것을 볼 수 있습니다.