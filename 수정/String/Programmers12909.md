# 12909 → 올바른 괄호
### 문제 정리📝
1. 괄호로만 구성된 문자열(s)이 주어진다.
2. 괄호 문자열은 (로 열렸으면 반드시 짝지어서 ) 문자로 닫혀야 한다.
3. 문자열(s)가 주어질 때, 올바른 괄호 문자열이면 true를 반환하고, 올바르지 않는 괄호 문자열이면 false를 반환한다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- `(` 과 `)`를 카운트 해줄 변수를 만들어, for문을 사용하여 s의 글자 중에 `(`라면 count를 1증가 시키고 `)`라면 1감소 시킨다. 

- count가 0보다 작으면 `)`의 갯수가 더 많다는 것이기 때문에 for문을 중단시키고, count가 0이라면 true를, 아니라면 false로 결과를 반환한다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation
 
func solution(_ s:String) -> Bool
{
    var count = 0
    for ch in s {
        if ch == "(" {
            count += 1
        } else {
            count -= 1
        }
        if count < 0 {
            break
        }
    }
    return count == 0 ? true : false
}
```

</br>

### Additional 📂
- 가볍게 풀 수 있는 문제였다.
