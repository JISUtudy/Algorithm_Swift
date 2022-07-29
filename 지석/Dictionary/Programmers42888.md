# 42888 → 오픈채팅방
### 문제 정리📝
1. 한 오픈채팅방에 `유저들이 들어온 기록(record)`을 할당 받는다.
2. 해당 기록에는 `Enter/Leave, uid, nickname`으로 구성이 되어있다.
3. `Enter`는 "님이 들어왔습니다."로 `Leave`는 "님이 나갔습니다."로 기록이 된다.
4. `Change`는 해당 `uid`를 가진 `nickname`을 새롭게 바꿔준다. 닉네임을 바꾸는 조건은 하나가 더 있다. 채팅방을 나갔다가 닉네임을 바꾸고 다시 들어오면 그 전의 기록도 새로운 닉네임으로 바뀐다.(단, uid는 바뀌지 않는다.)
5. 해당 기록들을 이용해 아래와 같은 형태로 반환해주면 된다.
```
• record ▾
["Enter uid1234 Muzi", "Enter uid4567 Prodo","Leave uid1234","Enter uid1234 Prodo","Change uid4567 Ryan"]

• result ▾
["Prodo님이 들어왔습니다.", "Ryan님이 들어왔습니다.", "Prodo님이 나갔습니다.", "Prodo님이 들어왔습니다."]
```
</br>

## 접근🚶🏻
### 나의 생각 ▾
* 문제를 보고 `자료구조`를 이용한 `구현`문제라고 생각했다.

* 구성은 다음과 같다.

    * `uid(key)`와 `nickname(value)`로 구성된 `Dictionary`

    * `uid` + `Enter(님이 들어왔습니다.)` or `Leave(님이 나갔습니다.)`로 구성된 (String, String) 타입의 배열

    * user_record[0] = "uid1234님이 들어왔습니다"</br>
      user_record[1] = "uid1234님이 나갔습니다."

* 위와 같은 구조로 바꿔준뒤 `Dictionary[uid]`를 통해 `uid`에 맞는 `nickname`을 바꿔주면서 뒤에 글귀를 같이 붙여주는 `새로운 String 타입의 배열`을 반환해주면 된다고 생각했다.

</br>

### 내 코드👨🏻‍💻
```swift
func checkStatus(_ info: [String]) {
    switch info[0] {
    case "Enter":
        saveRecord(info[0], info[1], info[2])
        
    case "Leave":
        saveRecord(info[0], info[1], nil)
        
    default:
        user_dict[info[1]] = info[2]
    }
}

func saveRecord(_ status: String, _ uid: String, _ nickname: String?) {
    var status_str: String = ""
    switch status {
    case "Enter":
        status_str = "님이 들어왔습니다."
        if user_dict[uid] != nil && user_dict[uid] != nickname {
            changeNickname(uid, nickname)
        }
        
    default:
        status_str = "님이 나갔습니다."
    }

    result.append((uid, status_str))

    guard (user_dict[uid] != nil) else {
        user_dict.updateValue(nickname ?? "", forKey: uid)
        return
    }
}

var user_dict = [String: String]()
var result = [(String, String)]()

func solution(_ record:[String]) -> [String] {
    var ans = [String]()

    for rcd in record {
        let info = rcd.split(separator: " ").map { String($0) }
        checkStatus(info)
    }
    
    for i in 0..<result.count {
        ans.append("\(String(describing: user_dict[result[i].0]!))\(result[i].1)")
    }
    
    return ans
}
```

* `checkStatus`

    * 앞에 붙어있는 상태(Etner, Leave, Change)를 구분하여, 상태에 맞는 함수로 할당해주는 함수이다.

* `saveRecord`

    * `Result(String, String)`배열에 `uid`, `Enter or Leave` 형태로 넣어주는데, 만약 참여한적 있던 `uid`라면 `nickname`을 바꿔서 들어온 것으로 간주하고 해당 `Dictionary`의 `uid`가 `Key`인 `Value(nickname)`를 갱신시켜준다.
    
    * 참여한적이 없는 `uid`라면 바로 저장을 해준다.

</br>

### 다른 사람 풀이👨🏻‍💻
```swift
func solution(_ record:[String]) -> [String] {
    let actions = ["Enter":"님이 들어왔습니다.", "Leave":"님이 나갔습니다."]
    var a = [String:String]()

    record.forEach {
    let separated = $0.components(separatedBy: " ")
    if separated.count > 2 {
        a[separated[1]] = separated[2]
    }
}

return record.filter { !$0.contains("Change") }.map { (value:String) -> String in
        let separated = value.components(separatedBy: " ")
        let newString = a[separated[1]]! + actions[separated[0]]!
        return newString
}
}
```

- `Enter/Leave`를 `님이 들어왔습니다./님이 나갔습니다.` 형태로 키값 형태로 할당해준다.

- 기록을 String형 배열로 쪼갠 뒤, leave일 경우를 제외한 나머지 경우 `uid:nickname` 구조로 `a(Dictionary)`에 할당 시켜준다.

- 고차함수인 `filter`를 통해 기록 중 `Change`가 있다면 해당 기록의 `uid`인 `nickname`을 새롭게 변경시켜주며, 새로운 String으로 바꾸어 반환해준다.

</br></br>

### Additional 📂
- 문제를 풀면서 `Enter, Leave`를 처리하는 부분도 `Dictionary`로 처리해서 구현했다면 더 간결한 구현이 나오지 않았을까 하는 생각이 들었다.

- 다른 사람들의 코드를 참고하다보면 문제를 푼것에 중점을 두던 내가 점점 구현은 물론이고, 더 간결하고 효율적인 코드를 지향하게 된다. 위의 코드만 봐도 정말 대단한 구성이다..👍

- 해당 문제를 풀어보면서 더 효율적인 구현을 위해 노력해야겠다고 다짐하게 되었다.