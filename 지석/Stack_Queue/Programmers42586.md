# 42586 → 기능개발
### 문제 정리📝
1. 작업의 진도 `progresses`를 입력받는다.
2. 각각의 작업 속도 `speeds`를 입력받는다.
3. 각각의 작업들은 먼저 배포되어야 하는 순서대로 입력을 받기 때문에 작업이 완료 되었을 때 뒤에 작업도 완료가 되었다면 같이 배포가 된다.
4. 한번 배포 될 때마다 완료되는 개수를 출력한다.
> 단, 작업의 진도가 95%이고, 작업 속도가 4%라고 하면 2일이 걸린다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 걸리는 작업의 일 수를 먼저 구해보기로 했다.
- 작업이 걸리는 시간은 `(100 - progresses - 1) / speeds + 1`라고 정의했다.
- 작업의 걸리는 시간을 배열에 담아 첫 원소보다 작을 경우 `count`를 누적시켜주고, 클 경우 `count`를 `result`배열에 담아 리턴하기로 했다.

</br>


### 내 코드👨🏻‍💻
```swift
func solution(_ progresses: [Int], _ speeds: [Int]) -> [Int] {
    
    var valueList = [Int]()
    var count: Int = 1
    var result = [Int]()
    
    for idx in 0..<progresses.count {
        valueList.append((100-progresses[idx] - 1) / speeds[idx] + 1)
    }
    
    var value = valueList.removeFirst()
    
    valueList.forEach {
        if value > $0 {
            count += 1
        } else {
            result.append(count)
            count = 1
            value = $0
        }
    }
    
    if count >= 1 {
        result.append(count)
    }
    
    return result
}
```

</br>


### Additional 📂
- 일단 좀 불편한건 여러 케이스 중 실패 케이스가 떴다..
- 조만간 다시 풀어서 추가적으로 코드를 달아보려고 한다 😂
