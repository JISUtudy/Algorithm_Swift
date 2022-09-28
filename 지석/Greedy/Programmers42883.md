# 42883 → 큰 수 만들기
### 문제 정리📝
1. `number`라는 문자열과 `k`라는 정수가 주어진다.
2. `number`는 숫자로 이루어져 있는데 이 중 `k`개의 숫자를 제거했을 때 `가장 큰 수`를 반환해준다.

```
example ▾
number = "1924", k = 2
result = [19, 12, 14, 92, 94, 24]
return 94
```

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 지문에선 `가장 큰 값`만 만들어주면 되는 부분이었기에 `그리디 알고리즘`이라고 생각이 들었다. 그래서 `result`라는 값을 저장해줄 배열을 하나 만들어 값을 하나씩 저장을 해주는데, 여기서 `k`를 카운팅 해줄 변수를 만들어 해당 `for문`을 돌리면서 추가되는 마지막 값이 이전에 값보다 큰지,작은지에 대한 여부를 따져 제거해주면서 카운팅을 해줄 수 있을 것으로 보였다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ number:String, _ k:Int) -> String {
    let integer_List = number.map { Int(String($0))! }
    var kCount = k
    var result = [Int]()
    
    for index in integer_List.indices {
        while kCount > 0 && !result.isEmpty && result.last! < integer_List[index] {
            result.removeLast()
            kCount -= 1
        }
        result.append(integer_List[index])
    }
    
    if kCount == k {
        for _ in 0..<k {
            result.removeLast()
        }
    }
    
    return result.reduce("") { $0 + "\($1)"}
}
```

</br></br>

### Additional 📂
- 문제를 푸는 부분에서 `[Int]`을 `String`으로 변환하는 과정에서 `reduce`의 새로운 기능을 알게 되었다. 막연하게 총합을 구할 때만 사용을 했었다면 그걸 응용해 요소들을 `String`으로 합쳐주는 형식이었다.

- 나름 배울 것이 많았던 문제였다. 특히 `while`문 구현부와 `if kCount == k`이 구현부가 많은 시간을 소요시키는 요소였다.. 12번 케이스... 그래도 풀었으니 만족! 😅