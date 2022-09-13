# 118666 → 성격 유형 검사하기
### 문제 정리📝
1. `1번~4번 지표`가 있다. 해당 지표는 아래와 같다.
2. 각 지표에는 `질문`이 `7가지`가 있다. 해당 질문도 아래와 같다.
3. 지표는 1~4번, 질문에 따른 점수가 각각 `배열` 형태로 주어진다.
4. 아래 `지표` 및 `질문`을 통해 검사자의 `성격 유형(문자열)`을 반환해주면 된다.
```
• 1번 지표: 라이언형(R), 튜프형(T)
• 2번 지표: 콘형(C), 프로도형(F)
• 3번 지표: 제이지형(J), 무지형(M)
• 4번 지표: 어피치형(A), 네오형(N)

• 매우 비동의 (1)
• 비동의 (2)
• 약간 비동의 (3)
• 모르곘음 (4)
• 약간 동의 (5)
• 동의 (6)
• 매우 동의 (7)
```

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 해당 문제는 `Dictionary`를 이용해 풀 수 있었다.
- survey에 있는 수를 첫번째 글자와 마지막 글자로 나눠주어 choices가 4 미만일 때, 그렇지 않을 때로 구분하여 점수를 매길 수 있었다.
```
예) ["RF"] -> R과 F로
```
- 그런 다음, 자표에 따라 점수가 더 큰 것을 반환하여 구할 수 있었다.
</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ survey:[String], _ choices:[Int]) -> String {
    var dict : [String:Int] = ["R": 0, "T": 0, "C": 0, "F": 0, "J": 0, "M": 0, "A":0, "N": 0]

    for i in 0..<survey.count {
        let first = String(survey[i].first!)
        let last = String(survey[i].last!)

        if choices[i] < 4 {
            dict[first] = dict[first]! - choices[i] + 4
        } else {
            dict[last] = dict[last]! + choices[i] - 4
        }
    }

    let RT = dict["R"]! >= dict["T"]! ? "R" : "T"
    let CF = dict["C"]! >= dict["F"]! ? "C" : "F"
    let JM = dict["J"]! >= dict["M"]! ? "J" : "M"
    let AN = dict["A"]! >= dict["N"]! ? "A" : "N"

    return RT + CF + JM + AN
}
}
```

</br></br>

### Additional 📂
- 오랜만에 다시 알고리즘을 풀어보았다. 그렇기 때문에 이 문제를 푸는데에 다소 오랜 시간이 걸렸던 것 같다.
- 어떻게 구현할지에 대해 생각했지만 바로 구현해내는 것에는 한계가 있었다. 다른 사람들의 풀이도 찾아보면서 내가 생각했던 방법으로 구현해 낼 수 있었다.
- 여전히 알고리즘은 어렵지만, 내가 생각한 방식대로 구현했을 때에는 너무 짜릿하당