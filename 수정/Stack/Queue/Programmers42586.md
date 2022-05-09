# 42586 → 기능개발
### 문제 정리📝
1. `progresses`를 입력받는다.
2. `speeds`를 입력받는다.
3. 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다.
> ex) progresses가 95%인 작업의 speeds가 하루에 4%라면 배포는 2일 뒤에 이루어진다.
4. 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성한다.
5. 작업의 개수(progresses, speeds배열의 길이)는 100개 이하이다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- progresses에 speeds를 추가했을 때, 맨 첫번째 인덱스부터 100이 되면 하나하나 제거해 나가면 되겠다고 생각했다.

- progresses와 speeds는 let이기 때문에 이것을 var 변수로 만들어주어 넣어준다. 

- while문을 사용하여 progressesTmp에 값이 빌때까지 반복한다. for문을 이용하여 progressesTmp에 speedsTmp를 한번씩 더해준다.

    ```
    ex)
    progressesTmp 값이 [95, 90, 99, 99, 80, 99] 이랬다면 → [96,91,100,100,81,100] 이런식으로 speedsTmp 값을 더해준다.
    ```

- progressesTmp에 값이 남아있는 동시에, progresses[0]이 100보다 크거나 같으면 while문의 조건을 만족하면 진입한다.

- progressesTmp의 firstIndex와 speedsTmp의 firstIndex를 제거한다. 

- cnt를 +1씩 추가해준다. 

- `progressesTmp에 값이 남아있는 동시에, progresses[0]이 100보다 크거나 같으면 while문의 조건을 만족하면 진입한다.` 라는 조건을 여전히 만족한다면 `progressesTmp의 firstIndex와 speedsTmp의 firstIndex를 제거하고, cnt를 +1씩 추가`를 반복한다.

- answer배열에 cnt값을 append() 함수를 이용해 삽입한다.

- progressesTmp에 값이 남아있지 않거나 progressesTmp[0]이 100보다 작다면 while문의 조건을 만족하지 못하고 지나간다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ progresses:[Int], _ speeds:[Int]) -> [Int] {  
    var progressesTmp = progresses
    var speedsTmp = speeds
    var answer = [Int]()
    
    while !progressesTmp.isEmpty {
        for i in 0..<progressesTmp.count {
            progressesTmp[i] += speedsTmp[i]
        }
        var cnt = 0
        while !progressesTmp.isEmpty && progressesTmp[0] >= 100 {
            progressesTmp.removeFirst()
            speedsTmp.removeFirst()
            cnt += 1
        }
        if cnt > 0 {
            answer.append(cnt)
        }
    }  
    return answer
}
```

</br>

### Additional 📂
- 
- 

