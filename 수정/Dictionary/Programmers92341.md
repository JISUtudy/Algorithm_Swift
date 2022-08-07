# 92341 → 주차 요금 계산
### 문제 정리📝
1. 주차 요금을 나타내는 정수 배열 fees, 자동차의 입/출차 내역을 나타내는 문자열 배열 records가 주어진다.
> fees의 길이 = 4, 1 ≤ records의 길이 ≤ 1,000
2. 주차장의 요금표와 차량이 들어오고(입차) 나간(출차) 기록이 주어졌을 때, 차량별로 주차 요금을 계산하려고 한다.
```
ex) 
- 요금표   
기본 시간(분)	기본 요금(원)	단위 시간(분)	단위 요금(원)
180	        5000	    10	        600

- 입출차 기록
시각(시:분)	차량 번호	 내역
05:34	    5961	 입차
06:00	    0000	 입차
06:34	    0000	 출차
07:59	    5961	 출차
07:59	    0148	 입차
18:59	    0000	 입차
19:09	    0148	 출차
22:59	    5961	 입차
23:00	    5961	 출차

- 자동차별 주차 요금
차량 번호   누적 주차 시간(분)  주차 요금(원)
0000	34 + 300 = 334	5000 + ⌈(334 - 180) / 10⌉ x 600 = 14600
0148	670	5000 +⌈(670 - 180) / 10⌉x 600 = 34400
5961	145 + 1 = 146	5000
```
> - 어떤 차량이 입차된 후에 출차된 내역이 없다면, 23:59에 출차된 것으로 간주한다.
> - 0000번 차량은 18:59에 입차된 이후, 출차된 내역이 없기때문에, 23:59에 출차된 것으로 간주한다.
> - 00:00부터 23:59까지의 입/출차 내역을 바탕으로 차량별 누적 주차 시간을 계산하여 요금을 일괄로 정산한다.
> - 누적 주차 시간이 기본 시간이하라면, 기본 요금을 청구하고, 누적 주차 시간이 기본 시간을 초과하면, 기본 요금에 더해서, 초과한 시간에 대해서 단위 시간 마다 단위 요금을 청구한다.
> - 초과한 시간이 단위 시간으로 나누어 떨어지지 않으면, 올림한다.  
⌈a⌉ : a보다 작지 않은 최소의 정수를 의미합니다. 즉, 올림을 의미함

</br>

## 접근🚶🏻
### 나의 생각 ▾
- 해시 테이블은 차번호 : [입/출차 기록]으로 구성하고, 입출차 시간은 분으로 변환하여 Int로 저장한다.
- 각 차 번호마다 구한 입출차 기록을 이용해 주차 시간을 계산한다. 만약, 입출차 기록의 개수가 홀수라면 마지막 출차 기록이 없는 것이므로 23:59를 추가해준다.
- 주차 시간을 이용해 비용을 구하는데, 주차 시간에서 기본 시간을 뺀 후 단위 시간에 따른 요금을 계산하여 구해준다.
- 이때 요금은 올림을 해야하므로 ceil 메서드를 이용해준다.
- 차 번호를 기준으로 오름차순 정렬한다.
</br>

### 내 코드👨🏻‍💻

```swift
import Foundation

func strToMin(_ str: String) -> Int {
    let time = str.split { $0 == ":" }.map { Int(String($0))! }
    return time[0] * 60 + time[1]
}

func solution(_ fees:[Int], _ records:[String]) -> [Int] {
    var result: [Int] = []
    
    let lastTime = strToMin("23:59")
    var cars: [String: [Int]] = [:]
    
    for record in records {
        let record = record.components(separatedBy: " ")
        
        let min = strToMin(record[0])
        let number = record[1]
        
        if let _ = cars[number] {
            cars[number]?.append(min)
        } else {
            cars[number] = [min]
        }
    }
    
    cars.forEach {
        let key = $0.key
        
        if $0.value.count % 2 != 0 {
            cars[key]?.append(lastTime)
        }
        
        var minSum = 0, minNums = cars[key]!
        for i in 0..<minNums.count {
            if i % 2 != 0 {
                minSum += (minNums[i] - minNums[i-1] )
            }
        }
        
        var cost = fees[1]
        if minSum > fees[0] {
            cost = cost + (Int(ceil(Double(minSum - fees[0]) / Double(fees[2]))) * fees[3])
        }

        cars[key] = [cost]    
    }
    
    cars.keys.sorted().forEach {
        result.append(cars[$0]![0])
    }
    
    return result
}
```

### Additional 📂
- 해시함수를 이용하여 푸는 구현문제였는데, 시간이 다소 부족하여 내가 생각했던 구현방법으로 푼 다른 분의 코드를 참고하여 해결할 수 있었다.
- 다음번에 다시 한번 더 풀어봐야겠다.