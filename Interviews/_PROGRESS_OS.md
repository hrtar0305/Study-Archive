# OS — 모의면접 진행 현황

> 다른 PC에서 이어서 진행하기 위한 진도 트래커.
> 최종 갱신: 2026-07-22

---

## 다룬 개념

| 날짜 | 개념 | 이해도 | 핵심 약점 |
|---|---|---|---|
| 07-19 | 프로세스와 스레드 | 🟡 보통 | ASID·PCID, TLB와 cache 구분, many-to-one·one-to-one·M:N, 블로킹·멀티코어 관계 |
| 07-20 | 파일 시스템 기초 | 🔴 부족 | 디렉터리 엔트리·아이노드·데이터 블록 관계부터 답변 중단. 별도 학습 후 재면접 필요 |
| 07-20 | CPU 스케줄링 | 🟡 보통 | 평가 지표 계산, hardware timer interrupt, burst 지수 평균, MLFQ gaming 방지 |
| 07-21 | 커널·시스템 콜·실행 모드 | 🟡 보통 | 모드 전환과 컨텍스트 스위칭 구분, 커널 스택의 trap frame, TCB와 trap 문맥 구분 |
| 07-21 | 교착상태 | 🟡 보통 | RAG 판정, safe·unsafe·deadlocked 구분, 은행원 계산, 타조 알고리즘의 범위 |
| 07-21 | 가상 메모리 | 🟡 보통 | PTE 필드, page fault 처리, TLB shootdown, Clock·Belady, PFF, backing data 용어 |
| 07-22 | 프로세스 상태 | 🔴 부족 | New·Ready·Running·Waiting·Terminated, 상태 전이, Ready와 Waiting 구분 |
| 07-22 | 프로세스 간 통신(IPC) | 🟡 보통 | 파이프·FIFO·메시지 큐·Unix domain socket 구분, process-shared 동기화 객체 |
| 07-22 | Race Condition·Critical Section | 🟡 보통 | Mutual Exclusion·Progress·Bounded Waiting, CAS와 acquire·release 메모리 순서 |
| 07-22 | Lock·Semaphore·Condition Variable | 🟡 보통 | Condition Variable의 wait 원자성, Mutex 재획득, predicate의 while 재검사 |
| 07-22 | Crash Consistency·Journaling | 🔴 부족 | 최초 노출. 파일 시스템 구조 선행 학습 후 journaling·recovery 재면접 필요 |
| 07-22 | fork·exec·Copy-on-Write | 🟡 보통 | fork·exec 기본 의미, 상속 FD의 open file description·파일 오프셋 공유. COW는 양호 |

## 남은 범위

- [x] ~~Kernel·system call·user/kernel mode~~ — 07-21 완료 (trap frame·커널 스택 복습 필요)
- [x] ~~Process state·IPC~~ — 07-22 완료 (프로세스 상태 재학습, IPC 수단 구분 복습 필요)
- [x] ~~CPU Scheduling~~ — 07-20 완료 (평가 지표·timer·MLFQ 복습 필요)
- [x] ~~Virtual Memory~~ — 07-21 완료 (PTE·page fault·교체·thrashing 복습 필요)
- [x] ~~Paging·Swapping·TLB·Page Table~~ — 07-21 가상 메모리 면접에서 통합 진행
- [x] ~~Concurrency: Race Condition·Critical Section~~ — 07-22 완료 (세 조건·메모리 순서 복습 필요)
- [x] ~~Lock·Semaphore·Condition Variable~~ — 07-22 완료 (Condition Variable 복습 필요)
- [x] ~~Deadlock~~ — 07-21 완료 (RAG·안전 상태·은행원 알고리즘 복습 필요)
- [ ] **File System — 면접 중단, 별도 학습 후 재면접**
- [ ] **Crash Consistency·Journaling — 07-22 최초 노출 확인, 파일 시스템 학습 후 재면접**

## 복습 우선순위

1. **파일 시스템 전체** — 별도 학습 후 재면접
2. **Crash Consistency·Journaling** — 파일 시스템 구조 선행 후 log·commit·recovery 학습
3. **프로세스 상태와 전이** — New·Ready·Running·Waiting·Terminated, Ready와 Waiting 구분
4. **fork·exec** — 자식 프로세스 생성과 현재 프로세스 이미지 교체 구분
5. **상속된 파일 디스크립터** — 별도 FD 테이블과 공유 open file description·오프셋
6. **Condition Variable** — wait의 Mutex 원자적 해제·수면, 재획득, predicate의 while 재검사
7. **임계구역 해결 조건** — Mutual Exclusion·Progress·Bounded Waiting
8. **메모리 순서** — CAS 원자성과 acquire·release·happens-before 구분
9. **IPC 수단 구분** — 익명 파이프·FIFO·메시지 큐·Unix domain socket·TCP/UDP socket
10. **프로세스 간 동기화** — 공유 메모리의 process-shared mutex와 이름 있는 세마포어
11. **가상 메모리 주소 변환·폴트** — VPN·offset, PTE 필드, 예외 처리, PTE·TLB 갱신과 shootdown
12. **페이지 교체·스래싱** — Clock reference bit, Belady·stack property, Working Set·PFF
13. **교착상태 안전성 판단** — safe·unsafe·deadlocked 구분, Maximum·Allocation·Need·Available, 안전 순서 계산
14. **RAG와 다중 인스턴스** — 요청·할당 간선, 사이클의 필요·충분조건
15. **시스템 콜 진입 문맥** — 사용자 복귀 상태는 스레드별 커널 스택의 trap frame에 저장
16. **모드 전환 vs 컨텍스트 스위칭** — 같은 스레드 복귀와 블로킹 후 스레드 교체 구분
17. **CPU 스케줄링 지표** — turnaround·waiting·response 정의와 계산
18. **CPU 스케줄링 구현** — hardware timer interrupt, burst 지수 평균, MLFQ cumulative allotment
19. **스레드 대응 모델** — many-to-one, one-to-one, M:N의 블로킹·병렬성 차이
20. **ASID·PCID** — 주소 공간별 TLB 엔트리를 구분하는 태그
21. **TLB vs CPU cache** — 역할과 컨텍스트 스위칭 시 영향 구분

> 질문 운영은 [_CHECKLIST_OS.md](_CHECKLIST_OS.md), 기록 규칙은 [_PROTOCOL.md](_PROTOCOL.md) 참고.
