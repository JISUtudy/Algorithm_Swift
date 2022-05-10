# 42587 → 프린터
### 문제 정리📝
1. 현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities를 입력받는다.
> 인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다.
2. 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location을 입력받는다.
3. 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 출력한다.
> ex) 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄한다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 구현하는게 어려워 참고하였다. 
- `우선순위 큐`(우선순위 큐는 기본적으로 최대힙이므로)를 `내림차순`으로 정렬한다.
    ```swift
    var priorityQueue = priorities.sorted(by : >)
    ```
- 우선순위를 순회하면서 `enumerated()`를 이용하여 큐에 인덱스와 함께 우선순위를 저장한다.
    ```
    [(0, 1), (1, 1), (2, 9), (3, 1), (4, 1), (5, 1)]
    ```
- 큐가 비어있을 때까지 순회를 한다.
- 큐의 `맨 앞에 있는 우선순위`와 `우선순위 큐의 첫번째 값`을 `비교`한다.
- 큐의 맨앞에 있는 값의 인덱스가 내가 요청한 문서의 인덱스인지 확인한다.
- 우선순위의 값과 일치하므로 큐애 우선순위 큐에서 하나를 `pop`한다.
- 더 높은 우선순위의 값이 존재하므로 하나를 꺼내 `맨 뒤에 push` 한다.

</br>

### 내 코드👨🏻‍💻
```swift
func solution(_ priorities:[Int], _ location:Int) -> Int {
    var queue: [(Int, Int)] = []
    var priorityQueue = priorities.sorted(by : >)
    var answer = 0
    
    priorities.enumerated().forEach { (index, property) in
        queue.append((index, property))
    }
    
    while !queue.isEmpty {
        if queue.first!.1 == priorityQueue.first! {
            if queue.first!.0  == location {
                return answer + 1
            }
            answer += 1
            queue.removeFirst()
            priorityQueue.removeFirst()
        } else {
            queue.append(queue.removeFirst())
        }
    }
    return answer
}
```

</br>

### Additional 📂
- 구현하는 것이 어려워 블로그를 참고하였다. 
- 인덱스의 값을 쉽게 찾기위해 enumerated를 사용해서 적용해보는 방법을 배울 수 있었다. 

