# 42583 → 다리를 지나는 트럭
### 문제 정리📝
1. 다리에 트럭이 최대 올라갈 수 있는 `bridge_length`를 입력받는다.
2. 다리가 견딜 수 있는 무게 `weight`를 입력받는다. 
> 단, 다리에 완전히 오르지 않은 트럭의 무게는 무시한다.
3. 트럭 별 무게 `truck_weights`를 입력받는다.
4. 모든 트럭이 다리를 건너려면 `최소 몇 초`가 걸리는지 return 하도록 solution 함수를 출력한다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 다리를 건너기 위해 time을 1초씩 추가해주고, 맨 앞의 인덱스를 remove한다.
- `현재 무게`와 `다리가 견딜 수 있는 무게`를 `비교`하여 넘으면 trucks.removeFirst()을 bridgeWeight에 넣어주고 넘지않으면 트럭이 지나갈 수 있도록 한다.

</br>

### 내 코드👨🏻‍💻
```swift
func solution(_ bridge_length:Int, _ weight:Int, _ truck_weights:[Int]) -> Int {
    var bridge = Array(repeating: 0, count: bridge_length)
    var trucks = truck_weights
    var time = 0
    var bridgeWeight = 0

    while !bridge.isEmpty {
        time += 1
        bridgeWeight -= bridge.removeFirst()

        if let t = trucks.first {
            if t + bridgeWeight <= weight {
                bridgeWeight += trucks.removeFirst()
                bridge.append(t)
            } else {
                bridge.append(0)
            }
        }
    }
    return time
}
```

</br>

### Additional 📂
- 할 수 있을 것 같으면서도 구현하는게 아직까지도 조금 어려운 것 같다.
- 수도코드를 적어보면서 생각한 방법을 코드로 옮기는 작업을 더 연습해봐야할 것 같다.

