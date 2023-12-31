# DeadLock

Deadlock은 "교착 상태"라는 의미로, 프로세스들이 서로가 원하는 자원들을 점거한채로, 다른 프로세스가 가진 자원을 요구하며 Block된 상태를 가리킨다. <br> <br>

예를 들어 첵스초코를 우유에 말아 먹기 위해 나는 첵스 초코를 가지고 있고, 동호는 우유를 가지고 있을 때, <br>
나는 절대 첵스초코를 내려놓지 않으면서 동호에게 우유를 달라고 손 내밀고 있고, <br>
동호는 절대 우유를 내려 놓지 않으면서 나에게 첵스초코를 달라고 손 내밀고 있는 상태로 가만히 기다리는 것이다. <br> <br>

결국 필요한 자원은 똑같은데, 서로에게 양보만을 요구하며 하염없이 기다리는 상황. <br>
안타깝게도 이러한 자원은 첵스초코일 때보다, 하드웨어, 소프트웨어 자원일 때가 더욱 많다. 

<br>


# 1. Deadlock 발생 4가지 조건
단순히 "자신의 것을 내려놓지 않고, 서로 상대의 것을 원한다"라는 말로 표현 가능하지만, <br>
구체적으로 4가지 발생 조건이 있다. 

<br>

1. `Mutual Exclusion - 상호배제` : 한가지 **자원은 한번에 하나의 프로세스만** 사용 가능하다.
2. `No Preemption - 비선점형`: 프로세스는 다른 프로세스에게 **강제로 자원을 빼앗기지 않는다.** 
3. `Hold and Wait - 보유 대기`: 자원을 가진 프로세스가 다른 자원을 기다리는 상황에서, **자신이 보유한 자원을 내려 놓지 않는다.**
4. `Circular Wait - 순환형 대기`: 프로세스들이 원하는 자원들간의 (원형) 사이클이 구성됨. 서로 자원을 요구하는 프로세스들을 이용해 Resource-Allocation Graph를 그리면 사이클이 형성된다.


<br>

**정확히 위 4가지 요소가 모두 만족될 때 Deadlock이 발생할 수도 있다.**

## 2. DeadLock의 처리 방법
DeadLock을 "처리"하는 방법은 4가지가 있다.

<br>

1. `DeadLock Prevention - 예방`: 데드락 발생 가능성을 예방한다. <br> 앞서 설명한 4가지 조건 중 하나라도 예방할 수 있다면, 예방이 가능하다. (현실적으론 어렵)
2. `DeadLock Avoidance - 회피`: **자원을 할당해주기 전에, 미리 할당해줘도 안전한지 확인해서 데드락을 회피한다.** <br> 자원 인스턴스가 하나라면, 그래프를 그려 Cycle 발생 여부를 체크한다. (Resource-Allocation Graph) <br> 여러개라면 뱅커스 알고리즘을 통해 최대 할당량을 미리 조사해보고 할당해준다.
3. `Deadlock Detection and Recovery - 감지와 회복`: **그냥 Deadlock이 발생하게 두고 복구한다.** 자원을 그냥 요구하는 대로 다 할당하고, Deadlock 상황시 복구를 한다. (희생자를 정하는 등의 방법으로)
4. `Deadlock Ignorance - 무시`: 데드락을 무시하는 것이다. **의외로 UNIX나 대부분의 OS가 채택했다.** <br> 결국 Deadlock은 빈번히 발생하는 문제가 아니므로, 그냥 무시하고 문제가 생기면 인간이 알아서 프로세스를 종료하게 한다.

<br>

## 3. DeadLock Prevention
데드락을 예방하기 위해 4가지 조건들 중 하나를 예방한다. <br>
현실적으로 불가능한데, 4가지 조건들을 예방하는 방법을 살펴보자.

### 3.1 `Mutual Exclusion` 예방
`Mutual Exclusion`은 막을 수도 없고, 막으면 안된다. **동시성 문제 때문이다.** <br>
애초에 동시성 문제가 발생하는 이유가 자원을 공유해서이고, 막는 방법도 한번에 한 작업주체만 접근하게 하는건데 <br>
데드락 막겠다고, 자원을 여러 프로세스가 한번에 쓰게 하는 것은 말이 안 된다.

### 3.2 `Hold And Wait`
`Hold And Wait`는 두 가지 방법으로 예방할 수 있다.
1. 애초에 프로세스 시작시 모든 필요한 자원을 미리 할당한다. -> 엄청난 비효율. 쓰지도 않을 자원들 때문에 다른 프로세스가 실행조차 못 된다. 
2. 자원이 필요할 경우 보유 자원을 모두 내려놓고 요청 -> 여러 예방 방법 중 유일하게 조금 유효한 방법 <br> 안 되는 이유는 아래 `No Preemption` 예방에서 설명

### 3.3 `No Preemption`
자원을 어디까지 어떻게 썼는지 기록하기가 어려워서 불가능하다. <br>
프로세스나 스레드는 PCB, TCB 같은 곳에 자신의 "컨텍스트"를 저장하기 때문에, 흐름이 끊겼다가 이어져도, 작업 진행을 이어갈 수 있는 것이다. <br>
하지만 모든 사용 자원들을 기록할 수는 없다. state를 쉽게 저장하고 복원할 수 있는 자원들만 비선점형으로 바꿀 수 있기 때문에, 전체적인 선점형화 어렵다.

### 3.4 `Circular Wait`
자원들에게 사용 순서를 정해주면 `Circular Wait`를 막을 수 있다 된다. <br>
그러니까 우유와 첵스초코를 들어서 그릇에 담는 순서를 정확히 정해두는 것이다. <br>
좋은 방식이지만 비효율적이다.
- Utilization이 저하
- Throughput이 감소
- Starvation 문제가 발생할 수 있음

<br>

전부 순서가 정해져있으니 효율이 떨어진다는 것이다. <br>
위는 짧은 예시여서 그렇지 무조건 `A -> B -> C -> D -> E` 순서를 지켜야 한다고 생각해보자. <br>
다섯 프로세스가 동시에 실행될 수 있더라도 매번 다음 자원을 기다려야 한다.

<br>

## 4. DeadLock Avoidance
Deadlock 자체를 미리 방지한다! <br>
자원에 대한 인스턴스가 하나인 경우, Resource Allocation Graph를 그려본다. <br>
자원과 프로세스들을 노드로 나타내어, 프로세스가 자원을 요청할 경우 화살표로 이은다. <br>
그리고 평생에 한번이라도 요청할 **가능성이** 있다면 점선으로 긋는다. 언젠간 호출할 수도 있다는 것이고, 실제로 요청할 경우에만 실선으로 바뀐다. <br>
이를 Claim edge라고 부른다. <br>
**DeadLock Avoidance에서는 최악의 상황을 상정한다.**
만약 점선이 포함된 사이클이 형성되는 경우, deadlock의 위험이 있기 때문에 할당해주지 않는다. <br>

꽤나 비효율적인 방식이다. Cycle 생성 여뷰 확인시 무려 O(N)의 시간이 소요된다. <br>

이런 방식도 자원 인스턴스가 하나일 때나 가능하다. 여러개인 경우 뱅커스 알고리즘을 도입해야 한다!


## 4.1 Banker's Algorithm - DeadLock Avoidance
어떤 프로세스들이 자원 요청을 했을 때, 최대 할당을 고려해서 할당해 줄지 안 해줄지를 판단하는 알고리즘으로, <br>
**DeadLock을 해결하는 4가지 방법 중 DeadLock Avoidance에 속한다** <br>
1. 프로세스들이 필요로 하는 각 자원별 최대 사용량을 미리 선언하게 한다. 
2. 현재 남은 자원 양을 계속 체크한다
3. 비록 어떤 프로세스가 남은 양들 보다 적은 자원을 요구해도, <br> **해당 프로세스의 최대 사용량이 현재 남은 양보다 크다면, 할당해주지 않는다!** <br> 즉, **safe 상태를 유지할 경우에만 할당한다**

모든 프로세스는 요청 자원을 모두 할당 받은 경우 유한 시간 자원을 다시 반납한다. 그 덕분에 모든 프로세스들이 결국 자원을 할당 받을 수 있게 되는 것이다. 

### Safe State
프로세스들의 자원 할당 순서를 적절하게 조절해서 Banker's 알고리즘을 만족하면서 모든 프로세스들에게 할당해줄 수 있는 순서를 **safe sequence라고 하고,** 그러한 상태를 **safe state라고 한다.** <br>

어떤 순서 `P1, P2, P3, ... , Pn`이 있다고 하자. <br>
프로세스의 sequence가 safe하려면, 자원 요청이 `가용 자원 + 이전까지의 P들의 보유 자원`에 의해 충족 되어야 한다. <br>
조건을 만족한다면 safe하다. 어떤 Pi번째 자원 요청이 즉시 중족되지 않는다면, **이전까지의 모든 프로세스들의 종료를 기다린 다음, 자원요청을 만족 시켜 수행한다**  <br>

만약에 다른 정책이나 알고리즘으로, 가용 자원 보다 최대 요구가 높은 프로세스에게 자원을 할당 해줌으로서, 시스템이 unsafe state에 있다고 무조건 deadlock에 걸리는 것은 아니다. 그럴 가능성이 있는 것일 뿐. <br>
하지만 safe 상태는 아예 그럴 가능성을 없애기 때문에 DeadLock Avoidance방식은 참 좋다.


## 5. Deadlock Detection And Recovery
### Detection
데드락 감지의 경우 각 프로세스와 자원들을 표로 나타내어 찾아낼 수 있다. <br>
이미 할당된 자원, 요구 자원, 가용 자원들을 표로 나타내어 할당 하는 과정에서 감지한다. <br>
자원들이 1개씩만 있는 경우 각 프로세스와 자원을 그래프로 나타내어 dfs를 통해 사이클을 감지함으로써 찾아낼 수 있다. <br>
사이클이 있는 경우 deadlock이다.  <br>

### Recovery
복구라고 해서 꼭 진짜 복구는 아니다. 리커버리에는 두 가지 방법이 있다.
1. `Process Termination`: 데드락과 관련된 모든 프로세스를 죽여버린다. 데드락 사이클이 사라질 때까지 프로세스를 한번에 하나씩 사살한다
2. `Resource Preemption`: 비용을 최소화할 희생양 (victim)을 선정한다. <br> safe rollback하여 prcess를 restart한다! 한명만 희생하면 모두가 살 수 있잖아.. 한명만 죽인다..! <br> 대신 Starvation 문제가 발생할 수 있다! 계속해서 같은 프로세스가 희생양으로 선정되는 경우 굶어 죽을 수도 있다. <br> 따라서 희생양을 선정할 때 사용하는 cost factor에 rollback 횟수도 포함시킨다!
