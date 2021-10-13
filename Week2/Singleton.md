# 📕Singleton

특정 용도로 객체를 **"하나만"** 생성하여 **"공용"** 으로 사용하고 싶을 때 Singleton 디자인 패턴을 활용한다.<br>
Singleton으로 구현된 클래스는 생성자가 여러 차례 호출되더라도 실제로 생성되는 객체는 하나이며, 최초 생성 이후에 호출된 생성자는 최초의 생성자가 생성한 객체를 리턴한다.

즉, 객체를 하나만 생성하여, 생성된 객체를 어디서든 참조할 수 있도록 하는 패턴이다.

<br>

```
class UserInfo {
    var id: String?
    var password: String?
    var name: String?
}

// A뷰컨
let userInfo = Userinfo()
userInfo.id = "Sodeul"

// B뷰컨
let userInfo = Userinfo()
userInfo.password = "1234"

// C뷰컨
let userInfo = Userinfo()
userInfo.name = "Sodeul"
```

만약 위와 같이 각 뷰컨에서 따로 따로 정보를 받게 되면, 각각의 인스턴스에서 정보가 따로 놀게 된다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/b7DLbv/btqOYtTGZ4t/2HuCG2pgmg1TcJMkxhIne1/img.png" width="70%">

따라서 이를 해결 하기 위해, 해당 인스턴스는 최초 생성될 때 **전역으로 저장**해두고, 그 이후에는 이 전역 인스턴스에만 접근하게 하는 방법을 사용하게 된다.

```
class UserInfo {
    static let shared = UserInfo()

    var id: String?
    var password: String?
    var name: String?
    
    private init() { }
    //혹시라도 init 함수를 호출해 Instance를 또 생생하는 것을 막기 위해, init() 함수 접근 제어자를 private로 지정해주면 된다.
}

// A뷰컨
let userInfo = UserInfo.shared
userInfo.id = "CMC"

// B뷰컨
let userInfo = UserInfo.shared
userInfo.password = "1234"

// C뷰컨
let userInfo = UserInfo.shared
userInfo.name = "MakeUs Challenger"
```
#### 💡어느 클래스에서든 shared라는 static 프로퍼티로 접근하면, 하나의 Instance를 공유할 수 있다.<br>

위의 예시에서 UserInfo 클래스가 **싱글턴 객체**라고 부르며, 위와 같은 방식을 **싱글턴 패턴**이라고 부른다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/VmsQc/btqOYt0xgaU/k4fR7SVzSexrukeToKNAKk/img.png" width="70%">

클래스에 대한 Instance는 최초 생성될 때 딱 한번만 생성해서 전역에 두고, 그 이후로는 이 Instance만 접근 가능하게 한다.

<br>

### 📌많은 곳에 사용되는 Singleton Pattern

```
let screen = UIScreen.main
let userDefault = UserDefaults.standard
let application = UIApplication.shared
let fileManager = FileManager.default
let notification = NotificationCenter.default
```

### 📌Singleton Pattern의 장단점

**장점**
- 한 번의 Instance만 생성하므로 메모리 낭비를 방지할 수 있다.<br>
- Singleton Instance는 전역 Instance로 다른 클래스들과의 자원 공유가 쉽고 접근이 쉽다.<br>
- DBCP(DataBase Connection Pool)처럼 공통된 객체를 여러개 생성해서 사용해야하는 상황에서 많이 사용 (쓰레드풀, 캐시, 대화상자, 사용자 설정, 레지스트리 설정, 로그 기록 객체 등)<br>

**단점**
- Singleton Instance가 너무 많은 일을 하거나, 많은 데이터를 공유시킬 경우 다른 클래스의 Instance들 간 결합도가 높아져 “개방=폐쇄” 원칙을 위배한다. (객체 지향 설계 원칙 어긋남)<br>
- 수정과 테스트가 어려워진다.

<br><br>

<details>
    <summary>추가 실습예제</summary>

  <br>
  
1. 싱글톤 패턴을 이용하여 이름과 나이를 인스턴스로 가지고 있는 클래스 생성
  
 <img width="357" alt="image" src="https://user-images.githubusercontent.com/70688424/137126162-d0bb044d-92b7-4086-85cb-f149389db29e.png"><br><br>


2. ViewController에서 이름과 나이 정해줌
  
 <img width="367" alt="image" src="https://user-images.githubusercontent.com/70688424/137126175-14313ee1-9691-4bb0-a664-7ad1c6f6e54d.png"><br><br>


3. ViewController1에서 이름 사용
  
 <img width="371" alt="image" src="https://user-images.githubusercontent.com/70688424/137126184-bee40279-9651-483d-85b0-0cd19bb9f94f.png"><br><br>

  
4. ViewController2에서 나이 사용
  
 <img width="374" alt="image" src="https://user-images.githubusercontent.com/70688424/137126195-f953508c-ea92-42f7-933c-717b79cf4032.png">



</details>
