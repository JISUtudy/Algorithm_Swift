# 67256 → 키패드 누기
### 문제 정리📝
1. `번호들`을 입력 받는다.
2. `왼손 엄지손가락`과 `오른손 엄지손가락`을 이용해 각각의 `번호`를 키패드를 통해 누르려고 한다.
3. 각 손들은 고정적으로 누를 수 있는 번호가 있는데, `왼손`은 `1, 4, 7`을, `오른손`은 `3, 6, 9`가 있다.
4. 그 외에 `숫자`는 `가까운 거리` 거리에 위치한 손을 이용해 누르려고 하는데, `거리가 똑같을 땐` `왼손잡이`는 `왼손`으로, `오른손잡이`는 `오른손`으로 누른다.
5. 왼손으로 누르면 `L`, 오른손으로 누르면 `R`을 반환한다.
6. 주어진 번호를 키패드로 표현하려고 할 때 반환되는 `문자열`을 구한다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 처음엔 `bfs`알고리즘을 이용해 `왼손`과 `오른손`의 좌표를 각각 보내어 거리가 가까운지를 체크하려고 했는데, 생각해보면 현재 손들의 위치와 눌러야하는 숫자의 위치만 알고 있으면 해당 좌표들의 거리를 `절대값`으로 추출만 해도 될 것으로 생각을 했다.

- 키패드를 `2차원 배열`로 표현하고, 각 숫자들의 위치를 알아내는 `함수`와 거리를 구해주는 `함수`를 만들면 쉽게 구현할 수 있을 것이라고 생각했다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ numbers:[Int], _ hand:String) -> String {
    var board = Array(repeating: Array(repeating: "0", count: 3), count: 4)
    var result: String = ""
    var left_hand: (Int, Int) = (3, 0)
    var right_hand: (Int, Int) = (3, 2)

    var number: Int = 1
    for i in 0..<4 {
        for j in 0..<3 {
            board[i][j] = String(number)
            number += 1
        }
        if i == 3 {
            board[i][0] = "*"
            board[i][1] = "0"
            board[i][2] = "#"
        }
    }

    func find_coord(_ num: Int) -> (Int, Int) {
        var x: Int = 0
        var y: Int = 0
        
        for i in 0..<4 {
            for j in 0..<3 {
                if num == Int(board[i][j]) {
                    x = i
                    y = j
                }
            }
        }
        return (x, y)
    }
    
    func make_dist(_ cx: Int, _ cy: Int, _ tx: Int, _ ty: Int) -> Int {
        return abs(cx - tx) + abs(cy - ty)
    }

    for num in numbers {
        let data = find_coord(num)
        
        if [1, 4, 7].contains(num) {
            result += "L"
            left_hand = (data.0, data.1)
        }
        else if [3, 6, 9].contains(num) {
            result += "R"
            right_hand = (data.0, data.1)
        }
        else {
            let left_cnt = make_dist(data.0, data.1, left_hand.0, left_hand.1)
            let right_cnt = make_dist(data.0, data.1, right_hand.0, right_hand.1)
            
            if left_cnt < right_cnt {
                result += "L"
                left_hand = (data.0, data.1)
            }
            else if right_cnt < left_cnt {
                result += "R"
                right_hand = (data.0, data.1)
            }
            else {
                if hand == "right" {
                    result += "R"
                    right_hand = (data.0, data.1)
                }
                else {
                    result += "L"
                    left_hand = (data.0, data.1)
                }
            }
        }
    }
    return result
}
```

</br></br>

### Additional 📂
- 구현하는 동안 의식에 흐름대로 생각없이 구현하다가 지저분하고, 비효율적인 구현을 했었다.</br>
문제를 접근할 때 여러 방법을 생각해보고, 그 중 가장 효율적인 방법으로 구현해야겠다고 생각하게 된 문제였다.