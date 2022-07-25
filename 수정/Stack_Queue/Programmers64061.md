# 64061 → 크레인 인형뽑기 게임
### 문제 정리📝
1. 게임 화면의 격자의 상태가 담긴 `2차원 배열 board`가 주어진다. 
> • board   
2차원 배열로 "5 x 5" 이상 "30 x 30" 이하  
각 칸에는 0 이상 100 이하인 정수가 담겨있고, 0은 빈 칸을 나타냄  
1 ~ 100의 각 숫자는 각기 다른 인형의 모양을 의미하며 같은 숫자는 같은 모양의 인형을 나타냄  
2. 인형을 집기 위해 크레인을 작동시킨 `위치가 담긴 배열 moves`가 주어진다. 
> • moves   
배열의 크기는 1 이상 1,000 이하  
각 원소들의 값은 1 이상이며 board 배열의 가로 크기 이하인 자연수
2. 크레인을 모두 작동시킨 후 터트려져 `사라진 인형의 개수`를 출력한다.
> 주의사항  
• 크레인 작동 시 집어지지 않는 경우 없음  
• 인형이 없는 곳에서 크레인이 작동하면 아무런 일도 일어나지 않음

</br>

## 접근🚶🏻
### 나의 생각 ▾
- board 배열을 보면 각 행의 같은 열 중에서 가장 앞에 있는 인형이 선택되는 것을 알 수 있다.
- 따라서 board 배열의 각 행의 같은 열에 해당하는 index를 순차적으로 탐색하여 0이 아닌 경우를 찾아서 처리할 수 있었다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ board:[[Int]], _ moves:[Int]) -> Int {
  var result = 0 
  var boards = board
  var basket = [Int]()

  for i in moves {
    for index in 0..<boards.count {
      if boards[index][i-1] != 0 {
        if basket.last == boards[index][i-1] {
          result += 2
          basket.removeLast()
        } else {
          basket.append(boards[index][i-1])
        }
        boards[index][i-1] = 0
        break
      }
    }
  }
  return result
}
```

</br>

### Additional 📂
- 어려운 문제라고 생각해서 골랐는데 생각보다 쉽고 재미있는 문제였다.
