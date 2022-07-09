# 72410 → 신규 아이디 추천
### 문제 정리📝
1. `아이디(new_id)`가 주어진다.
2. 해당 아이디를 아래에 규칙에 따라 변형시켜 반환시켜주면 된다.
```
1단계 new_id의 모든 대문자를 대응되는 소문자로 치환합니다.
2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
3단계 new_id에서 마침표(.)가 2번 이상 연속된 부분을 하나의 마침표(.)로 치환합니다.
4단계 new_id에서 마침표(.)가 처음이나 끝에 위치한다면 제거합니다.
5단계 new_id가 빈 문자열이라면, new_id에 "a"를 대입합니다.
6단계 new_id의 길이가 16자 이상이면, new_id의 첫 15개의 문자를 제외한 나머지 문자들을 모두 제거합니다.
     만약 제거 후 마침표(.)가 new_id의 끝에 위치한다면 끝에 위치한 마침표(.) 문자를 제거합니다.
7단계 new_id의 길이가 2자 이하라면, new_id의 마지막 문자를 new_id의 길이가 3이 될 때까지 반복해서 끝에 붙입니다.
```

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 해당 문제는 크게 어려움 없이 각 조건에 맞춰 변형만 시켜주면 될 것으로 보였다.

- 각각 단계들을 `함수`로 구분해 `모듈화`시켜서 각각의 `함수`를 거쳐 원하는 `문자열`을 만들면 풀 수 있을 것으로 보였다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func LowAlphabet(_ id: String) -> String {
    let newString = id.lowercased()
    return newString
}

func Remove_character(_ id: String) -> String {
    let arrID = Array(id)
    let possible = "0123456789abcdefghijklmnopqrstuvwxyz-_."
    var newString: [Character] = []
    for ch in arrID {
        if possible.contains(ch) {
            newString.append(ch)
        }
    }
    return String(newString)
}

func Change_points(_ id: String) -> String {
    var newString = id
    while true {
        if newString.contains("..") {
            newString = newString.replacingOccurrences(of: "..", with: ".")
        } else{ break }
    }
    return newString
}

func Check_point(_ id: String) -> String {
    var newString = id
    if newString.first == "." {
        newString.removeFirst()
    }
    if newString.last == "." {
        newString.removeLast()
    }
    return newString
}

func Fill_string(_ id: String) -> String {
    if id.isEmpty {
        return "a"
    } else { return id }
}

func Cut_string(_ id: String) -> String {
    var newString = id
    while newString.count >= 16 {
        newString.removeLast()
    }
    if newString.last == "." {
        newString.removeLast()
    }
    return newString
}

func Append_character(_ id: String) -> String {
    var newString = id
    while newString.count <= 2 {
        newString = newString + String(newString.last!)
    }
    return newString
}

func solution(_ new_id:String) -> String {
    var newString = new_id
    newString = LowAlphabet(newString)
    newString = Remove_character(newString)
    newString = Change_points(newString)
    newString = Check_point(newString)
    newString = Fill_string(newString)
    newString = Cut_string(newString)
    newString = Append_character(newString)
    return newString
}
```

</br>

### Additional 📂
- 문자열을 다루는 부분에서 문법이 다소 햇갈리는 부분이 있었으나 크게 어려움이 없었던 문제였다.