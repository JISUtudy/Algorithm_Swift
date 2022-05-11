# 42587 → 프린터
### 문제 정리📝
1. `문서의 중요도`를 입력받는다.
2. 각각의 문서에서 `location`의 매개변수를 받을 때 해당 `location`번째에 있는 문서는 중요도에 따라 몇 번째로 출력이 되는지 출력하면 된다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 처음엔 딕셔너리를 생각했다. 각각 인덱스에 `중요도`를 붙혀 정렬시킨 뒤 해당 `중요도`의 값을 가진 키의 인덱스를 출력시키려고 했다.
- 구현이 너무 복잡할 것 같아 방향을 바꾸어 인덱스를 가지는 배열을 하나 만들고, 최댓값을 가진 `max_value`를 만들어 계속 앞에 값부터 비교하면서 해당 값이랑 같을 때 `idx`값을 계속 더해주면서 `인덱스의 원소 값`과 `location`의 값이 같을 경우 출력시키게 해주었다.

</br>


### 내 코드👨🏻‍💻
```swift
func solution(_ priorities: [Int], _ location: Int) -> Int {
    
    var priorities = priorities
    var indexList = [Int]()
    var idx: Int = 0

    for i in 0..<priorities.count {
        indexList.append(i)
    }

    while !priorities.isEmpty {

        guard let max_value = priorities.max() else { return 0 }
        let value = priorities.removeFirst()
        let index_value = indexList.removeFirst()

        if value == max_value {
            idx += 1
            if index_value == location { break }
        } else {
            priorities.append(value)
            indexList.append(index_value)
        }

    }
    return idx
}
```

</br>


### Additional 📂
- 이제는 문제를 보면 어떻게 접근해야겠다 정도는 생각하는데, 어떻게 구현하고, 어떻게 구현해야 시간 복잡도를 더 낮게 나오게 할지 고민해보아야 할 필요가 있다고 생각하게 되었다.
- 많이 부족하지만 계속 노력해보려고 한다 😅
