# 64061 → 크레인 인형뽑기 게임
### 문제 정리📝
1. `5개`칸으로 이루어진 인형뽑기 기계가 있다.
2. 해당 칸에는 빈 공간`(0)`과 인형 종류`(1~100)`로 이루어져있다.
3. 크레인으로 인형을 뽑으려고 하는데 어떤 칸으로 가서 크레인을 내릴지에 대한 `크레인 작동 위치를 담은 배열(moves)`가 주어진다.
4. 크레인을 통해 뽑은 인형은 `바구니`에 쌓아두는데, 해당 바구니에 `같은 종류의 인형`이 만나면 `두 인형`은 사라진다.
> 단, 빈 공간을 집으려고 하면 아무러 일이 일어나지 않으며, 인형이 집어지지 않는 경우는 없다고 가정한다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 지문을 읽자마자 `Queue`가 생각이 났다. `Queue`의 `마지막 원소`와 `앞으로 들어올 원소`를 비교하여, 같으면 `popLast()`(Queue라고 구현한다면) 혹은 `removeLast()`(Stack으로 구현한다면)로 같은 인형들을 제거해 줄 수 있을 것 같았다.

- 크레인이 내려가는 `index`에 `board`의 원소를 `for`문을 통해 위에서부터 순차적으로 검사하며 내려간다. `board[i][index] != 0`이 될 경우에 해당 값이 `바구니`의 마지막 원소와 같은지 체크하는 `my_list.last == board[i][index]`를 거쳐 처리를 해주면 될 것 같다.

- 위에 조건이 `True`라면 `my_list`에 마지막 원소를 두 번 제거해준뒤, `카운팅 횟수 += 2`를 해주면 될 것으로 보였다.

</br>


### 내 코드👨🏻‍💻
```swift
func solution(_ board:[[Int]], _ moves:[Int]) -> Int {
    var my_list = [Int]()
    var my_board = board
    var remove_cnt: Int = 0
    
    for index in moves {
        for (i, value) in my_board.enumerated() {
            if value[index-1] != 0 {
                my_list.append(value[index-1])
                my_board[i][index-1] = 0
                break
            }
        }
        
        if my_list.count >= 2 {
            if my_list[my_list.endIndex-1] == my_list[my_list.endIndex-2] {
                my_list.removeLast()
                my_list.removeLast()
                remove_cnt += 2
            }
        }
    }
    
    return remove_cnt
}
```

</br>


### Additional 📂
- 문제가 그림도 많고 지문도 길어서 엄청 어려울 줄 알았으나 천천히 읽어보니 쉽게 풀 수 있었던 문제였던 것 같다.

- 요즘 PS를 조금 소홀히 한 것 같다.. 앞으로 더 신경을 써서 그나마 조금이라도 있는 실력이 녹슬지 않게 해주어야겠다..😂
