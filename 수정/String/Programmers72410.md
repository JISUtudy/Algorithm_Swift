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
- 단계별로 처리과정을 구해 리턴할 수 있도록 만들었다. 
- 1단계, 2단계를 처리하기위해 `possible`이라는 상수를 만들어, 새로운 아이디를 받으면 가장 먼저 `contains` 함수로 문자열 포함여부를 확인하고 str에 append 해주었다.
- 3단계를 처리하기 위해 `replacingOccurrences`를 사용하여 `..`을 `.`으로 치환해주었다. 
- 4단계를 처리하기 위해 str 배열에 `.`이 있다면 첫번째 인덱스를 삭제해주었다.
- 5단계는 빈 문자열일 때, a를 대입해주기 위해 if문을 사용했다.
- 6단계는 아이디의 길이가 16자 이상이므로, str의 길이를 비교해주어 그 값에 맞지않는 수는 제거해주었다.
- 7단계는 아이디의 길이가 2자 이하인지 아닌지 비교하고 그렇다면 추가하고 아니면 제거해주었다.
- 각 단계별로 처리해 str을 리턴할 수 있었다.

</br>

### 내 코드👨🏻‍💻

```swift
import Foundation

func solution(_ new_id:String) -> String {
    var id = new_id
    id = id.lowercased()
    var str: [Character] = []
    var arr = Array(id)
    let possible = "0123456789abcdefghijklmnopqrstuvwxyz-_."

    for i in 0..<arr.count {
        if possible.contains(arr[i]) {
            str.append(arr[i])
        }
    }
    id = String(str)

    while id.contains("..") {
        id = id.replacingOccurrences(of: "..", with: ".")
    }

    str = Array(id)

    if str[0] == "." {
        str.removeFirst()
    }

    if str.count == 0 {
        str.append("a")
    }

    while str.count >= 16 {
        str.remove(at: str.count-1)
    }
    
    if str[str.count-1] == "." {
        str.remove(at: str.count-1)
    }

    if str.count <= 2 {
        while str.count != 3 {
            str.append(str[str.count-1])
        }
    }
    return String(str)
}
```

### Additional 📂
- 문자열 치환 방법 `replacingOccurrences(of:, with:)`과 소문자 변경 `lowercased` 등 몰랐던 문자열 변경 방법들을 새롭게 알 수 있었다.