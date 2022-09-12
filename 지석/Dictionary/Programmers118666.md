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
- 문제를 읽으면서 `Dictionary`를 이용해 구현해야겠다는 생각을 했다. 또한 질문에 대한 정도 점수를 구분해줄 함수를 하나 구현해주면 편하게 구현할 수 있을 것이라고 생각했다. 이 후 `Dictionary`에 해당하는 값을 `조건`을 걸어 `이상(>=)` 조건일 경우에 따른 `String`을 각각 더해 반환해주면 된다고 생각했다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func inputScore_Dict(_ score: Int) -> Int {
    switch score {
    case 1, 7: return 3
    case 2, 6: return 2
    case 3, 5: return 1
    default: return 0
    }
}

func update_Dict(_ dict: inout [Character:Int], _ servey: [String], _ scores: [Int]) {
    for i in 0..<servey.count {
        let type = servey[i].map { Character(extendedGraphemeClusterLiteral: $0) }
        let score = scores[i]
        
        if score < 4 {
            dict[type[0]]! += inputScore_Dict(score)
        }
        else {
            dict[type[1]]! += inputScore_Dict(score)
        }
    }
}


func checkMostScore(_ dict: [Character:Int]) -> String {
    let RT = dict["R"]! >= dict["T"]! ? "R" : "T"
    let CF = dict["C"]! >= dict["F"]! ? "C" : "F"
    let JM = dict["J"]! >= dict["M"]! ? "J" : "M"
    let AN = dict["A"]! >= dict["N"]! ? "A" : "N"
    return RT + CF + JM + AN
}

func solution(_ survey:[String], _ choices:[Int]) -> String {
    var mbti: [Character:Int] = [ "R": 0, "T": 0,
                                   "C": 0, "F": 0,
                                   "J": 0, "M": 0,
                                   "A": 0, "N": 0 ]
    update_Dict(&mbti, survey, choices)
    return checkMostScore(mbti)
}
```

</br></br>

### Additional 📂
- `Dictionary`를 이용하는 문제는 항상 애를 먹었던 것 같다. 이번 문제는 `Dictionary`에 대한 이해도도 요구하겠지만 나의 구현력이 어느 정도인지가 더 중요했던 것 같다. `Dictionary`에 `Value`을 이용해 어떻게 해당 성격이 나오게 할지에 대해 많은 고민을 했던 것 같다. 

- 다른 분들의 구현도 보면서 많이 배운 문제였다. 하지만 어려운건 매 항상인듯 하다..🥲