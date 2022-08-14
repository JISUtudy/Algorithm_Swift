# 81302 → 거리두기 확인하기
### 문제 정리📝
1. 크가가 `5*5`인 대기실이 있다.
2. 거리두기를 위해 응시자들 끼리는 `맨해튼 거리`가 `2`이하로 앉지 말아야 하지만, `파티션`으로 막혀 있을 경우는 허용이 된다.
3. `places`로 각 대기실의 정보를 준다. `P`는 응시자가 앉아있는 자리이며, `O`는 빈 테이블을 의미하고, `X`는 파티션을 의미한다.
4. 각 대기실은 거리두기를 잘 지키고 있다면 `1`을, 지켜지지 않는다면 `0`을 반환해준다.
> 맨해튼 거리: |x1 - x2| + |y1 - y2|

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 지문을 읽으며 `bfs`알고리즘이 생각이 났다. `P`인 지점의 좌표를 `for`문에 넣어 구현하면 되겠다는 생각을 했다.

- 맨해튼 거리를 위해 `distance`라는 2차원 Int 배열을 선언하여, 이동할 수 있는 칸의 좌표를 `queue`에 삽입해줌과 함께 해당 좌표의 `distance` 값을 `+1` 해주면 된다고 생각했다(맨해튼 거리를 위함). 방문 처리를 위한 `visited` 라는 2차원 Bool 타입으로 선언해주었다. 그래서 해당 두 배열을 이용해 문제를 구현하면 쉽게 해결할 수 있을 것이라고 생각했다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

let dx = [-1, 0, 1, 0]
let dy = [0, -1, 0, 1]

func is_valid_coord(_ x: Int, _ y: Int) -> Bool {
    return (0 <= x && x < 5) && (0 <= y && y < 5)
}

func bfs(_ b: [[String]]) -> Int {
    var people = [(Int, Int)]()
    
    for i in 0..<5 {
        for j in 0..<5 {
            if b[i][j] == "P" {
                people.append((i, j))
            }
        }
    }
    
    for p in people {
        var queue = [(Int, Int)]()
        queue.append((p.0, p.1))
        
        var visited = Array(repeating: Array(repeating: false, count: 5), count: 5)
        var distance = Array(repeating: Array(repeating: 0, count: 5), count: 5)
        visited[p.0][p.1] = true
        
        while !queue.isEmpty {
            let (cx, cy) = queue.removeFirst()
            
            for i in 0..<4 {
                let nx = cx + dx[i]
                let ny = cy + dy[i]
                
                if is_valid_coord(nx, ny) && !visited[nx][ny] {
                    if b[nx][ny] == "O" {
                        queue.append((nx, ny))
                        visited[nx][ny] = true
                        distance[nx][ny] = distance[cx][cy] + 1
                    }
                    
                    if b[nx][ny] == "P" && distance[cx][cy] <= 1 {
                        return 0
                    }
                }
            }
        }
    }
    return 1
}

func solution(_ places:[[String]]) -> [Int] {
    var answer = [Int]()
    
    for place in places {
        var board = [[String]]()
        for p in place {
            board.append(p.map{ String($0) })
        }
        answer.append(bfs(board))
    }
    return answer
}
```

</br></br>

### Additional 📂
- `bfs` 알고리즘 문제를 최근에 잘 안 풀었더니 감을 좀 잃었던 것 같다. 이 문제를 통해 어느 정도 감을 익힐 수 있어서 좋았다.

- 알고리즘을 앞으로 더 성실히 풀어야겠다고 다짐을 하게 해준 고마운 문제였다 😏