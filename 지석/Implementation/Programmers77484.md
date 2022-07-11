# 77484 → 로또의 최고 순위와 최저 순위
### 문제 정리📝
1. `로또 번호(1차원 배열, Int type)`과 `당첨 번호(1차원 배열, Int type)`이 주어진다.
2. 알 수 없는 번호인 `0`은 당첨 번호가 될 수도 있고, 안될 수도 있다.
3. `로또 번호`가 `당첨 번호`와 일치하는 개수를 토대로 `등수`를 반환해준다.
> 이 때 0이 당첨번호와 일치할 경우와 불일치할 경우 두 개의  값을 오름차순으로 정렬하여 반환한다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 단순하게 `일치하는 숫자`를 카운팅하고, `0`을 카운팅해서 해당 값을 합쳤을 경우 몇등인지와 `일치하는 숫자의 개수`만으로는 몇등을 하는지 체크해주면 될 것으로 보였고, `일치하는 개수`를 넘겨주었을 때 `등수`를 반환해주는 함수를 하나 만들어주면 될것으로 보였다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func Check_rank(_ score: Int) -> Int {
    switch score {
    case 6: return 1
    case 5: return 2
    case 4: return 3
    case 3: return 4
    case 2: return 5
    default: return 6
    }
}

func solution(_ lottos:[Int], _ win_nums:[Int]) -> [Int] {
    var cnt = 0
    var zero_cnt = 0
    var ans = [Int]()

    for number in lottos {
        if win_nums.contains(number) {
            cnt += 1
        }
        if number == 0 {
            zero_cnt += 1
        }
    }
    
    ans.append(Check_rank(cnt+zero_cnt))
    ans.append(Check_rank(cnt))
    ans.sort(by: <)
    
    return ans
}
```

</br>

### 다른 코드👨🏻‍💻
```swift
import Foundation

func solution(_ lottos:[Int], _ win_nums:[Int]) -> [Int] {

    let zeroCount = lottos.filter { $0 == 0}.count
    let winCount: Int = win_nums.filter { lottos.contains($0) }.count


    return [min(7-winCount-zeroCount,6), min(7-winCount,6)]
}
```

- `filter`를 통해 값이 `0, win_nums의 원소` 인지 체크하여, 최고 값인 `6`을 `min`을 통해 반환해주는 구조이다.

- 구현을 하면서 더 간단하고 간결한 방법이 있을 거 같았으나 고차 함수를 다루는 부분이 아직 미숙했었던 탓인지 이런 구현을 생각도 못했다..

</br></br>

### Additional 📂
- 이번 문제를 풀어보면서 `고차 함수`에 대해 공부를 해야겠다는 생각이 들었다.

- 저번에 공부하기론 `고차 함수`가 시간이 오래걸리는 것으로 알고 있었으나 그래도 알고 있으면 더 간결한 구현이 가능할 것으로 보이고, 최대한 효율적인 구현도 가능할 것 같다.