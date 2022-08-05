# 77884 → 약수의 개수와 덧셈
### 문제 정리📝
1. 두 정수 `left`와 `right`가 매개변수로 주어진다.
2. `left`부터 `right`까지의 모든 수들 중에서, 약수의 개수가 짝수이면 더하고, 홀수이면 뺀 수를 반환하면 된다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 쉽게 `for`문을 통해 `약수`를 찾아주면 될 것으로 보였다.</br>`num % i == 0` 해당 조건으로 접근하면 쉽게 찾을 수 있고, 이 조건을 만족하면 카운팅을 증가시키면 될 것으로 보였다.

- 위 `for`문을 통해 쉽게 풀 수 있으나, 쉬운 문제인만큼 `고차함수(map, filter, reduce)`를 이용해 풀어보기로 했다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func find_division(_ num: Int) -> Int {
    return (1...num).filter { num % $0 == 0}.count % 2 == 0 ? num : -num
}

func solution(_ left:Int, _ right:Int) -> Int {
    return (left...right).map { find_division($0) }.reduce(0, +)
}
```

</br></br>

### Additional 📂
- 쉬운 문제였던만큼 고차함수를 연습하기 좋았던 문제였던 것 같다.

- 고차함수를 더 능숙히 다룰때까지 더 연습을 해야겠다고 생각하게 해준 문제였다.