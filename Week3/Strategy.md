# ๐Strategy Pattern

Strategy Pattern์ ํด๋์ค์ ํ์๋ฅผ **์บก์ํ** ํ์ฌ **๋์ **์ผ๋ก ํ์๋ฅผ ์์ ๋กญ๊ฒ ๋ฐ๊ฟ ์ ์๋๋ก ๋๋ ํจํด์๋๋ค.

<br>

Strategy Pattern์ ๊ตฌ์ฑ์์๋ 3๊ฐ์ง๋ก ๋๋ฉ๋๋ค.

<img src="https://t1.daumcdn.net/cfile/tistory/9997303C5E0DC6830E">

###### ***<Strategy pattern์ ๋ค์ด์ด๊ทธ๋จ>***

>1. Strategy๋ฅผ ์ฌ์ฉํ  ๊ฐ์ฒด
>2. Strategy๋ฅผ ์ ์ํ๋ ํ๋กํ ์ฝ
>3. 2๋ฒ์ ํ๋กํ ์ฝ์ ๊ตฌํํ Strategy๊ฐ์ฒด

๋ ๊ฐ ์ด์์ ์ ์ฌํ ๋์์ด ํ์ํ๊ณ , ์ด ๋์์ด ์ ์ฐํ๊ฒ ๋ฐ๋๊ธฐ๋ฅผ ์ํ  ๋ ์ฌ์ฉํ๋ฉด ์ข์ต๋๋ค.

<br><br><br>

**Delegateํจํด๊ณผ ๊ต์ฅํ ์ ์ฌํ๋ค. (๊ตฌ์ฑ์์๋ง๋ด๋ ๋๊ฐ์)**

<img src="https://t1.daumcdn.net/cfile/tistory/9997353A5E0DC6972C">

###### ***<Delegate pattern์ ๋ค์ด์ด๊ทธ๋จ>***

<br>

## ์ฅ/๋จ์  โญ

### ์ฅ์ 

- **๋ฐํ์** ์์ ๊ฐ์ฒด ๋ด๋ถ์์ ์ฌ์ฉ๋๋ ์๊ณ ๋ฆฌ์ฆ์ ๋ณ๊ฒฝ ํ  ์ ์์ต๋๋ค.
- ์๊ณ ๋ฆฌ์ฆ์ ์ฌ์ฉํ๋ ์ฝ๋์ ์๊ณ ๋ฆฌ์ฆ์ ๊ตฌํํ๋ ์ฝ๋๋ฅผ ๋ถ๋ฆฌํ  ์ ์์ต๋๋ค.
- **Open / Closed Principle(๊ฐ๋ฐฉ ํ์ ์์น)์ ์ค์**ํฉ๋๋ค. **Context(SuperClass)๋ฅผ ๋ณ๊ฒฝํ์ง ์๊ณ ๋** ์๋ก์ด Strategy๋ฅผ ๋์ํ  ์ ์์ต๋๋ค.

### ๋จ์ 

- ์๊ณ ๋ฆฌ์ฆ์ด ๋ช ๊ฐ ์๊ณ  ๋ณ๊ฒฝ๋๋ ์ผ๋ ๊ฑฐ์ ์๋ ๊ฒฝ์ฐ ์ ๋ต ํจํด์ ๋์์ด ์คํ๋ ค ๋ณต์ก์ฑ์ ์ฆ๊ฐ์ํฌ ์ ์์ต๋๋ค.
- ํด๋ผ์ด์ธํธ๊ฐ ์ ์ ํ Strategy๋ฅผ ์ ํํ๊ธฐ ์ํด์๋ ๊ฐ๊ฐ์ ์ฐจ์ด์ ์ ์๊ณ  ์์ด์ผ ํฉ๋๋ค.
**(๊ฐ๊ฐ์ ์๊ณ ๋ฆฌ์ฆ๊ตฐ ํน์ฑ์ ์ ์์์ผํจ)**
- Strategy, Context๊ฐ ํต์  ์ค๋ฒํค๋๊ฐ ๋ฐ์ํฉ๋๋ค.
**(๊ฐ์ ํ๋๊ตฐ ์์์ ๋ค๋ฅธ ํ๋์ ํ๊ธฐ์ํด์  ํ๋ ํด๋์ค๋ฅผ ๋ณ๊ฒฝํด์ค์ผํจ. ์ด ๋ณ๊ฒฝ ๊ณผ์ ์ด ์ค๋ฒํค๋)**

<br>

<hr>

<br>

### ๐์ฌ์ฉ ์์

๋จผ์  Strategy ์ธํฐํ์ด์ค ์ญํ ์ ํ  ํ๋กํ ์ฝ์ ํ๋ ์ ์ํด์ค๋๋ค.
(ํ๋๊ตฐ)

```swift
// ํ๋๊ตฐ ์ ์งํฉํ!
protocol FindRouteBehavior { 
    // ๊ธธ์ฐพ๊ธฐ (์๋์ฐจ, ๋๋ณด, ์์ ๊ฑฐ)
    func findRoute() 
}

protocol SearchBehavior {
    // ๊ฒ์. (๋๋ก๋ช, ์ง๋ฒ)
    func search() 
}
```

์ด๋ฒ์๋ Strategy ํ๋กํ ์ฝ์ ์ฑํํ๋ ์๊ณ ๋ฆฌ์ฆ๋ค์ ๋ง๋ค์ด์ฃผ๋ฉด ๋ฉ๋๋ค.<br>
๋ค๋น๊ฒ์ด์์ผ๋ก ์๋์ฐจ, ๋๋ณด, ์์ ๊ฑฐ ๊ฒฝ๋ก๋ฅผ ์ฐพ๋ Strategy ํ๋กํ ์ฝ์ ์ฑํํ 3๊ฐ์ ํด๋์ค๋ฅผ ๋ง๋ค์ด์ค๋๋ค.

```swift
// Concrete Strategy
class CarRoute: FindRouteBehavior {
    func findRoute() {
        print("์๋์ฐจ ๊ฒฝ๋ก ์ฐพ๊ธฐ ์๋ฃ!")
    }
}

// Concrete Strategy
class WalkRoute: FindRouteBehavior {
    func findRoute() {
        print("๋๋ณด ๊ฒฝ๋ก ์ฐพ๊ธฐ ์๋ฃ!")
    }
}

// Concrete Strategy
class BikeRoute: FindRouteBehavior {
    func findRoute() {
        print("์์ ๊ฑฐ ๊ฒฝ๋ก ์ฐพ๊ธฐ ์๋ฃ!")
    }
}

class LoadName: SearchBehavior {
    func search() {
        print("๋๋ก๋ช์ผ๋ก ์ฃผ์ ๊ฒ์!\n")
    }
}

class NumberName: SearchBehavior {
    func search() {
        print("์ง๋ฒ์ผ๋ก ์ฃผ์ ๊ฒ์!\n")
    }
}
```

๊ทธ๋ฐ ๋ค ๋ง๋  ์๊ณ ๋ฆฌ์ฆ๋ค์ ๊ต์ฒดํด๊ฐ๋ฉฐ ์ฌ์ฉํ  Context๋ฅผ ๊ตฌํํฉ๋๋ค.

```swift
// Context
class Navigation {
    private var routeBehavior: FindRouteBehavior? // ๊ธธ์ฐพ๊ธฐ (์๋์ฐจ, ์์ ๊ฑฐ, ๋๋ณด) ํ๋๊ตฐ/์๊ณ ๋ฆฌ์ฆ ๊ตฐ
    private var searchBehavior: SearchBehavior? // ์ฃผ์ ๊ฒ์ (๋๋ก๋ช, ์ง๋ฒ) ํ๋๊ตฐ/์๊ณ ๋ฆฌ์ฆ ๊ตฐ
    
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

**์คํ ๋ถ๋ถ**

```swift
func main(){
    let navigation: Navigation = Navigation()
    
        // ์ด๊ธฐ ์ธํ
    navigation.setRouteBehavior(behavior: CarRoute())
    navigation.setSearchBehavior(behavior: LoadName())
    
    navigation.findRoute()
    navigation.searchAddress()
    
        // ์๊ตฌ์ฌํญ์ ๋ณํ๊ฐ ์๊ฒผ์ ๊ฒฝ์ฐ, ๋ค๋ฅธ ํ๋ ํจํด์ ๋์
    navigation.setRouteBehavior(behavior: BikeRoute())
    navigation.setSearchBehavior(behavior: NumberName())
    
    navigation.findRoute()
    navigation.searchAddress()
}
```


Strategy ๊ฐ์ฒด๋ฅผ ์ฐธ์กฐํ๊ณ  ์๋ Context ํด๋์ค๋ฅผ ๋ง๋ค์๋ค๋ฉด ๋์๋๋ค.

์ค์ ๋ก ์ฌ์ฉ์ ํด๋ณด๋ฉด, ๋ค์๊ณผ ๊ฐ์ต๋๋ค.

<img width="536" alt="แแณแแณแแตแซแแฃแบ 2021-10-22 แแฉแแฎ 6 26 03" src="https://user-images.githubusercontent.com/55231029/138430059-5b9d5da6-9a6d-401f-9f00-23d507a8af16.png">


<!-- <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FClOpR%2Fbtq8wmVKNlT%2FZwpKZHayXtFqKOzUgAmuIk%2Fimg.png" width="50%">

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbajEwH%2Fbtq8ujlFIEt%2FeICBC5WiORWHAnJtyOaQZ1%2Fimg.png" width="250"> -->

์์ ๊ฒฐ๊ณผ๋ฅผ ๋ณด๋ฉด ๊ณ์ํด์ Strategy ๊ฐ์ฒด๋ฅผ ๋ณ๊ฒฝํ๋ฉฐ ๋ค๋ฅธ ์๊ณ ๋ฆฌ์ฆ์ ์ฌ์ฉํ๋ ๊ฒ์ ๋ณผ ์ ์์ต๋๋ค.

<br>
<br>
<br>

---

# ๋ถ๋ก

## ๋์์ธ ์์น

### **์ ํ๋ฆฌ์ผ์ด์์์ ๋ฌ๋ผ์ง๋ ๋ถ๋ถ์ ์ฐพ์๋ด๊ณ , ๋ฌ๋ผ์ง์ง ์๋ ๋ถ๋ถ์ผ๋ก๋ถํฐ ๋ถ๋ฆฌ์ํจ๋ค.**

- ๋ฐ๋๋ ๋ถ๋ถ์ ๋ฐ๋ก ๋ฝ์์ ์บก์ํ. 
๋ฐ๋์ง ์๋ ๋ถ๋ถ์๋ ์ํฅ์ ๋ฏธ์น์ง ์์ ์ฑ๋ก ๋ฐ๋๋ ๋ถ๋ถ๋ง ์ ์ง ๋ณด์ํ๊ธฐ ์ฉ์ดํ๋ค.

### ๊ตฌํ์ด ์๋ ์ธํฐํ์ด์ค์ ๋ง์ถฐ์ ํ๋ก๊ทธ๋๋ฐ ํ๋ค.

- '์ธํฐํ์ด์ค์ ๋ง์ถฐ์ ํ๋ก๊ทธ๋๋ฐ ํ๋ค.' ๋ผ๋ ๋ง์ ์ฆ, "์์ ํ์์ ๋ง์ถฐ ํ๋ก๊ทธ๋๋ฐ ํ๋ค." ๋ผ๋ ๋ง๊ณผ ๋์ผํ๋ค.
- ๋คํ์ฑ์ ์ด์ฉํด ์์ ์ถ์ ํด๋์ค๋ ์ธํฐํ์ด์ค์ ๊ฐ์ **์์ ํ์** ์ผ๋ก ์ ์ธ ํ  
์คํ์์ ๊ตฌ์ฒด์ ์ผ๋ก ๊ตฌํ๋ ๊ฐ์ฒด๋ฅผ ๋์ํด์ฃผ๋ฉด ๋๋ค.

### ์์๋ณด๋ค๋ ๊ตฌ์ฑ์ ํ์ฉํ๋ค.

- ์๋ฅผ ๋ค์ด Duck์ด๋ผ๋ ์ํผ ํด๋์ค,  ๊ทธ์ ์๋ธ ํด๋์ค๋ค์์ ํ๋์ ์ง์  ๊ตฌํํ๊ธฐ๋ณด๋จ
ํน์  ์ญํ ๊ตฐ(ํด๋์ค) ์ ๋ฌถ์ด ์ญํ ๊ตฐ ๋ง๋ค ์ธํฐํ์ด์ค๋ฅผ ์์, ์ญํ ๊ตฐ(ํด๋์ค) ์์ ๊ตฌ์ฒด์ ์ธ ํ๋์ ๊ตฌํ
- "A(Duck) ์๋ B(Behavior) ๊ฐ ์๋ค." ๊ด๊ณ๋ฅผ ๊ตฌ์ฑ์ด๋ผ ํํ.
ํ๋ ํด๋์ค๋ฅผ ์์๋ฐ๋ ๋์  ๋ณ์(ํ๋กํผํฐ)๋ฅผ ์ฌ์ฉํจ์ผ๋ก์ ํ๋์ ๋ถ์ฌ๋ฐ๋๋ค.

```swift
class Duck {
	var flyBehavior: FlyBehavior
	var quackBehavior: QuackBehavior

	func ....
}
```


