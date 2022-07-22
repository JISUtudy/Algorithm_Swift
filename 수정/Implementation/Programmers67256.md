# 60057 → 문자열 압축
### 문제 정리📝
1. `순서대로 누를 번호가 담긴 배열` numbers와 `왼손잡이인지 오른손잡이인 지를 나타내는 문자열` hand가 주어진다. 
2. 맨 처음 `왼손` 엄지손가락은 `*` 키패드에 `오른손` 엄지손가락은 `#` 키패드 위치에서 `시작`한다.
> 엄지손가락 규칙  
엄지는 `상하좌우 4가지 방향`으로만 이동이 가능하며, 키패드의 이동 `한 칸은 거리 1`을 의미한다.  
👍🏻 `1,4,7`을 입력할 때는 `왼손 엄지손가락`을 사용한다.  
👍🏻 `3,6,9`를 입력할 때는 `오른손 엄지손가락`을 사용한다.  
가운데 열 4개의 숫자 `2, 5, 8, 0`을 입력할 때는, 두 엄지손가락의 현재 키패드의 위치에서 `더 가까운 엄지손가락`을 사용한다.  
⚠️ 만약 두 엄지손가락의 거리가 같다면, 오른손잡이는 오른손 엄지손가락, 왼손잡이는 왼손 엄지손가락을 사용한다.
3. 각 번호를 누른 엄지손가락이 왼손인 지 오른손인 지를 나타내는 `연속된 문자열 형태로 return` 한다.

</br>

## 접근🚶🏻
### 나의 생각 ▾

- s로 나눌 수 있는 최대의 길이는 s길이의 반이라고 생각해 `for i in 1 ... s.count / 2` 1부터 반으로 나눈 길이 만큼을 for문으로 반복해주었다.
- `prefix`를 이용하여 문자열 앞 2글자를 잘라 배열에 넣어줬고 마지막 남은 글자는 붙여줬다.
- 반복문을 통해 이전 값과 같다면 cnt를 증가시켜주고, 작다면 숫자를 넣었다.
- 또한 글자가 1개일 경우 1을 반환해주었다.

- 문제 그대로 구현할 수 있었다.
- `1,4,7`은 무조건 `left`이고 `3,6,9`는 무조건 `right`라는 것을 해주기 위해 `tapHand`라는 변수를 통해 left, right를 정할 수 있었다.
- 키패드의 마지막 `*`과 `0`과 `#`은 `10,11,12`라는 숫자로 생각했고 그것들을 `leftHand` 변수와 `rightHand` 변수, `number`이라는 변수에 각각 넣어주었다.
- 나머지 `2,5,8,0`의 숫자들 중 손의 위치가 가까운 쪽을 선택해줘야 했는데, 이것은 `왼쪽 손과 눌러야 하는 수의 거리와 오른쪽 손과 눌러야하는 수의 거리를 비교`해 줌으로써 구할 수 있었다.
```
현재 손의 위치 - 왼쪽 손 시작점 / 3 + 현재 손의 위치 - 왼쪽 손 시작점 % 3을 통해서 현재 손의 위치에서 눌러야하는 숫자의 거리를 구할 수 있다. 단, 절대값으로 구해준다.
ex) 
왼쪽 손의 위치 1, 오른쪽 손의 위치 9, 눌러야 하는 숫자 8
왼쪽의 거리는 (1-10/3)+(1-10%3) = 3
오른쪽의 거리는 (9-12/3)+(9-12%3) = 1
따라서 가까운 오른쪽 손으로 이용해 8번을 누를 수 있다.
``` 

</br>

### 내 코드👨🏻‍💻
```swift
func solution(_ numbers:[Int], _ hand:String) -> String {
  
  var result = ""
  var leftHand = 10
  var rightHand = 12
  var tapHand = ""
  
  for i in numbers {
    let number = i == 0 ? 11 : i 

    if number == 1 || number == 4 || number == 7 {
      tapHand = "left"
    } else if number == 3 || number == 6 || number == 9 {
      tapHand = "right"
    } else {
      let leftDistance = abs(number - leftHand) / 3 + abs(number - leftHand) % 3
      let rightDistance = abs(number - rightHand) / 3 + abs(number - rightHand) % 3
      if leftDistance == rightDistance { 
        tapHand = hand == "left" ? "left" : "right"
      } else {  
        tapHand = leftDistance < rightDistance ? "left" : "right"
      }
    }
    
    if tapHand == "left" {
      result.append("L")
      leftHand = number
    } else {
      result.append("R")
      rightHand = number
    }
  }
  return result
}
```

</br>

### Additional 📂
- 쉬운 방법으로 접근했을 때 풀기 쉬운 문제였다.
- 재미있는 문제였던 것 같다.
