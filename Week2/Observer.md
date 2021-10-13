# **옵저버 패턴**

<img width="600" alt="스크린샷 2021-10-14 오전 12 40 08" src="https://user-images.githubusercontent.com/55231029/137167118-09db24ff-6f6f-44dd-8737-a278c7f11f51.png">

유튜브 구독 매커니즘으로 비유하자면 **, 주제(유튜브 채널) + 옵저버(구독자)** 

## 용어

### Subject

구독자(ConcreteObserver) 가 이벤트를 받을 주요 주제(Subject)
해당 Subject의 특정 이벤트 변경 시 구독하고 있는 구독자들이 해당 이벤트를 수신한다.

### Observer

구독자들의 부모가 되는 인터페이스 (java 에서는 추상 클래스)

### ConcreteObserver

Observer 인터페이스를 상속받고, Subject에 등록이 될 객체.
Subject에 등록(구독) 이 되면 이벤트를 받게된다.

---

### 옵저버 패턴의 정의

옵저버 패턴은 **한 Obejct의 상태가 바뀌면 그 객체에 의존(구독) 하는 다른 객체들한테 연락이 가고** 자동으로 내용이 갱신되는 방식으로 **1:N (일대다)** 관계를 정의합니다.

- 관찰 중인 객체에서 발생하는 이벤트를 여러 다른 객체에 알리는 매커니즘
(유튜브에서 구독자에게 알림 메세지 보내는 느낌)

## **느슨한 결합**

느슨한 결합이란 두 객체가 상호작용을 하지만, 서로에 대해 잘 모른다는 점을 의미합니다. 

인터페이스를 이용하여 객체간의 느슨한 결합(Loose Coupling)가능.
즉 상속을 통한 구현이 아닌 구성(Composition)을 이용한다!
**~~(스트래티지 패턴에서 배울 수 이따@!)~~**

### 이게 뭔말이냐@

<img width="619" alt="스크린샷 2021-10-14 오전 12 41 00" src="https://user-images.githubusercontent.com/55231029/137167283-2d5d9b11-de8a-4603-9498-79e23c28e444.png">

Dog, Duck, Cat, Mouse Object 와 같이 전혀 관련이 없는 객체들을 observer 라는 인터페이스로 묶음으로서 
주제(Object) 는 Observer들의 정보를 구체적으로 알 필요없이 정보 전달을 할 수 있고, 
Dog, Duck, Cat, Mouse Object 와 같은 Observer 객체들은 주제(Object)의 정보를 알 필요 없이 구독을 할 수 있다. 
**(객체지향의 다형성을 생각하면 편함!)**

### 결론

옵저버 패턴에서는 주제(subject or publisher)와 옵저버(observer)가 느슨하게 결합되어 있는 객체 디자인을 제공한다.

---

## **About 옵저버 패턴 👨🏻‍💻**

- 관찰 중인 객체에서 발생하는 이벤트를 여러 다른 객체에 알리는 메커니즘을 정의할 수 있는 디자인 패턴
- 다른 객체의 상태가 변경될 때마다 어떤 이벤트를 실행하고 싶을 때 주로 사용함
- 주로 **MVC패턴**사용함
    - ViewController → **Observer(Subscriber)**
    - Model → **Subject(Publisher)**
- Model은 View Controller의 타입에 대해 알 필요 없이 상태가 변경될 때마다 이를 View Controller에 전달함
- 여러 개의 View Controller가 하나의 Model의 변경사항을 사용할 수 있게 됨

---

### 옵저버 패턴의 장/단점 ⭐

- 변경 사항이 생겨도 무난히 처리할 수 있는 유연한 객체지향 시스템을 구축할 수 있다. 
이는 객체 사이의 상호의존성을 최소화할 수 있기 때문! (느슨하게 결합되어 있기 때문!)
- Open / Close 원칙을 지킬 수 있음 
**(확장에는 열려있고, 변경에는 닫혀있어야 한다.)**

단점

- Observer에게 알림이 가는 순서 보장 x
- Observer, Subject의 관계가 잘 정의되지 않으면 원하지 않는 동작이 발생 가능

### 디자인 패턴들은

→ 서로 상호작용을 하는 객체 사이에서는 가능하면 느슨하게 결합되는  디자인을 사용해야한다.

---

# 그림으로 볼까!

### 1. Duck이 Subject(주제) 에 구독 신청!
<img width="298" alt="스크린샷 2021-10-14 오전 12 41 21" src="https://user-images.githubusercontent.com/55231029/137167337-453cb10a-3870-441c-8f19-fec6cd0100de.png">


### 2.  Duck이 구독자 목록(observers)에 추가 됨
<img width="299" alt="스크린샷 2021-10-14 오전 12 41 35" src="https://user-images.githubusercontent.com/55231029/137167386-18f190ba-395c-4158-95f2-2ba03bcb58ad.png">



### 3. Subject에서 특정 이벤트가 발생해서 값이 변경 → 구독자들에게 알림
<img width="289" alt="스크린샷 2021-10-14 오전 12 42 06" src="https://user-images.githubusercontent.com/55231029/137167461-1f53f1cd-4ce6-42dc-b3f2-93690e8e4df2.png">


### 4. 구독 해제도 가능! (Mouse가 구독자 목록에서 탈퇴하고 싶어함)
<img width="301" alt="스크린샷 2021-10-14 오전 12 42 17" src="https://user-images.githubusercontent.com/55231029/137167493-543ef75d-7231-475f-bbf9-fb7bb9194c07.png">


### 5. Mouse 구독 해제!
<img width="308" alt="스크린샷 2021-10-14 오전 12 42 35" src="https://user-images.githubusercontent.com/55231029/137167540-00442e99-f242-42d4-b22e-550206aef109.png">


### 6. 또 다른 이벤트 발생! → 구독자 목록에서 빠진 Mouse 를 제외한 모든 구독자에게 이벤트 전달
<img width="301" alt="스크린샷 2021-10-14 오전 12 42 44" src="https://user-images.githubusercontent.com/55231029/137167558-178fa53d-ef06-4b9c-8264-0a07afc409d1.png">

---

# 코드로 보자!

### Subject
```swift
// 주체 프로토콜 (인터페이스 느낌)
protocol Subject {
    var observers: [Observer] { get set }
    func subscribe(observer: Observer)
    func unSubscribe(observer: Observer)
    func notify(message: String)
}
// 애플 스토어
class AppleStore: Subject {
    var observers: [Observer]
    
    init(observers: [Observer]){
        self.observers = observers
    }
    func subscribe(observer: Observer) {
        self.observers.append(observer)
    }
    
    func unSubscribe(observer: Observer) {
        if let index = self.observers.firstIndex(where: { $0.id == observer.id }) {
            self.observers.remove(at: index)
        }
    }
    
    func notify(message: String) {
        for observer in observers {
            observer.update(message: message)
        }
    }
}
```

### Observer

```swift
// 옵저버 프로토콜
protocol Observer {
    var id: String { get set }
    func update(message: String)
}
// 고객
class Customer: Observer {
    var id: String
    
    init(id: String){
        self.id = id
    }
    
    func update(message: String){
        print("\(id), -> \(message) 수신")
    }
}
```

### 오또케쓰누

```swift
func test(){
    let appleStore = AppleStore(observers: [])
    
    let mumu = Customer(id: "mumu")
    let nunu = Customer(id: "nunu")
    let ayos = Customer(id: "Ayos")
    
		// 애플 스토어에 고객이 구독!
    appleStore.subscribe(observer: mumu)
    appleStore.subscribe(observer: nunu)
    appleStore.subscribe(observer: ayos)
    
		// 애플 스토어에서 알림이 왔네!
    appleStore.notify(message: "첫번째 알림~~ ")
    
		// 누누가 구독 취소
    appleStore.unSubscribe(observer: nunu)
    
		// 두번째 알림 구독자한테 감
    appleStore.notify(message: "두번째 알림~~ ")
}

test()
```

# 결과는?

<img width="430" alt="스크린샷 2021-10-14 오전 12 48 21" src="https://user-images.githubusercontent.com/55231029/137168586-0029ce95-f79f-4794-836c-39f4b82e5a49.png">




### 실습 예제: https://github.com/leesoongin/Design-Patterns/blob/main/Observer/Observer%20example.md
