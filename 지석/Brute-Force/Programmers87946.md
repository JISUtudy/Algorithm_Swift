# 87946 → 피로도
### 문제 정리📝
1. 던전들이 주어지는데, 각 던전은 `최소 필요 피로도` + `소모 피로도`의 정보를 제공한다.
2. 각 던전의 정보에서 `최소 필요 피로도`보다 높아야 해당 던전을 탐험할 수 있으며, 탐험을 마친 뒤 `현재 피로도`에서 `소모 피로도`의 값이 감소한다.
3. 하루에 한 번씩 탐험할 수 있는 던전이 여러 개가 있을 때, 한 유저가 여러 던전들을 최대한 많이 탐험하려고 할 때, 탐험할 수 있는 `최대 탐험 횟수`를 반환해준다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 처음엔 막연하게 `최소 필요 피로도`와 `소모 피로도`를 정렬들을 통해 들어가게 하려고 했으나, 순차적으로 가는 것이 아닌 모든 경우를 따져야 최대한의 값을 구할 수 있다고 생각이 들었다. `완전 탐색`을 생각하던 중 `제한 사항`에서 `던전의 개수 범위`가 `1이상 8이하`라는 부분에서 `완전 탐색`인 것을 직감했고, 순열을 통해 나열하여 순차적으로 방문하거나, 조합을 통해 여러 경우들을 돌려보는 경우가 있을 것 같다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ k:Int, _ dungeons:[[Int]]) -> Int {
    var ans: Int = 0
    
    func visited(_ plans: [Int]) {
        guard dungeons.count != plans.count else {
            var visitCount: Int = 0
            var visit_k = k
            
            for plan in plans {
                if dungeons[plan][0] <= visit_k {
                    visit_k -= dungeons[plan][1]
                    visitCount += 1
                }
            }
            ans = max(ans, visitCount)
            return
        }
        
        for i in 0..<dungeons.count {
            if !plans.contains(i) { visited(plans + [i]) }
        }
    }
    for i in 0..<dungeons.count { visited([i]) }
    return ans
}
```

- `visited`함수는 재귀적으로 호출하기 위한 하나의 함수이며, 해당 함수 내에서 `순열`을 구현하기 위해 아래와 같이 구현하게 된다.

</br>

```swift
for i in 0..<dungeons.count {
    if !plans.contains(i) { visited(plans + [i]) }
}
```
- 해당 코드는 `plans`라는 `[Int]`타입의 배열로써, `인덱스`를 의미하는 `i`가 포함되어 있지 않다면 포함 시켜줄 수 있도록 진행하였다.

</br>

```swift
for plan in plans {
    if dungeons[plan][0] <= visit_k {
        visit_k -= dungeons[plan][1]    // 탐험을 했으니 피로도 감소
        visitCount += 1                 // 탐험을 했으니 카운팅
    }
}
ans = max(ans, visitCount)              // 재귀적으로 불리는 단계에서 매번 최대 값을 저장
```
- 모두 포함이 되었다면 `max`를 통해 가장 최대의 값을 추출하면 된다. 이 과정에선 아래와 같은 코드로 구현이 가능하다.


</br></br>

### Additional 📂
- 최근 풀었던 알고리즘 문제 중 가장 어려웠던 것 같다. 파이썬으로 풀었을 경우에는 지원하는 라이브러리들이 있어서 쉽게 구현이 가능했을 것으로 보였다..

- 순열을 구현하는 단계에선 구현 방법이 떠오르지 않아 다른 분들의 코드를 참고해 풀었다.. 이런 문제들도 충분한 시간을 통해 혼자 풀 수 있을 때까지 열심히 공부해야겠다.