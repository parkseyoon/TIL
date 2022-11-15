# Alert 띄우는 방법

## Alert 이란?
주로 사용자에게 중요한 알림이나 경고 메세지를 나타내야 할 때 사용하는 경고 표시 방법이다.
경고 메세지를 통해 메세지와 함께 두 가지 이상의 선택을 요구할 수도 있고 선택에 따라 특정 작업도 수행할 수 있다.

## Alert 창의 과거
Alert은 다음과 같은 파라미터를 가지고 있었다.

```swift
Alert(title: Text, message: Text?, dismissButton: Alert.Button?)
```

그리고 다음 코드와 같이 버튼과 `@State` 변수를 만들어, 버튼을 누르면 원하는 Alert 창이 나오게 할 수 있었다.

```swift
struct ContentViewNine: View {
    @State private var showingAlert = false
    
    var body: some View {
        Button(action: {
            self.showingAlert = true
        }) {
            Text("Show Alert")
        }
        .alert(isPresented: $showingAlert) {
            Alert(title: Text("Title"), message: Text("This is a alert message"), dismissButton: .default(Text("Dismiss")))
        }
    }
}
```

iOS 13과 14를 지원하기 위해서는 여전히 Alert을 이렇게 구현해야 한다.

## Alert 창의 현재
위의 Alert 표시 방법은 더 이상 사용되지 않는다.
View 프로토콜의 modifier인 `alert(...)`을 사용해서 alert 창을 띄울 수 있다.
iOS 15부터는 `alert` modifier로 Alert이 대체되었다.

```swift
struct ContentView: View {
  @State private var showing = false
  
  var body: some View {
    Button("Alert 띄우기") {
        showing = true
    }
    .alert("메시지", isPresented: $showing) {
      Button("OK", role: .cancel) { ... }
    }
  }
}
```