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
10. 쿠키와 세션, Stateless
11. HTTP 응답 코드와 차이
12. HTTP Method와 Header
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
