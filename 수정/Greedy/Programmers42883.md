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
- result에 새로 들어운 수보다 작은 수들을 지워주었다.
- 12번 테스트케이스는 하나도 안지워지는 경우인데, 이 때는 가장 작은 수가 가장 뒤에 있기 때문에 뒤에서부터 k번 지워주었다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ number:String, _ k:Int) -> String {
    var arr = number.map { Int(String($0))! }
    var count = 0
    var result = [Int]()

    for i in 0..<arr.count {
        while result.count > 0 && result.last! < arr[i] && count < k {
            result.removeLast()
            count += 1 
            
            if count == k{
                break
            }
        }
        result.append(arr[i])
    }
    if count == 0 {
        for i in 1...k{
            result.removeLast()
        }
    }
    
    return result.reduce(""){ $0 + "\($1)" }
}
```

</br></br>

### Additional 📂
- 테스트 케이스 하나가 잘 안돼서 다른 분의 코드를 조금 참고해서 해결할 수 있었다.
- 조금 더 생각해보고 푼다면 혼자서도 가능할 것 같다.