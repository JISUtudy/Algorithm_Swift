# 60057 → 문자열 압축
### 문제 정리📝
1. 압축할 문자열 s가 매개변수로 주어진다.
> s의 길이는 1 이상 1,000 이하, s는 소문자로만 이루어져 있다.
```
ex) 문자열 압축하는 방법
• s = "aabbaccc" → "2a2ba3c"(문자가 반복되지 않아 한번만 나타난 경우 1은 생략함)
• s = "ababcdcdababcdcd" → 1개: 전혀 압축되지 않음, 2개: "2ab2cd2ab2cd", 8개: 2ababcdcd 8개가 가장 짧게 압축하여 표현가능
• s = "abcabcdede" → 2개: "abcabc2de", 3개: "2abcdede" 3개 단위가 가장 짧게 압축할 수 있는 방법이며, 마지막 남는 문자열은 그대로 붙여주면 된다.
```
3. 위에 방법으로 1개 이상 단위로 문자열을 잘라 압축하여 표현한 문자열 중 가장 짧은 것의 길이를 return 해준다.


</br>

## 접근🚶🏻
### 나의 생각 ▾
- s로 나눌 수 있는 최대의 길이는 s길이의 반이라고 생각해 `for i in 1 ... s.count / 2` 1부터 반으로 나눈 길이 만큼을 for문으로 반복해주었다.
- `prefix`를 이용하여 문자열 앞 2글자를 잘라 배열에 넣어줬고 마지막 남은 글자는 붙여줬다.
- 반복문을 통해 이전 값과 같다면 cnt를 증가시켜주고, 작다면 숫자를 넣었다.
- 또한 글자가 1개일 경우 1을 반환해주었다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ s:String) -> Int {
    
  var result = s
  if s.count == 1 {
      return 1
  }
  for i in 1 ... s.count / 2 {
    var s = s
    var splitS:Array<String> = []
    
    while !s.isEmpty {
      let a = String(s.prefix(i))
      splitS.append(a)
      if s.count < i {
        s.removeAll()
      } else {
        s.removeFirst(i)
      }    
    }
    
    var cnt = 1
    var prev = ""
    var word = ""
      
    for j in 0 ..< splitS.count {
      if prev == "" {
        prev = splitS[0]
      } else {
        if prev == splitS[j] {
          cnt += 1
        } else {
          if cnt == 1 {
            word.append("\(prev)")
          } else {
            word.append("\(cnt)\(prev)")
          }
          prev = splitS[j]
          cnt = 1
        }
      }
    }
    if cnt == 1 {
      word.append("\(prev)")
    } else {
      word.append("\(cnt)\(prev)")    
    }
    if word.count < result.count {
      result = word
    }
  }
  return result.count
}
```

</br>

### Additional 📂
- 몰랐던 문법들이 있어서 혼자 풀기에는 어려웠던 문제였다.
- 혼자 최대한 풀어보고 다른 사람들의 코드를 참고하였는데, 다음부터는 참고하지 않고 풀어보고 싶다.
- 아직 문자열 관련 문제가 많이 약한 것 같다.
