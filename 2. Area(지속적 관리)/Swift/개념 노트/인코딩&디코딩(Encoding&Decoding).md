
## 디코딩이란 ?
> **디코딩**은 JSON(문자열 형태의 데이터)을 Swift의 타입으로 **변환**하는 과정이야.

예를 들어 이 JSON이 있다고 해보자:

``` json
{
  "name": "진혁",
  "age": 27
}
```

이걸 Swift 코드에서 쓰려면 이렇게 생긴 구조체가 필요해:

``` swift
struct Person: Decodable {
    let name: String
    let age: Int
}
```

그리고 이걸 **디코딩**해서 Swift에서 쓸 수 있게 만들려면 이렇게 해:

``` swift
let jsonData = """
{
  "name": "진혁",
  "age": 27
}
""".data(using: .utf8)!

let person = try? JSONDecoder().decode(Person.self, from: jsonData)
print(person?.name) // → "진혁"
```
> 즉, 디코딩은 JSON → Swift로 바꾸는 거야!

---

### 💡 그럼 "디코딩할 수 있는 타입"은 뭘까?

Swift에서는 JSON으로부터 디코딩이 되려면 반드시 그 타입이 `Decodable`이라는 프로토콜을 따라야 해.

#### ✅ `Decodable` 프로토콜을 따르는 타입 예시

``` swift
struct User: Decodable {
    let name: String
    let age: Int
}
```

- 위처럼 `Decodable`을 채택하면 JSONDecoder가 JSON을 이 구조체로 바꿔줄 수 있어.
    
- `Decodable`이 없다면 Swift는 “어떻게 이 JSON을 구조체로 바꿔야 할지” 몰라서 에러나.

---

### 🔄 반대로 "인코딩"도 있어

인코딩은 Swift → JSON

```swift
struct User: Codable {
    let name: String
    let age: Int
}

let user = User(name: "진혁", age: 27)
let jsonData = try? JSONEncoder().encode(user)
```
> `Codable = Encodable + Decodable` (양방향 가능)

---

### 🧠 한 줄 정리

- `Decodable`을 따르는 타입만 JSON에서 **Swift 구조체로 변환(디코딩)** 가능해.
    
- Swift는 타입이 `Decodable`을 따르고 있어야 `JSONDecoder().decode()`를 쓸 수 있어.
    

---

### 📦 정리 요약

|용어|뜻|
|---|---|
|디코딩|JSON을 Swift 구조체로 변환하는 것|
|Decodable|"나를 JSON에서 만들어도 돼!"라고 약속하는 프로토콜|
|JSONDecoder|디코딩을 해주는 도구|
|`T: Decodable`|제네릭 T는 JSON에서 디코딩될 수 있는 타입이어야 한다는 조건|