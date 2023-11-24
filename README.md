# 도와줘요 스피드 웨건
**[목표]** <br>

1. **내가 스피드 웨건이 된다 - 개념을 말로 설명하는 것을 연습하기 위함** <br> 말로 설명할 수 없으면, 이해하고 있지 않은 것이나 다름 없다. 이 레포는 말하기 위한 연습장. <br> **핵심은 놓치지 않으면서, 너무 지엽적이거나 길어지지 않는 설명이 목표** 

2. **Divide and Conquer** : 머리속에 잘 정리해 담아두고, 말로 설명할 수 있어야 한다고 생각한 개념들이 **너무 많다.** 너무 많다보니, 의욕도 떨어지고 막막하다. 또 공부해야겠다 싶은 개념들이 많다보니, 생각만 하고 잊어버리는 일이 잦았다. <br> **-> 이런 상황에선 분할 정복이 최고다.** 한번에 다 하려 욕심내지 말고, 필요하다고 생각되는 개념들을 목차처럼 나열하고, 시간이 허락할 때마다 하나씩 작성해보자.

<br>

할 수 있다. 천천히 하나씩 하면 된다.

## 1. Network
1. OSI 7 계층 
2. TCP/IP
3. 3, 4-Way Handshake
4. TCP vs UPD
5. DHCP
6. [HTTPS와 SSL/TLS Handshake](https://github.com/binary-ho/Save-Me-Speedwagon/blob/main/Network/HTTPS%EC%99%80%20SSL-TLS%20Handshake.md)
7. 소켓과 포트, 웹소켓, 소켓 통신
8. HTTP/1.1, HTTP/2 차이
9. RESTful
<details> <summary> <b> 10. 쿠키와 세션, JWT -> Stateless </b> </summary>  
============================================== <br>
**결국 Stateless한 서버와 HTTP 사용 중 "인가"가 필요하기 때문에 쓴다.** <Br>
Stateless한 경우, 인증을 위한 정보들을 페이지를 이동할 때마다 다시 인증을 받아야 한다. 쿠키와 세션은 결국엔 이러한 정보를 어디에 저장할 것인지에 대한 이야기이다. <br> <br>
1. **쿠키는 이런 인증 정보를 브라우저에 저장한다. (클라이언트 로컬)** <br> Request에 쿠키를 포함시킨다. <br> 단점으로는 이런 쿠키를 브라우저에서 조작하거나, 중간에 가로챌 수 있다는 점이다. (클라이언트 로컬에 저장하기 때문) <br> <br>

2. **세션은 인증 정보를 서버에 저장한다.** 브라우저 1개당 하나의 Session ID를 발급해 저장하고, 브라우저 종료시 소멸된다. <br> **물론 이 세션 ID도 쿠키에 저장해야 한다.** 하지만, 인증을 위한 중요한 정보가 서버에 저장되기 때문에, 쿠키보다 보안은 우수하다. 대신에 Stateless가 깨지는 것. <br> <br>

세션을 사용하는 것의 단점은 **결국 Stateless가 깨지는 것에서 오는데,** Scale Out상황에서 세션 정보들을 여러 서버가 공유해야 한다는 단점이 생기고, 서버에 문제가 생기는 경우 서버 자체가 State를 복구해야 할 수도 있는 책임이 생긴다. <br> **장점으로는 역시 보안과 + 동시접속 파악이 가능하다.** 넷플릭스와 같은 서비스는 이런 세션 정보를 저장할때 접속처를 저장해두고, 대조해서 동시접속을 파악한다.  <br> <br>

3. **JWT 토큰은 왜 사용하나** <br>
결국 쿠키를 활용해 인증인가 하면 편한데, 중간에 탈취되는 것이 문제. <br>
JWT는 이런 인증 정보를 이용해 만든 Json Web Token으로 인증 정보들을 인코딩해 보관한다. <br>
그럼 간단하게 디코딩 가능한데 이게 안전한가? 그냥 쿠키 아닌가? 싶은데, <br>
토큰을 만드는 과정에서 사용하는 여러 정보들을 이용해 "Signature" - 서명을 만드는데, 이 서명은 서버의 공개키로 암호화 되어 있다. 그래서 서버만 복호화 할 수 있다. <br> **결국 개인키로 암호화된 시그니처 덕분에 안전한 것.** <br> <br>
 
============================================== <br>

</details>

11. HTTP 응답 코드와 차이

<details> <summary> <b> 12. HTTP Method 밸런스 게임 </b> </summary>  
============================================== <br>

### 1. GET vs POST
`GET`은 서버에 리소스 Read를 요청할 때 주로 사용하고, POST는 리소스를 생성하거나 업데이트 하기 위해 주로 사용한다. 이런 규칙들은 꼭 지킬 필요는 없다. 특징을 이해하고 상황에 맞게 쓰면 된다. <Br>
**GET은 일반적으로 Request Body가 없고, Data path가 노출된다. 또한 응답시 `Cache-Control` 헤더를 통해 캐싱할 수 있고, 멱등하다.** (브라우저에게 데이터를 캐싱하도록 한다. `max-age` 값이 캐시 유효 시간을, `age`는 경과 시간을 의미) <br>
POST는 Body를 넣을 수 있다. 일반적으로 캐싱할 수 없고, 멱등하지 않다. (당연히 브라우저 캐싱을 말하는 것)

### 2. PUT vs PATCH
둘 다 자원을 수정하는 용도로 사용하나, 차이가 있음
- `PUT` : 요청한 URI를 payload나 Request Body에 있는 자원으로 대체한다. (replace) <br> 해당 URI에 자원이 없으면 저장하고 201 (Created) 응답을 한다. <br> 자원이 있는 경우 payload로 자원을 만들어, 기존 자원을 대체한다. 200 ok 혹은, 204 (no content)를 통해 알려준다. <br> <br>

**주의할 점은 해당 자원의 모든 상태를 적어야 한다는 점이다.** 자원의 일부만 보내면 그 부분만 교체하는 것이 아니라, 그 일부분으로 전체를 교체해버린다. <br> 엔티티 필드 일부가 null이 되어버릴 수도 있다. <Br>
**또한 PUT은 멱등하다.** [이해하진 못했다](https://stackoverflow.com/questions/28459418/use-of-put-vs-patch-methods-in-rest-api-real-life-scenarios)

- `PATCH` : **자원의 부분적 수정을 위한 HTTP 메서드** <br> 

<br>

**참고로 POST는 "생성"으로서 수정과는 성격이 조금 다르고, 멱등하지 않다.** 매번 새로운 자원을 만들기 떄문이다.

<br>

============================================== <br>

</details>


13. 브라우저 주소 입력 이후 랜더링 까지
14. DNS와 Load Balancer
15. SOP 정책, CSRF, XSS
16. 라우팅과 포워딩
17. Subnet Mask, Gateway
18. Multiplexing, Demultiplexing

## 2. OS
1. System Call
2. Interrupt
3. [Process와 Thread](https://github.com/binary-ho/Save-Me-Speedwagon/blob/main/Operation%20System/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%99%80%20%EC%8A%A4%EB%A0%88%EB%93%9C%2C%20%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8%20%EC%8A%A4%EC%9C%84%EC%B9%AD%20%EB%B9%84%EA%B5%90.md)
4. [Process vs Thread](https://github.com/binary-ho/Save-Me-Speedwagon/blob/main/Operation%20System/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%99%80%20%EC%8A%A4%EB%A0%88%EB%93%9C%2C%20%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8%20%EC%8A%A4%EC%9C%84%EC%B9%AD%20%EB%B9%84%EA%B5%90.md)
<details> <summary> 5. Process 주소 공간 </summary>  
============================================== <br>
컨텍스트를 저장함. 시분할 시스템에서 프로세스 스위칭시 문맥을 저장하기 위한 자료 구조이고, 저장 및 복원의 오버헤드가 있다. <br> <br>
여러 프로세스들의 PCB는 링크드 리스트 형태로 줄줄이 달려있다. 스레드는 TCB를 가지고 있다. <br>
(기억 안 나는건 찾아보기) <br> <br>

1. Process State
2. PC: Program Counter의 Value
3. CPU Register의 Value
4. CPU Scheduling information
5. Memory Management Information
6. Accounting Information: 자원 사용 정보
7. I/O Status Information

==============================================
</details> 

6. CPU Scheduling
7. 동기화
8. 뮤텍스와 세마포어
9. Dead Lock
10. 캐시메모리와 메모리 계층성
11. 웹 캐싱
12. 이질형 캐싱
13. 캐시 만료 정책
14. Redis 싱글 스레드
15. Redis Collections
16. Redis 캐싱 전략
17. Redis Architecture
18. 가상 메모리
19. Thrashing
20. Paging vs Segmentation
21. Page Replacement Algorithem
22. TLB
23. File Descriptor, File System
24. Sync, Async, Blocking, Non-Blocking
25. I/O Multiplexing

## 3. DB
1. Index
2. B-Tree, B+Tree
3. Index in MySQL, PostgreSQL
4. Table Full Scan, Index Range Scan
5. Clustered vs Non-Clustered
6. ACID와 Durability
7. 트랜잭션 격리 수준
8. 트랜잭션 격리 수준 in MySQL, PostgreSQL
9. MVCC
10. DB Locking
11. JOIN
12. Schema 3계층
13. DBCP


## 4. Java
1. JVM과 내부 구조
2. JVM 메모리 구조
3. JIT 컴파일러
4. 클래스 로더
5. Garbage Collection
6. Reflection
7. equals와 동등 연산자
8. System.out.println()
9. stream parallel 조심 이유
10. 어노테이션
11. 제네릭과 Type Erase
12. 컬렉션 정적 팩터리 메서드
13. 자바와 동시성
14. 동시성 컬렉션
15. 직렬화와 역직렬화
16. String Constant Pool
17. Completable Future
18. Java 11 to 17
19. Thread Pool이 클 수록 좋은가
