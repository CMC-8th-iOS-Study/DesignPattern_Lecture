# ‣  커맨드 패턴 ( Command Pattern) 💻

![IMG_0301](https://user-images.githubusercontent.com/88825022/138418506-2be25817-be24-4413-ac94-18966f1eba7d.PNG)
</br>
저장이나 복사/붙여넣기 같은 일부 기능은 여러 위치에서 호출되기 때문에 한 기능이 여러 클래스에 구현되는 문제가 발생한다.

</br>

![IMG_0302](https://user-images.githubusercontent.com/88825022/138419064-61ec4804-abe8-4086-a2b3-a9950da83ff8.PNG)
</br>
커맨드 패턴은 UI 객체가 요청을 직접 보내지 않고, 호출되는 객체나 메서드 및 파라미터 같은 모든 세부 사항을 담는 새로운 커맨드 클래스를 추출한다.

</br></br><hr/>
> UML 도식화 ▾
<img width="930" alt="Command-UML" src="https://user-images.githubusercontent.com/64394744/138112372-b5d5242f-b67a-4274-8659-1d3cd113bc13.png">
<hr/>

* **Command**
    * 실행될 기능에 대한 인터페이스를 선언하는 객체
    * Command를 실행하기 위한 하나의 메서드로 이루어진 경우가 많다.
    
* **Concreate Command** 
    * 실제로 실행되는 인터페이스를 구현하는 객체
    * Receiver 객체와 작업 사이 **바인딩**을 정의한다.
    * Receiver에서 해당 작업을 호출하여 실행한다.
    * 직접 작업을 수행하는 것이 아닌 **Recevier에게 전달하기 위한 목적**을 갖고 있다.
    * 코드를 **단순화**하기 위해 클래스를 합칠 수도 있다.

* **Client**
    * Concreate Command 객체를 만들고 Receiver를 설정한다.
    * Receiver의 **인스턴스**를 포함한 작업에 필요한 모든 매개변수를 Command의 **생성자**에 전달하여 작업을 처리한다.

* **Invoker**
    * 기능의 실행을 요청하는 호출자 클래스 객체
    * Invoker 클래스에는 **명령 객체**에 대한 참조를 저장하기 위한 **필드**가 있어야 한다.
    * Client가 생성자를 통해 Invoker 객체를 만들 때 Command 객체를 받게 된다.
    * 요청을 Receiver에게 직접 보내는 것이 아닌 해당 **요청의 시작**을 담당한다.
    
* **Receiver**
    * Concreate Command 객체에서 실행할 메서드를 구현할 때 필요한 클래스 객체
    * Concreate Command 객체의 기능을 실행하기 위해서 사용하는 수신자 클래스 객체
<hr/> </br>

## ‣  About **"Command Pattern"**  📖
* **실행될 기능을 캡슐화**함으로써 주어진 여러 기능을 실행할 수 있는 **재사용성이 높은 클래스**를 설계하는 행위패턴이다.

    * Why **Encapsulation(캡슐화)** ?
    
        * 기능의 실행을 요구하는 **호출자(Invoker)** 클래스와 실제 기능을 실행하는 **수신자(Receiver)** 클래스 사이의 **의존성을 제거**한다.
        
        * 따라서 실행될 기능의 변경에도 호출자 클래스를 수정 없이 그대로 사용할 수 있도록 해준다.
        
- 이벤트가 발생했을 때 **실행될 기능이 다양하면서도 변경이 필요한 경우에 이벤트를 발생시키는 클래스를 변경하지 않고 재사용**하고자 할 때 유용하다.

</br>
    
## ‣  Command Pattern 장/단점  ⭐️
* 장점 
    * Single Responsibility (단일 책임 원칙)을 만족한다. Command 객체를 통해 **작업을 수행하는 객체**와 **작업을 호출하는 객체**를 나눌 수 있다.
    
    * Open / Closed Principle (개방 / 폐쇄 원칙)을 만족한다. 클라이언트의 코드를 수정하지 않고도 새로운 Command를 추가할 수 있다.
    
    * 실행 취소, 다시 실행을 구현할 수 있다.
    
    * 작업의 시작을 지연시킬 수 있다.
    
    * 여러 개의 단순한 명령을 조합해서 복잡한 명령을 만들 수 있다.
    
* 단점
    * Receiver, Invoker 사이에 관계를 도입해야 하므로 **코드가 복잡**해질 수 있다.
</br>    

# ‣ 예제 코드 (1)

- 복사 & 붙여넣기 예제 구현 + 실행 취소, 다시 실행 구현
</br>

![IMG_34928759A490-1](https://user-images.githubusercontent.com/88825022/138416159-60eae1a9-e522-4f93-a3b5-52cad952f7cd.jpeg)


### **Command**
```swift
// Command
protocol Command {
    var receiver: TextEditor { get set }
    var bakup: String { get set }
    
    func execute()
    func undo()
}
```
- Command 프로토콜 정의
</br>

### **Invoker**

```swift
// Invoker
class Invoker {
    var history: [Command] = []
    
    private func push(command: Command) {
        self.history.append(command)
    }
    
    private func pop() -> Command? {
        return history.popLast()
    }
    
    func executeCommand(command: Command) {
        command.execute()
        self.push(command: command)
    }
    
    func undoCommand() {
        let command = self.pop()
        if command == nil {
            print("되돌릴 작업이 존재하지 않습니다.")
        } else {
            command?.undo()
        }
    }
}
```
- Invoker는 Command를 수행하고, 되돌리는 걸 시작하는 역할만 한다.
- 실행 취소를 구현하기 위해 실행된 Command들을 순서대로 저장할 Stack을 하나 만들어준다. → histroy 객체
</br>

### **Receiver**

```swift
// Receiver
class TextEditor {
    var text: String = ""
    var clipboard: String = ""
}
```
- Receiver는 Command가 실제로 수행되는 곳이다.
</br>

## **Concreate Command**


### **Copy Function**
```swift
// Concreate Command
class CopyCommand: Command {
    var receiver: TextEditor
    var backup: String = ""
    
    init(receiver: TextEditor) {
        self.receiver = receiver
    }
    
    func undo() {
        receiver.clipboard = self.backup
        self.backup = ""
    }
    
    func execute() {
        self.backup = receiver.clipboard
        receiver.clipboard = receiver.text
    }
}
```
</br>

### **Paste Function**
```swift
// Concreate Command
class PasteCommand: Command {
    var receiver: TextEditor
    var backup: String
    
    init(receiver: TextEditor) {
        self.receiver = receiver
        self.backup = self.receiver.clipboard
    }
    
    func undo() {
        let startIdx = receiver.text.startIndex
        let lastIdx = receiver.text.inex(startIdx, offsetBy: receiver.text.count - backup.count)
        receiver.text = String(receiver.text[startIdx..<lastIdex])
    }
    
    func execute() {
        self.receiver.text += backup
    }
}
```
</br>


### **Write Function**
```swift
// Concreate Command
class WriteCommand: Command {
    var receiver: TextEditor
    var backup: String
    
    init(receiver: TextEditor, backup: String) {
        self.receiver = receiver
        self.backup = backup
    }
    
    func undo() {
        let startIdx = receiver.text.startIndex
        let lastIdx = receiver.text.inex(startIdx, offsetBy: receiver.text.count - backup.count)
        receiver.text = String(receiver.text[startIdx..<lastIdex])
    }
    
    func execute() {
        receiver.text += backup
    }
}
```
</br>


### **Output**
<img width="800" alt="Output" src="https://user-images.githubusercontent.com/64394744/138123844-1c345bdf-2891-4900-887e-cfd6a89c52d0.png">

- Command가 실행되면 receiver에서 실제로 실행되고, Invoker에서 undo를 하면 가장 최근에 한 작업이 취소가 되는 것을 볼 수 있다.
</br>

# ‣ 예제코드 (2)
+ 램프 & 알람 켜기/끄기

### 커맨드 프로토콜
```swift
protocol Command {
    func execute()
}
```
</br>

### 버튼 클래스
```swift
class Button {

    private var command: Command
    
    init(command: Command) {
        self.command = command
    }
    
    func setCommand(command: Command) {
        self.command = command
    }
    
    func pressed() {
        self.command.execute()
    }
    
}
```
</br>

### 램프 클래스 & 램프 커맨드 클래스
```swift
class Lamp {
    func turnOn() {
        print("Lamp On")
    }
}

class LampOnCommand: Command {
    
    private var lamp: Lamp
    
    init(lamp: Lamp) {
        self.lamp = lamp
    }
    
    func execute() {
        self.lamp.turnOn()
    }
    
}
```
</br>

### 알람 클래스 & 알람 커맨드 클래스
```swift
class Alarm {
    func start() {
        print("Alarm Start")
    }
}

class AlarmStartCommand: Command {
    
    private var alarm: Alarm
    
    init(alarm: Alarm) {
        self.alarm = alarm
    }
    
    func execute() {
        self.alarm.start()
    }
    
}
```
</br>

### 클라이언트
```swift
let lamp = Lamp()
let lampOnCommand = LampOnCommand(lamp: lamp)

let alarm = Alarm()
let alarmStartCommand = AlarmStartCommand(alarm: alarm)

// 램프를 켜는 버튼
let button1 = Button(command: lampOnCommand)
button1.pressed()           // Lamp On

// 한 번 누르면 알람이 켜지고, 두 번 누르면 램프가 켜지는 버튼
let button2 = Button(command: alarmStartCommand)
button2.pressed()           // Alarm Start
button2.setCommand(command: lampOnCommand)
button2.pressed()           // Lamp On
```
</br>

