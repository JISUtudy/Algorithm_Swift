# 72411 → 메뉴 리뉴얼
### 문제 정리📝
1. 스카피의 레스트랑은 기존 단품 메뉴들을 조합해서 코스요리 형태로 재구성해서 새로운 메뉴를 제공하기로 한다.
2. 코스요리 메뉴는 각 손님들이 주문할 때 `가장 많이 주문한 단품 메뉴들`로 구성하기로 한다. 아래와 예시를 보자

| 손님 번호 | 주문한 단품메뉴 조합 |
| :----------: | :----------: |
| 1번 손님 | A, B, C, F, G |
| 2번 손님 | A, C |
| 3번 손님 | C, D, E |
| 4번 손님 | A, C, D, E |
| 5번 손님 | B, C, F, G |
| 6번 손님 | A, C, D, E, H |

3. 위의 표를 기준으로 코스요리 메뉴를 구성 후보는 아래와 같다.

| 코스 종류 | 메뉴 구성 | 설명 |
| :----------: | :----------: | :----------: |
| 요리 2개 코스 | A, C | 1번, 2번, 4번, 6번 손님으로부터 총 4번 주문됐습니다. |
| 요리 3개 코스 | C, D, E | 3번, 4번, 6번 손님으로부터 총 3번 주문됐습니다. |
| 요리 4개 코스 | B, C, F, G | 1번, 5번 손님으로부터 총 2번 주문됐습니다. |
| 요리 4개 코스 | A, C, D, E | 4번, 6번 손님으로부터 총 2번 주문됐습니다. |

4. 각 손님은 단품메뉴를 2개 이상 주문해야 한다. 이 중 가장 많이 주문된 메뉴가 코스요리 메뉴가 된다.
5. 가장 많이 함께 주문된 메뉴 구성이 여러 개라면, 모두 배열에 담아 `오름차순`으로 `return` 하면 된다.


</br>

## 접근🚶🏻
### 나의 생각 ▾
- 이미 지문에서 `조합`에 관련된 부분이 언급이 되어 `조합`하여 문제를 풀어야된다고 생각을 했다.

- 해당 문제들을 하나씩 담아보며 어떤 메뉴가 가장 많이 호출이 되는지를 알아야되므로, `Dictionary`를 이용해 가장 많이 주문된 메뉴를 알아낼 수 있을 것 같았다.

- 늘 `Python`에선 지원하던 `조합`기능 없이 직접 구현하려니 막막했다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

var combi_orders = [[String]]()
var combi_dict = [String:Int]()

func make_combination(order: [String], pickDish: [String] ,orderCount: Int, currentIndex: Int) {
    
    if orderCount == 0 { combi_orders.append(pickDish) }
    
    else if order.count == currentIndex { return }
    
    else {
        var pickDishs = pickDish
        pickDishs.append(order[currentIndex])
        make_combination(order: order, pickDish: pickDishs, orderCount: orderCount - 1, currentIndex: currentIndex + 1)
        make_combination(order: order, pickDish: pickDish, orderCount: orderCount, currentIndex: currentIndex + 1)
    }
}

func pick_maxCombination(combinations: [[String]]) -> [String] {
    
    for combination in combinations {
        let key = combination.joined()

        if let _ = combi_dict[key] {
            combi_dict[key]! += 1
        } else {
            combi_dict[key] = 1
        }
    }
    
    let best_order = combi_dict.sorted { $0.value > $1.value }.first?.value ?? 1
    return best_order == 1 ? [] : combi_dict.filter { $0.value == best_order }.map { $0.key }
}


func solution(_ orders:[String], _ course:[Int]) -> [String] {
    var result = [String]()
    
    for cur in course {
        combi_orders = []
        combi_dict = [:]
        
        for order in orders {
            make_combination(order: order.map{String($0)}.sorted(), pickDish: [], orderCount: cur, currentIndex: 0)
        }
        result.append(contentsOf: pick_maxCombination(combinations: combi_orders))
    }
    
    return result.sorted()
}
```

- 각각의 함수 기능들을 아래서 살펴보자

</br>

### make_combination
```swift
func make_combination(order: [String], pickDish: [String] ,orderCount: Int, currentIndex: Int) {
    
    if orderCount == 0 { combi_orders.append(pickDish) }
    
    else if order.count == currentIndex { return }
    
    else {
        var pickDishs = pickDish
        pickDishs.append(order[currentIndex])
        make_combination(order: order, pickDish: pickDishs, orderCount: orderCount - 1, currentIndex: currentIndex + 1)
        make_combination(order: order, pickDish: pickDish, orderCount: orderCount, currentIndex: currentIndex + 1)
    }
}
```
- 위 함수는 `조합`을 만드는 함수이다.

- 첫번째 `if`는 담아야할 코스의 개수를 카운팅 하는 것으로 점차 감소하다가 `0`이 되었을 때 전역 변수인 `combi_orders` 배열에 삽입해준다.

- 두번째 `else if`는 메뉴를 하나씩 빼서 조합을 하는데 `마지막 메뉴`일 경우는 더 이상 메뉴를 추가해줄 수 없어서 그대로 반환해준다.

* 세번째는 일반적인 케이스를 담은 부분이다.
    * 기존 선택해 담아놓은 메뉴를 담은 배열의 copy 배열을 만들어, 메뉴들 중 `인덱스`에 맞는 원소를 담아준다.
    * 여기서 재귀 함수 두 개를 넣어준다.
        * 하나는 점점 `orderCount`를 감소시키며, `copy 배열`을 넘겨주는 것
        * 하나는 일반 메뉴를 그대로 가져가며, `currentIndex`의 값만 증가시켜주는 것

</br>

### pick_maxCombination
```swift
func pick_maxCombination(combinations: [[String]]) -> [String] {
    
    for combination in combinations {
        let key = combination.joined()

        if let _ = combi_dict[key] {
            combi_dict[key]! += 1
        } else {
            combi_dict[key] = 1
        }
    }
    
    let best_order = combi_dict.sorted { $0.value > $1.value }.first?.value ?? 1
    return best_order == 1 ? [] : combi_dict.filter { $0.value == best_order }.map { $0.key }
}
```
- 위 함수는 각 메뉴들의 `주문된 횟수`를 `Dictionary`를 통해 `[메뉴 : 주문된 횟수]` 꼴로 정의를 해주며, 해당 `Dictionary`의 값인 `주문된 횟수`가 많은 순으로 정렬을 해준다.

- 만약 가장 많이 주문된 횟수가 1이라면, 코스요리 메뉴의 후보 조건인 `2명이상 주문`에 대한 부분이 성립이 되지 않으므로 `빈 배열`을 반환시켜준다.

- 그 외일 경우는 `가장 많은 주문 횟수`를 가진 메뉴를 가진 `메뉴 이름(key)` 모두를 반환시켜준다.

</br>


### Additional 📂
- 여태까지 풀었던 문제 중 어려웠던 문제에 속하는 것 같다. 막연하게 Level 2여서 가볍게 봤었던 내가 부끄럽다.

- 이 문제를 통해 조합에 대한 부분을 공부할 수 있었으며, 전반적인 구현력을 기를 수 있는 좋은 문제였던 것 같다.