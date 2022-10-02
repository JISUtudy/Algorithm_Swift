# 92335 → k진수에서 소수 개수 구하기
### 문제 정리📝
1. 양의 정수 `n`이 주어진다. 
2. 이 숫자를 `k진수로 바꿨을 때`, 변환된 수 안에 아래 조건에 맞는 `소수(Prime number)가 몇 개인지 반환`한다.

```
조건 ▾
- 0P0처럼 소수 양쪽에 0이 있는 경우
- P0처럼 소수 오른쪽에만 0이 있고 왼쪽에는 아무것도 없는 경우
- 0P처럼 소수 왼쪽에만 0이 있고 오른쪽에는 아무것도 없는 경우
- P처럼 소수 양쪽에 아무것도 없는 경우
단, P는 각 자릿수에 0을 포함하지 않는 소수이다.
```

```
Example ▾
101은 P가 될 수 없다.
437674을 3진수로 바꾸면 211020101011이다. 
여기서 찾을 수 있는 조건에 맞는 소수는 왼쪽부터 순서대로 211, 2, 11이 있으며, 총 3개이다. 
(211, 2, 11을 k진법으로 보았을 때가 아닌, 10진법으로 보았을 때 소수여야 한다는 점에 주의) 211은 P0 형태에서 찾을 수 있으며, 2는 0P0에서, 11은 0P에서 찾을 수 있다.
```

</br>

## 접근🚶🏻
### 나의 생각 ▾
- n을 k진수로 바꾸고, 바꾼 문자를 0을 기준으로 나누어준다.
- 그리고 소수인지 판별해주고, 소수인 숫자의 갯수를 반환해준다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ n:Int, _ k:Int) -> Int {
    let change = String(n,radix: k)
    let num = change.split(separator: "0")
    return num.filter{ primeNumber(Int($0)!) }.count
}

func primeNumber(_ n:Int) -> Bool {
    if n == 1  { return false }
    if n == 2 || n == 3 { return true }
    for i in 2...Int(sqrt(Double(n))) {
        if n % i == 0 {
            return false
        }
    }
    return true
}
```

</br></br>

### Additional 📂
- 이번건 시간이 좀 부족해서 다른 분들의 코드를 참고해서 풀었다. 
- 다음부터는 참고하더라도 바로 풀지말고 1-2일 정도 있다가 내가 이해한 방식대로 다시 풀어보는 방법으로 풀면 좋을 것 같다.