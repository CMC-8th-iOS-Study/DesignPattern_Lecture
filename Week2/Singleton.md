# ๐Singleton

ํน์  ์ฉ๋๋ก ๊ฐ์ฒด๋ฅผ **"ํ๋๋ง"** ์์ฑํ์ฌ **"๊ณต์ฉ"** ์ผ๋ก ์ฌ์ฉํ๊ณ  ์ถ์ ๋ Singleton ๋์์ธ ํจํด์ ํ์ฉํ๋ค.<br>
Singleton์ผ๋ก ๊ตฌํ๋ ํด๋์ค๋ ์์ฑ์๊ฐ ์ฌ๋ฌ ์ฐจ๋ก ํธ์ถ๋๋๋ผ๋ ์ค์ ๋ก ์์ฑ๋๋ ๊ฐ์ฒด๋ ํ๋์ด๋ฉฐ, ์ต์ด ์์ฑ ์ดํ์ ํธ์ถ๋ ์์ฑ์๋ ์ต์ด์ ์์ฑ์๊ฐ ์์ฑํ ๊ฐ์ฒด๋ฅผ ๋ฆฌํดํ๋ค.

์ฆ, ๊ฐ์ฒด๋ฅผ ํ๋๋ง ์์ฑํ์ฌ, ์์ฑ๋ ๊ฐ์ฒด๋ฅผ ์ด๋์๋  ์ฐธ์กฐํ  ์ ์๋๋ก ํ๋ ํจํด์ด๋ค.

<br>

```
class UserInfo {
    var id: String?
    var password: String?
    var name: String?
}

// A๋ทฐ์ปจ
let userInfo = Userinfo()
userInfo.id = "Sodeul"

// B๋ทฐ์ปจ
let userInfo = Userinfo()
userInfo.password = "1234"

// C๋ทฐ์ปจ
let userInfo = Userinfo()
userInfo.name = "Sodeul"
```

๋ง์ฝ ์์ ๊ฐ์ด ๊ฐ ๋ทฐ์ปจ์์ ๋ฐ๋ก ๋ฐ๋ก ์ ๋ณด๋ฅผ ๋ฐ๊ฒ ๋๋ฉด, ๊ฐ๊ฐ์ ์ธ์คํด์ค์์ ์ ๋ณด๊ฐ ๋ฐ๋ก ๋๊ฒ ๋๋ค.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/b7DLbv/btqOYtTGZ4t/2HuCG2pgmg1TcJMkxhIne1/img.png" width="70%">

๋ฐ๋ผ์ ์ด๋ฅผ ํด๊ฒฐ ํ๊ธฐ ์ํด, ํด๋น ์ธ์คํด์ค๋ ์ต์ด ์์ฑ๋  ๋ **์ ์ญ์ผ๋ก ์ ์ฅ**ํด๋๊ณ , ๊ทธ ์ดํ์๋ ์ด ์ ์ญ ์ธ์คํด์ค์๋ง ์ ๊ทผํ๊ฒ ํ๋ ๋ฐฉ๋ฒ์ ์ฌ์ฉํ๊ฒ ๋๋ค.

```
class UserInfo {
    static let shared = UserInfo()

    var id: String?
    var password: String?
    var name: String?
    
    private init() { }
    //ํน์๋ผ๋ init ํจ์๋ฅผ ํธ์ถํด Instance๋ฅผ ๋ ์์ํ๋ ๊ฒ์ ๋ง๊ธฐ ์ํด, init() ํจ์ ์ ๊ทผ ์ ์ด์๋ฅผ private๋ก ์ง์ ํด์ฃผ๋ฉด ๋๋ค.
}

// A๋ทฐ์ปจ
let userInfo = UserInfo.shared
userInfo.id = "CMC"

// B๋ทฐ์ปจ
let userInfo = UserInfo.shared
userInfo.password = "1234"

// C๋ทฐ์ปจ
let userInfo = UserInfo.shared
userInfo.name = "MakeUs Challenger"
```
#### ๐ก์ด๋ ํด๋์ค์์๋  shared๋ผ๋ static ํ๋กํผํฐ๋ก ์ ๊ทผํ๋ฉด, ํ๋์ Instance๋ฅผ ๊ณต์ ํ  ์ ์๋ค.<br>

์์ ์์์์ UserInfo ํด๋์ค๊ฐ **์ฑ๊ธํด ๊ฐ์ฒด**๋ผ๊ณ  ๋ถ๋ฅด๋ฉฐ, ์์ ๊ฐ์ ๋ฐฉ์์ **์ฑ๊ธํด ํจํด**์ด๋ผ๊ณ  ๋ถ๋ฅธ๋ค.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/VmsQc/btqOYt0xgaU/k4fR7SVzSexrukeToKNAKk/img.png" width="70%">

ํด๋์ค์ ๋ํ Instance๋ ์ต์ด ์์ฑ๋  ๋ ๋ฑ ํ๋ฒ๋ง ์์ฑํด์ ์ ์ญ์ ๋๊ณ , ๊ทธ ์ดํ๋ก๋ ์ด Instance๋ง ์ ๊ทผ ๊ฐ๋ฅํ๊ฒ ํ๋ค.

<br>

### ๐๋ง์ ๊ณณ์ ์ฌ์ฉ๋๋ Singleton Pattern

```
let screen = UIScreen.main
let userDefault = UserDefaults.standard
let application = UIApplication.shared
let fileManager = FileManager.default
let notification = NotificationCenter.default
```

### ๐Singleton Pattern์ ์ฅ๋จ์ 

**์ฅ์ **
- ํ ๋ฒ์ Instance๋ง ์์ฑํ๋ฏ๋ก ๋ฉ๋ชจ๋ฆฌ ๋ญ๋น๋ฅผ ๋ฐฉ์งํ  ์ ์๋ค.<br>
- Singleton Instance๋ ์ ์ญ Instance๋ก ๋ค๋ฅธ ํด๋์ค๋ค๊ณผ์ ์์ ๊ณต์ ๊ฐ ์ฝ๊ณ  ์ ๊ทผ์ด ์ฝ๋ค.<br>
- DBCP(DataBase Connection Pool)์ฒ๋ผ ๊ณตํต๋ ๊ฐ์ฒด๋ฅผ ์ฌ๋ฌ๊ฐ ์์ฑํด์ ์ฌ์ฉํด์ผํ๋ ์ํฉ์์ ๋ง์ด ์ฌ์ฉ (์ฐ๋ ๋ํ, ์บ์, ๋ํ์์, ์ฌ์ฉ์ ์ค์ , ๋ ์ง์คํธ๋ฆฌ ์ค์ , ๋ก๊ทธ ๊ธฐ๋ก ๊ฐ์ฒด ๋ฑ)<br>

**๋จ์ **
- Singleton Instance๊ฐ ๋๋ฌด ๋ง์ ์ผ์ ํ๊ฑฐ๋, ๋ง์ ๋ฐ์ดํฐ๋ฅผ ๊ณต์ ์ํฌ ๊ฒฝ์ฐ ๋ค๋ฅธ ํด๋์ค์ Instance๋ค ๊ฐ ๊ฒฐํฉ๋๊ฐ ๋์์ ธ โ๊ฐ๋ฐฉ=ํ์โ ์์น์ ์๋ฐฐํ๋ค. (๊ฐ์ฒด ์งํฅ ์ค๊ณ ์์น ์ด๊ธ๋จ)<br>
- ์์ ๊ณผ ํ์คํธ๊ฐ ์ด๋ ค์์ง๋ค.

<br><br>

<details>
    <summary>์ถ๊ฐ ์ค์ต์์ </summary>

  <br>
  
1. ์ฑ๊ธํค ํจํด์ ์ด์ฉํ์ฌ ์ด๋ฆ๊ณผ ๋์ด๋ฅผ ์ธ์คํด์ค๋ก ๊ฐ์ง๊ณ  ์๋ ํด๋์ค ์์ฑ
  
 <img width="357" alt="image" src="https://user-images.githubusercontent.com/70688424/137126162-d0bb044d-92b7-4086-85cb-f149389db29e.png"><br><br>


2. ViewController์์ ์ด๋ฆ๊ณผ ๋์ด ์ ํด์ค
  
 <img width="367" alt="image" src="https://user-images.githubusercontent.com/70688424/137126175-14313ee1-9691-4bb0-a664-7ad1c6f6e54d.png"><br><br>


3. ViewController1์์ ์ด๋ฆ ์ฌ์ฉ
  
 <img width="371" alt="image" src="https://user-images.githubusercontent.com/70688424/137126184-bee40279-9651-483d-85b0-0cd19bb9f94f.png"><br><br>

  
4. ViewController2์์ ๋์ด ์ฌ์ฉ
  
 <img width="374" alt="image" src="https://user-images.githubusercontent.com/70688424/137126195-f953508c-ea92-42f7-933c-717b79cf4032.png">



</details>
