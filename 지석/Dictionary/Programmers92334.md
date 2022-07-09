# 92334 → 신고 결과 받기
### 문제 정리📝
1. `유저의 목록(id_list)`을 입력 받는다.
2. `각 유저가 신고한 ID(report)`를 입력 받는다.
3. `신고 횟수(K)`를 입력 받는다.
4. 각 유저는 한 유저를 `한번만` 신고할 수 있고, 추가적으로 신고할 경우 `1회`로 판정받는다.
5. `신고 당한 유저`가 `K`번 이상 누적이 되었을 경우 메일이 가며, `해당 유저를 신고한 유저`에게도 메일이 간다.
6. 각 유저별로 `받는 메일의 수`를 반환해주면 된다.

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 문제의 형식을 보자마자 `Dictionary`가 생각이 났다. 각 유저별로 `신고 당한 누적 횟수`를 카운팅 하는 `Dictionary(get_user)` 하나와 `신고 데이터를 저장`할 `Dictionary(declaration)` 하나를 선언해준다.

- 각 유저의 ID를 `Key`로 가지는 `get_user`의 `Value`가 `K` 이상 일 경우 `결과를 반환하는 하는 딕셔너리(result_count)`에 넣어주면 될 것으로 보였다.

</br>

### 내 코드👨🏻‍💻
```swift
func solution(_ id_list:[String], _ report:[String], _ k:Int) -> [Int] {
    var declaration = [String : Set<String>]()
    var result_count = [String: Int]()
    var get_user = [String: Int]()

    for id in id_list {
        result_count[id] = 0
        get_user[id] = 0
    }

    for dt in report {
        let user = dt.split(separator:" ")
        if var val = declaration[String(user[0])] {
            val.update(with: String(user[1]))
            declaration.updateValue(val, forKey: String(user[0]))
        } else {
            declaration.updateValue(Set(arrayLiteral: String(user[1])), forKey: String(user[0]))
        }
    }

    for (_, value) in declaration {
        for v in value {
            get_user[v]! += 1
        }
    }
    for (key, value) in declaration {
        for (rKey, rValue) in get_user {
            if rValue >= k {
                if value.contains(rKey) {
                    result_count[key]! += 1
                }
            }
        }
    }

    var ans = [Int]()

    for id in id_list {
        ans.append(result_count[id]!)
    }
    return ans
}
```

* 아래에 더 간결하고 획기적인 구현 코드가 있다. 아래에서 살펴보자

</br></br>

### 다른 사람 코드👨🏻‍💻
```swift
func solution(_ id_list:[String], _ report:[String], _ k:Int) -> [Int] {
    var reported: [String: Int] = [:]
    var user: [String: [String]] = [:]

    for r in Set(report) {
        let splited = r.split(separator: " ").map { String($0) }
        user[splited[0]] = (user[splited[0]] ?? []) + [splited[1]]      // splited[0]의 키의 값을 Optional 처리로 ?? Default 값 할당
        reported[splited[1]] = (reported[splited[1]] ?? 0) + 1          // 신고 당한 사람 카운트 진행
    }

    return id_list.map { id in                                          // id 하나씩 접근해주기 위해 map 사용
        return (user[id] ?? []).reduce(0) {                             // id 키를 가진 user의 값을 전부 더해줌
            $0 + ((reported[$1] ?? 0) >= k ? 1 : 0)                     // 현재 원소 값 + 다음 원소가 키인 reported(Dictionary)의 값이 K보다 크면 1을, 작으면 0을 반환
        }
    }
}
```
</br></br>





### Additional 📂
- 푸는 내내 더 간단한 방법과 간결한 구현이 있을 것이라고 생각은 했었으나 좋은 아이디어가 생각나지 않아 그냥 내 스타일대로 구현했다.

- `Swift` 언어 특성상 `Optional` 처리 및 `딕셔너리 구현`에서 조금 애먹었던 것 같다. `Python` 언어는 `defaultdict` 라이브러리를 지원해줘서 금방 풀었던 것 같은데 코딩 테스트를 준비한다면 `Python` 언어가 더 유리할 것 같다..