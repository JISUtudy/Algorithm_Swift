# 77884 → 약수의 개수와 덧셈
### 문제 정리📝
1. 두 정수 left와 right가 주어진다. 
2. left부터 right까지의 모든 수들 중에서, 약수의 개수가 짝수인 수는 더하고, 약수의 개수가 홀수인 수는 뺀 수를 출력한다.
</br>

## 접근🚶🏻
### 나의 생각 ▾
- 문제 그대로 구현하면 되는 문제였다.
- 짝수인 수는 더하고 홀수인 수는 빼면서 풀 수 있었다.
</br>

### 내 코드👨🏻‍💻

```swift
def solution(left, right):
  answer = 0

  for i in range(left,right+1):
    numbers = 0
    for j in range(1,i+1) :
      if i % j == 0:
        numbers += 1
    if numbers % 2 == 0 :
      answer += i
    else :
      answer -= i
  return answer
```

### Additional 📂
- 오랜만에 쉬운 문제였다.