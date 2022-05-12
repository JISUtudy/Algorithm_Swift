# 42583 → 다리를 지나는 트럭
### 문제 정리📝
1. `다리의 길이`를 입력받는다.
2. `다리가 견딜 수 있는 무게`를 입력받는다.
3. 지나가야하는 각각의 `트럭 무게`를 입력받는다.
4. 모든 트럭이 해당 다리를 건너가야 할 경우, 최소 몇 초가 걸리는지 출력한다.
> 트럭이 다리 위로 올라가거나 다리를 지날 때 마다 1초가 지나간다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 원소가 움직일 때 마다 1초씩 증가해야하는 조건이라 `while문`에 1초씩 증가하는 코드를 넣어야겠다는 생각이 제일 먼저 들었다.
- 각각의 다리를 지날 때 `현재 다리가 견디고 있는 무게`를 측정해서 `트럭`이 더 지나갈 수 있는지 여부를 판단해야하고, 지나 갈 수 있을 경우 `다리의 길이`의 크기를 가진 배열에 담아주기로 했다.
- `다리의 무게`에 루프를 돌 때마다 `다리의 길이` 배열의 초기 값을 제거와 함께 더해주고, 이 후 **다리를 지날 수 있는 조건**이 성립이 되거나 안될 때 마다 `트럭의 무게 or 0`을 넣어주었다.

</br>


### 내 코드👨🏻‍💻
```swift
func solution(_ bridge_length:Int, _ weight:Int, _ truck_weights:[Int]) -> Int {
    
    var time: Int = 0
    var birdge_weight: Int = 0
    var waitList = truck_weights
    var bridge_step = Array(repeating: 0, count: bridge_length)

    while !bridge_step.isEmpty {
        time += 1
        birdge_weight -= bridge_step.removeFirst()
        
        if let truck = waitList.first {
            if weight - birdge_weight >= truck {
                birdge_weight += waitList.removeFirst()
                bridge_step.append(truck)
            } else { bridge_step.append(0) }
        }
    }
    
    return time
}
```

</br>


### Additional 📂
- 처음에 `waitList.first`를 `gurad`로 옵셔널 바인딩하려다가 `return`을 만나면서 초기값이 없을 경우가 마지막에 생기는 이슈가 있었다.
- 해당 `gurad`를 `if let`으로 바꿔주어 초기값이 있을 경우에만 진행할 수 있도록 구현해주었다.
- 구현하는 부분에서 막히기 시작해서 다른분의 코드를 참고해서 풀었다.. 🥲
- 더 열심히 하는 걸로 😂
