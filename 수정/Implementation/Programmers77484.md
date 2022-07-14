# 77484 → 로또의 최고 순위와 최저 순위
### 문제 정리📝
1. 구매한 로또를 담은 배열 `lottos`와 당첨번호를 담은 배열 `win_nums`가  주어진다.
2. 알 수 없는 번호인 `0`은 당첨 번호가 될 수도 있고, 안될 수도 있다.
3. `lottos`가 `win_nums`와 일치하는 개수를 토대로 `당첨 가능한 최고 순위와 최저 순위를 차례대로 배열에 담아 등수`를 반환해준다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 구매한 로또를 담은 배열 `lottos`와 당첨번호를 담은 배열 `win_nums`를 `for문으로 비교`해주면서 구할 수 있었다.
- 0이 들어간 수는 무조건 최고 점수가 될 수 있기 때문에 lottos라는 배열에 0이 있으면 `최고점수에 1`을 더해주었다.
- lottos의 배열과 win_nums의 배열이 같으면 `최저점수에 1`을 더해주었다.
- `switch문`을 사용해 순위를 매겨 return 할 수 있었다,

</br>

### 내 코드👨🏻‍💻

```swift
import Foundation

func solution(_ lottos:[Int], _ win_nums:[Int]) -> [Int] {

  var min_cnt = 0
  var max_cnt = 0

  for i in lottos {
    if i == 0 {
      max_cnt += 1
    }
    for j in win_nums {
      if i == j {
        min_cnt += 1
      }
    }
  }
  
  return [rank(max_cnt + min_cnt), rank(min_cnt)]
}

func rank(_ cnt: Int) -> Int{
    switch cnt {
    case 6: return 1
    case 5: return 2
    case 4: return 3
    case 3: return 4
    case 2: return 5
    default: return 6
    }
}
```

### Additional 📂
- 쉽게 풀 수 있는 문제였지만, 간결하고 더 좋은 코드로 풀 수 있도록 공부를 해야할 것 같다.