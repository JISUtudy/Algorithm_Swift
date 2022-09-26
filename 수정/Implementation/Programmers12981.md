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
- 튜플형식으로 구현된 리스트형을 반환하기 위해 enumerated를 사용했다.
- 문제 그대로, 이전에 등장했던 단어인지, 끝말잇기가 성립되지 않는지를 체크해서 풀 수 있었다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ n:Int, _ words:[String]) -> [Int] {
    var result = [String]()
    for (idx, word) in words.enumerated() {
        if result.contains(word) {
            return [idx%n + 1, idx/n + 1]
        }
        if !result.isEmpty {
            if result.last!.last! != word.first! {
                return [idx%n + 1, idx/n + 1]
            }
        }
        result.append(word)
    }
    return [0, 0]
}
```

</br>

### Additional 📂
- 재미있는 문제였고 좀 더 간단하게 푸는 방법도 있을 것 같다.