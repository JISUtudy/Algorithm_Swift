# 92334 → 신고 결과 받기
### 문제 정리📝
1. `유저의 목록(id_list)`을 입력 받는다.
2. `각 유저가 신고한 ID(report)`를 입력 받는다.
3. `신고 횟수(K)`를 입력 받는다.
4. 각 유저는 한 유저를 `한번만` 신고할 수 있고, 추가적으로 신고할 경우 `1회`로 판정받는다.
5. `신고 당한 유저`가 `K`번 이상 누적이 되었을 경우 메일이 가며, `해당 유저를 신고한 유저`에게도 메일이 간다.
6. 각 유저별로 `받는 메일의 수`를 출력한다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- id_list의 각 값을 키로 하는 `딕셔너리`를 만들어 초기화해준다.
- report로 유저별 신고당한 정보를 구하되, `동일 중복 신고`를 방지해준다.
```
reportInfo[reported]?.insert(reporter)
```
- 이용이 정지된 유저를 구하고, 유저별 받을 결과 메일 수 `answer`을 리턴한다.

</br>

### 내 코드👨🏻‍💻

```swift
import Foundation

func solution(_ id_list:[String], _ report:[String], _ k:Int) -> [Int] { 
    var reportInfo = [String: Set<String>]()     
    var user = [String]()                        
    var answer: [Int] = Array(repeating: 0, count: id_list.count)  
    
    id_list.forEach {
        reportInfo[$0] = []
    }
    
    report.map { $0.split(separator: " ") }.forEach {
        let (reporter,reported) = (String($0[0]),String($0[1]))
        reportInfo[reported]?.insert(reporter)   
    }
    
    reportInfo.forEach {
        if $0.value.count >= k {
            user.append($0.key)
        }
    }
    
    user.forEach {
        reportInfo[$0]!.forEach {
            answer[id_list.firstIndex(of: $0)!] += 1
        }
    }
    
    return answer
}
```

### Additional 📂
- 파이썬에서는 set을 통해 중복 제거를 한 후 풀었는데 파이썬에서 한 것처럼 그대로 구현하지 못해 아쉽다.