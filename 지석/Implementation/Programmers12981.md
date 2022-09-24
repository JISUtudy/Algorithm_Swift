# 12981 → 영어 끝말잇기
### 문제 정리📝
1. `1~n`번까지 번호가 붙어있는 `n`명의 사람이 영어 끝말잇기를 한다.
2. 1번부터 번호 순서대로 단어를 말하는데 아래와 같은 규칙이 지켜져야한다.
3. 아래 규칙이 반영되지 않았을 경우 해당 사람의 `번호, 차례`를 `[Int]` 타입으로 반환한다.

```
 • 이전 사람의 단어의 끝글자로 시작하는 단어를 말해야한다.
 • 이전에 등장했던 단어는 제외하고 말해야한다.
 • 한 글자인 단어는 인정되지 않는다.
```

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 지문을 읽으면서 `Dictionary`로 구현과 새로운 `[String]` 변수를 만들어 조건을 만족할 때 마다 넣어주며 해당 배열의 원소 값이 포함되어있는지 여부를 같이 확인하는 방법이다.

- 첫 번째 방법이 더 깔끔한 구현이 될 것 같으나 쉽게 구현하기 위해 두 번째 방법으로 구현하는게 좋다고 생각했다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func check_FirstAndLast(_ prev: String, _ current: String) -> Bool {
    let prev_LastWord = prev.map { String($0) }.last
    let first_CurrentWord = current.map { String($0) }.first
    guard prev_LastWord != first_CurrentWord else { return false }
    return true
}

func check_ContainsArray(_ wordList: [String], _ target: String) -> Bool {
    guard wordList.contains(target) == true else { return false }
    return true
}

func calculate_IncorrectIndex(_ total: Int, _ index: Int) -> [Int] {
    var result = [Int]()
    result.append(index % total + 1)
    result.append(index / total + 1)
    return result
}

func solution(_ n:Int, _ words:[String]) -> [Int] {
    var correctWords = [String]()
    correctWords.append(words[0])

    for i in 1..<words.count {
        if words[i].count < 2 { continue }

        guard check_FirstAndLast(words[i-1], words[i]) == false else {
            return calculate_IncorrectIndex(n, i)
        }
        guard check_ContainsArray(correctWords, words[i]) == false else {
            return calculate_IncorrectIndex(n, i)
        }
        correctWords.append(words[i])
    }
    return [0, 0]
}
```

</br></br>

### Additional 📂
- 문제를 푸는 과정에서 `correctWords.append(words[i])`를 빼먹어서 계속 19,20번 문제에서 실패가 떴었다. 뭐가 문제인지 몰라 한참 해매다가 처음부터 다시 생각해보면서 문제를 찾을 수 있었다.

- 앞으로 구현을 할 때 어떤 걸 구현해야할지 미리 적어두면서 구현했는지 체크를 하면서 풀어나가야겠다고 생각했다. 나름 재밌는 문제였다.