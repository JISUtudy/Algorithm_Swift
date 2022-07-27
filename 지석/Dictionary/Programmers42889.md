# 42889 → 실패율
### 문제 정리📝
1. `스테이지의 개수(N)`와 `플레이어 별 현재 도전중인 스테이지를 담은 배열(stage)`가 주어진다.
2. 해당 스테이지 별 `실패율`을 구해서 실패율이 높은 스테이지부터 `내림차순`으로 `스테이지 번호`를 반환해주면 된다.
3. `실패율`이 같은 스테이지가 있다면 `작은 번호`의 스테이지가 먼저 오도록 한다.
4. 스테이지에 도달한 유저가 없는 경우 해당 스테이지의 실패율은 `0`으로 정의한다.
```
실패율: 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수
ex) N: 5, stages: [2,1,2,6,2,4,3,3] → result: [3,4,2,1,5]
```
</br>

## 접근🚶🏻
### 나의 생각 ▾
- 문제를 보고 `실패율`과 `해당 스테이지 번호`를 이용해 정렬해야하는 문제라 판단하고, `Dictionary`를 이용해 문제를 접근하면 될 것으로 보였다.

- `Dictionary`를 다루는 부분은 크게 막히지 않을 것 같았으나 `실패율`이 같은 스테이지가 존재하면 `작은 번호`의 스테이지부터 먼저 오도록 해야 하므로 해당 부분만 `sorted()`를 통해 정렬해주면 크게 문제 될 것이 없을 것으로 판단했다.

</br>

### 내 코드👨🏻‍💻
```swift
func solution(_ N:Int, _ stages:[Int]) -> [Int] {
    var failDict = [Int:Float]()
    var people = stages.count

    for level in 1...N {
        let failCount = stages.filter { $0 == level }.count
        let value = Float(failCount) / Float(people)
        failDict.updateValue(value, forKey: level)
        people -= failCount
    }
    
    return failDict.sorted(by: <).sorted{ $0.value > $1.value }.map{$0.key}
}
```

</br></br>

### Additional 📂
- 원래는 `while`문을 통해 정렬된 `copy_stage`를 만들어 `.first` 값과 스테이지 값이 같은지 비교하려고 했다. 이렇게 하니 `시간 초과`를 날 정도로 복잡하게 만들어지는 구조와 `실패율`을 구하는 과정이 얼추 맞게 구현을 해서 몇 개가 실패로 떴다.

- 이번 문제를 풀고 다른 사람 풀이를 봤는데 `reduce`를 사용하신 분도 있었다. 고차 함수가 시간을 많이 잡아 먹는것으로 알기에 최대한 지양하려고 했으나 그래도 알고는 있어야하고, 응용할 줄 알아야 된다고 다시 한번 생각하게 해준 문제였다.