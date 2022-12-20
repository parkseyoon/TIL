# 옵셔널(Optional)

3줄 요약
1. 스위프트는 프로그램의 안전성을 높혀 오류를 nil로 반환함으로써 개발자에게 문제가 있다는 것을 알린다.
2. 위의 상황에 nil을 반환하기 위한 타입을 옵셔널이라고 한다.
3. 옵셔널은 nil이거나 nil이 아닌 값만 가질 수 있고, 사용하려면 해제를 해야한다.

## 옵셔널이란?
값이 존재할 수도, 존재하지 않을 수도 있는 타입이며 존재할 경우 옵셔널 타입의 값을, 존재하지 않는다면 nil(NULL)을 값으로 가지고 있다.

옵셔널은 별도의 자료형이 아닌, 기본 자료형에 대응하는 타입이다. (e.g. 옵셔널 Int 타입, 옵셔널 String 타입)

### 선언 방법

```swift
let shortForm: Int? = Int("2")
let longForm: Optional<Int> = Int("2")
```

변수를 선언할 때 타입 뒤에 `?`를 붙히거나 `Option<>`의 꺾쇠 괄호 안에 타입을 적으면 된다.

## 옵셔널 바인딩(Optiona)
명시적 해제인 옵셔널 바인딩은 주로 사용하는 방법 중 하나이다.   
nil인지 아닌지 체크 후 안전한 값을 추출할 수 있는 방법이다.

### if let
```swift
var nickname: String? = "poodle"

print(nickname) // Optional("poodle")


if let name = nickname {
  print(name) // poodle
} else {
  print("nickname is nil")
}
```

if let의 name이라는 상수는 if 안에서만 사용 가능하다.   
만약 nickname이 nil이라면 `nickname is nil`이라고 출력되었을 것이다.

```swift
var nickname: String? = "poodle"
var password: String? = "1234"

if let name = nickname, let secret = password {
    print("nickname = \(name), password = \(secret)") // nickname = poodle, password = 1234
} else {
    print("nickname or password is nil")
}
```

위와 같이 한 번에 여러개의 값을 바인딩 할 수 있다.

### guard let
```swift
var nickname: String? = "poodle"

guard let name = nickname else { return }
print(name) // poodle
```

guard let은 뒤에 따라붙는 bool 타입의 값이 `참(true)` 일 경우 코드가 계속 실행되며, `거짓(false)`일 경우에는 else의 블록 내부 코드가 실행된다.

else 내부 코드에는 `return`, `break`, `continue`, `throw`등 <b>제어문 전환 명령어</b>를 사용해야 한다.

if let과는 다르게 guard문은 항상 else 구문이 뒤에 따라와야 하며, guard문은 함수 전체에서 추출된 상수나 함수를 사용할 수 있다.

## Force Unwrapping
옵셔널의 값을 강제로 추출하는 방법이다.

```swift
// 사용할 때 강제 추출
var nickname: String? = "poodle"

print("\(nickname!)") // poodle

// 선언할 때 강제 추출
var password: String! = "poodle"

print("\(password)") // poodle

// nil일 때 강제 추출
nickname = nil

print("\(nickname!)") // 강제로 추출할 값이 없어 런타임 오류 발생
```

옵셔널 강제 추출 방법은 안전하지 않기 때문에 옵셔널 바인딩을 사용하여 값을 추출하는 방법이 좋다.


> ## Reference 
> [옵셔널(optional)이란?](https://hodev.tistory.com/106#recentComments)   
> [Apple Developer Optional](https://developer.apple.com/documentation/swift/optional)   
> [야곰 옵셔널 값 추출](https://youtu.be/YBofMKyfDaQ)   
> [if let과 guard let의 차이는?](https://jud00.tistory.com/entry/%EC%98%A4%EB%8A%98%EC%9D%98-Swift-%EC%A7%80%EC%8B%9D-if-let-%EA%B3%BC-guard-let%EC%9D%98-%EC%B0%A8%EC%9D%B4%EB%8A%94)