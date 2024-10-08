### 1946번: 신입 사원

문제 사이트 : [바로가기](https://www.acmicpc.net/problem/1946)

**문제 조건**
- 1차 서류 심사와 2차 면접 시험의 등수를 알려준다.
- A 지원자와 B 지원자의 성적에서 B 지원자가 A 지원자보다 모두 성적이 떨어지면 선발되지 않는다.  
**(즉, B지원자가 선발되려면 A 지원자보다 서류 또는 면접 등수가 높아야 한다)**

**출력**  
- 선발될 수 있는 최대 인원을 출력

### 풀이
1. 테스트 케이스에서 N이 최대 100,000까지 입력받으므로 이중 반복문을 사용하면은 _시간초과_ 발생
2. 우선적으로 서류 심사를 기준으로 오름차순으로 정렬  
**본 코드에서는 `priority_queue`를 사용**
3. `priority_queue`로 오름차순으로 정렬하므로 top 값의 서류심사 등수는 1등이므로 무조건적으로 신입사원은 1명이 뽑힌다.  
_(적어도 하나의 시험에서 1등은 다른 지원자들보다 등수가 높은 것 : `ans = 1`)_
4. `tmp` 값에 현재 등수의 면접 등수(`second`) 값을 저장한다. **현재 등수의 면접 등수가 tmp에 저장된 면접 등수보다 높으면** 신입사원으로 선발 가능 => `ans++`    
_(왜냐하면, 서류 심사로는 등수가 낮지만, 면접 등수로는 높은 것이므로)_
5. `tmp` 값과 해당 등수의 면접 등수를 비교하여 등수가 더 높다면 `tmp`값에 면접 등수를 갱신한다.
6. `priority_queue`가 비어있을 때 까지 반복한 후에, `ans`를 출력 

### 핵심 코드
```
pair<int, int> p;
int ans = 1;
int tmp = pq.top().second;
while(!pq.empty()) {
    p = pq.top(); pq.pop();
    if(p.second < tmp) {
        tmp = p.second;
        ans++;
    }
}
cout << ans << "\n";
```
- `priority_queue`의 `top`에 저장된 값을 `p`에 저장하기 위해 `pair` 선언
- 최소 1명은 신입사원으로 뽑히므로 `ans` 값은 1로 저장
- `tmp` 값에 서류 심사 1등의 `second`(면접 등수)를 저장
- 큐가 빌 때까지 반복하며, `p.second`와 `tmp` 값을 비교  
(`p.second`가 더 등수가 높다면 `tmp` 값에 갱신 후, `ans++`)
- 최종적으로 `ans`를 출력하면 최대로 뽑힐 수 있는 신입사원 수