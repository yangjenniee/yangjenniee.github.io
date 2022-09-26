---
layout: single

title: "1.1.1) 싱글톤" 

categories: 
    - Design pattern

tags: [singleton]

toc: true

---

<br />

<br />

# 🐣 서론

---

디자인 패턴이란 프로그램을 설계할 때 발생했던 문제점들을 객체 간의 상호 관계 등을 이용하여 해결할 수 있도록 **하나의 '규약'** 형태로 만들어 놓은 것을 의미한다. 

# 💁🏻 싱글톤 패턴

---

싱글톤 패턴은 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴이다. 보통 데이터베이스 연결 모듈에 많이 사용한다. 

인스턴스 :  클래스에 소속된 개별적 개체 ex) User 클래스의 홍길동 객체

하나의 인스턴스를 만들어 놓고 해당 인스턴스를 다른 모듈들이 공유하며 사용하기 때문에 **인스턴스를 생성할 때 드는 비용이 줄어드는 장점**이 있다. 하지만 **의존성이 높아진다**는 단점이 있다. 



---



# 🔭 자바스크립트의 싱글톤 패턴

```javascript
const obj = {
    a:27
}
const obj2 = {
    a:27
}
console.log(obj === obj2)
//false
```

const는 변수값 변경이 불가능한 자료형을 선언한 것이다

console.log로 진위여부를 판단한다. 변수가 같은지 비교하기 위해 ===를 썼다.

자바스크립트에서는 ==보다 ===를 쓰기를 권장한다. (엄격히 비교)

(가능한 ==를 사용하지 않고 자료형을 직접 변환(캐스팅)하여 코드 가독성을 높이자)

자바스크립트에서는 리터럴{} 또는 new Object로 객체를 생성하면 다른 어떤 객체와도 같지 않다. 

따라서 엄격히 비교시같지 않으므로 따라서 결과는 false  

```javascript
class Singleton {
    constructor() {
 //약속된 이름으로 바꾸면 안됨
        if(!Singleton.instance) {
            Singleton.instance = this
        }
        return Singleton.instance
    }
    getInstance(){
        return this.instance
        }
}

const a = new Singleton()
const b = new Singleton()
console.log(a===b) // true 
```

constructor()  -> 이 함수로 객체의 초기값을 설정할 수 있음  약속된 이름으로 바꾸면 안된다 

싱글톤 패턴에서는 이미 객체가 생성되었는지 판단하는 instance와 같은 내부 변수가 필요

!Singleton.instance - > 인스턴스가 없으면 새로 지정 

인스턴스가 있으면 인스턴스를 리턴해준다.

이를 통해 a와 b는 하나의 인스턴스를 가지는 Singleton을 가진다 

a에 새로운 싱글톤을 생성해주면 Singleton.instance는 인스턴스가 있으므로 그냥 바로 return this.instance를 해준다  



---



# 💛 데이터베이스 연결 모듈

 싱글톤 패턴은 데이터베이스 연결 모듈에 많이 쓰인다 

```javascript
const URL = 'mongodb://localhost:27017/kundolapp'
const createConnection = url => ({"url" : url})
class DB {
  constructor(url) {
    if (!DB.instance) {
      DB.instance = createConnection(url)
    }
    return DB.instance
  }
  connect() {
    return this.instance
  }
}
const a = new DB(URL)
const b = new DB(URL)
console.log(a===b) 
```

위에 설명과 같이 a의 경우 DB.instance가 없으므로 생성해주고, 이를 return

있을경우엔 바로 connect() 메서드로 go , return this.instance를 해준다

이를 통해 하나의 인스턴스를 기반으로 a,b를 생성했다. 귀찮게 여러번 DB 객체를 생성 안해주어도 된다는 장점 ! 
