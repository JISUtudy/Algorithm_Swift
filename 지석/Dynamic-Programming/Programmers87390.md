# 87390 → n^2 배열 자르기
### 문제 정리📝
1. `n`, `left`, `right`가 주어진다.
2. `n * n` 2차원 배열을 만들고, 해당 배열의 요소들을 아래와 같이 표기된다.
3. 아래와 같은 배열을 만들었을 때, 1차원 배열로 나열을 하게 되면 `행`별로 이어서 값이 만들어진다.
4. 1차원 배열로 이루어졌을 때, `left`인덱스부터 `right`인덱스까지의 요소를 반환해준다.

```
n = 2    n = 3   n = 4

 1 2     1 2 3   1 2 3 4
 2 2     2 2 3   2 2 3 4
         3 3 3   3 3 3 4
                 4 4 4 4

n = 2 ▾
[1, 2] + [2, 2]
[1, 2, 2, 2]

n = 3 ▾
[1, 2, 3] + [2, 2, 3] + [3, 3, 3]
[1, 2, 3, 2, 2, 3, 3, 3, 3]

n = 4 ▾
[1, 2, 3, 4] + [2, 2, 3, 4] + [3, 3, 3, 4] + [4, 4, 4, 4]
[1, 2, 3, 4, 2, 2, 3, 4, 3, 3, 3, 4, 4, 4, 4, 4]
```

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 해당 문제는 예시가 시뮬레이션으로 나왔는데 배열 형태를 보면서 `DP`로 접근해야 풀 수 있을 것으로 보였다.

- 해당 배열들의 값들은 규칙적으로 값이 변하기 때문에 점화식만 찾으면 쉽게 구현할 수 있을 것이라고 생각했다.

</br>

### 시간초과 코드👨🏻‍💻
```swift
import Foundation

func solution(_ n:Int, _ left:Int64, _ right:Int64) -> [Int] {
    var num_Array = Array(repeating: Array(repeating: 0, count: n), count: n)
    var ans = [Int]()
    var result = [Int]()
    var idx: Int = 0

    for i in 0..<n {
        idx = i + 1
        for j in 0..<n {
            num_Array[i][j] = idx <= j ? j+1 : idx
        }
    }

    for row in num_Array {
        for v in row {
            ans.append(v)
        }
    }

    for i in left...right {
        result.append(ans[Int(i)])
    }

    return result
}
```

- 처음엔 `2차원 배열`로 구성하여, 구현하였으나 `시간 초과`가 떴다. 이에 더 간단하게 값을 추출할 수 있는 방법이 있음을 확신하고 점화식을 구해보았다. 아래 코드를 참고해보자

</br></br>

### 해결 코드👨🏻‍💻
```swift
import Foundation

func solution(_ n:Int, _ left:Int64, _ right:Int64) -> [Int] {
    let n = Int(n)
    var result = [Int]()
    
    for i in left...right {
        let max_Value = max(Int(i) / n + 1, Int(i) % n + 1)
        result.append(max_Value)
    }
    
    return result
}
```

- 각 행과 열은 행의 값으로 시작을 한다. 1행은 1, 2, 3... 2행은 2, 2, 3... 이러한 규칙을 이용해 점화식을 만들어 보았을 때 아래와 같이 볼 수 있다.

- `max(i/n+1, i%n+1)`로 점화식을 세울 수 있었고, 이에 맞게 구현하여 시간초과를 해결할 수 있었다.

</br></br>

### Additional 📂
- `DP`문제는 늘 규칙을 찾기 위해 여러 생각을 하게 만드는 문제인 것 같다. 나름 문제를 푸는 과정에서 여러 시도를 해보며 고통을 받다가 나름의 점화식을 찾아 구현해 문제를 해결하면 뿌듯하다.

- 다른 사람의 코드에선 `.map`을 통해 더 간결하게 구현을 하는 것을 보았다. 불필요한 변수 생성 없이 더 간결한 코드를 구현하기 위해 더 노력해야겠다는 생각을 하게 해주는 고마운 문제였다.