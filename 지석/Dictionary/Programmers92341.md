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
* 지문을 읽자 마자 `Dictionary`가 생각이 났다. 차량 번호를 `키`로 설정하고, 시간을 `값`으로 받아 구현하면 될 것으로 보였다.

* 시간 같은 경우에는 `시 * 60 + 분` 형태로 바꾸어 `분 단위`로 계산하면 될 것으로 보였다.

* 요금은 `누적 시간`을 기준으로 요금을 계산하기 때문에 누적 시킴과 동시에 출차가 완료된 차량인지 체크해주는 `Dictionary`와 총 누적 시간을 저장하는 `Dictionary`로 문제를 접근해보기로 했다.

</br>

### 내 코드👨🏻‍💻
```swift
import Foundation

func solution(_ fees:[Int], _ records:[String]) -> [Int] {
    var car_info = [String : Int]()
    var car_result = [Int: Int]()
    var result = [Int]()
    let MAX_TIME = 23 * 60 + 59

    for record in records {
        let data = record.split(separator: " ").map { String($0) }
        let time_data = data[0].split(separator: ":").map{ Int($0)! }
        let time = (time_data[0] * 60) + time_data[1]
        let status = data[2]
        
        switch status {
        case "IN":
            car_info.updateValue(time, forKey: data[1])
        case "OUT":
            if let passTime = car_info[data[1]] {
                let taken_time = time - passTime
                let carNumber = Int(data[1])!
                if let passResult = car_result[carNumber] {
                    car_result[carNumber] = taken_time + passResult
                } else {
                    car_result.updateValue(taken_time, forKey: carNumber)
                }
                car_info.removeValue(forKey: data[1])
            }
        default: break
        }
    }

    if !car_info.isEmpty {
        for (carNumber, takenTime) in car_info {
            if let passResult = car_result[Int(carNumber)!] {
                car_result[Int(carNumber)!] = (MAX_TIME - takenTime) + passResult
            } else {
                car_result[Int(carNumber)!] = MAX_TIME - takenTime
            }
        }
    }
    
    for (_, takeTiem) in car_result.sorted(by: {$0.key < $1.key}) {
        if takeTiem <= fees[0] {
            result.append(fees[1])
        } else {
            let price = Int(ceil(Double((takeTiem - fees[0])) / Double(fees[2]))) * fees[3] + fees[1]
            result.append(price)
        }
    }
    
    return result
}
```

</br>


### Additional 📂
- 더 간결히 정리한다면 가능한 코드이긴 하다. 여유가 생길 때 다시 한번 풀어서 더 간결한 구현을 해보려고 한다.

- 키-값으로 접근을 해야하는 문제에 약했었는데 이번 계기로 조금은 더 배울 수 있었던 것 같다.