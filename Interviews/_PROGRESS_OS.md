# OS — 모의면접 진행 현황

> 다른 PC에서 이어서 진행하기 위한 진도 트래커.
> 최종 갱신: 2026-07-21

---

## 다룬 개념

| 날짜 | 개념 | 이해도 | 핵심 약점 |
|---|---|---|---|
| 07-19 | 프로세스와 스레드 | 🟡 보통 | ASID·PCID, TLB와 cache 구분, many-to-one·one-to-one·M:N, 블로킹·멀티코어 관계 |
| 07-20 | 파일 시스템 기초 | 🔴 부족 | 디렉터리 엔트리·아이노드·데이터 블록 관계부터 답변 중단. 별도 학습 후 재면접 필요 |
| 07-20 | CPU 스케줄링 | 🟡 보통 | 평가 지표 계산, hardware timer interrupt, burst 지수 평균, MLFQ gaming 방지 |
| 07-21 | 커널·시스템 콜·실행 모드 | 🟡 보통 | 모드 전환과 컨텍스트 스위칭 구분, 커널 스택의 trap frame, TCB와 trap 문맥 구분 |

## 남은 범위

- [x] ~~Kernel·system call·user/kernel mode~~ — 07-21 완료 (trap frame·커널 스택 복습 필요)
- [ ] Process state·IPC
- [x] ~~CPU Scheduling~~ — 07-20 완료 (평가 지표·timer·MLFQ 복습 필요)
- [ ] Virtual Memory
- [ ] Paging·Swapping·TLB·Page Table
- [ ] Concurrency: Race Condition·Critical Section
- [ ] Lock·Semaphore·Condition Variable
- [ ] Deadlock
- [ ] **File System — 면접 중단, 별도 학습 후 재면접**
- [ ] Crash Consistency·Journaling

## 복습 우선순위

1. **파일 시스템 전체** — 별도 학습 후 재면접
2. **시스템 콜 진입 문맥** — 사용자 복귀 상태는 스레드별 커널 스택의 trap frame에 저장
3. **모드 전환 vs 컨텍스트 스위칭** — 같은 스레드 복귀와 블로킹 후 스레드 교체 구분
4. **CPU 스케줄링 지표** — turnaround·waiting·response 정의와 계산
5. **CPU 스케줄링 구현** — hardware timer interrupt, burst 지수 평균, MLFQ cumulative allotment
6. **스레드 대응 모델** — many-to-one, one-to-one, M:N의 블로킹·병렬성 차이
7. **ASID·PCID** — 주소 공간별 TLB 엔트리를 구분하는 태그
8. **TLB vs CPU cache** — 역할과 컨텍스트 스위칭 시 영향 구분

> 질문 운영은 [_CHECKLIST_OS.md](_CHECKLIST_OS.md), 기록 규칙은 [_PROTOCOL.md](_PROTOCOL.md) 참고.
