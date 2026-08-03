# OS — 면접관용 키워드 체크리스트

> 용도: 누구에게나 같은 기준으로 사용할 수 있는 범용 OS 모의면접 질문 세트.
> 흐름: 프로세스 기초 → 실행·통신 → 스케줄링·커널 → 동시성 → 메모리 → 저장장치.
> **[필수]** = 핵심 평가 요소 / **[권장]** = 심화 요소 / **[오답 시그널]** = 교정이 필요한 답변.
> 꼬리질문은 앞 답변의 실수에 반응해 만들지 말고, 각 항목을 기초 → 적용 → 구현·한계 순으로 선택한다.
> **[일반]** = 신입·주니어 CS/백엔드 면접에서 교과서 핵심으로 판정 가능한 질문.
> **[심화]** = OS 구현·아키텍처·플랫폼별 세부 동작까지 요구하는 질문. 일반 면접에서는 선택적으로 사용한다.

## [일반] Q1. 프로세스와 스레드
- [필수] 프로세스=실행 중인 프로그램의 인스턴스 · 자원 소유·보호 단위 · 독립 가상 주소 공간
- [필수] 스레드=실행·스케줄링 단위 · 같은 프로세스의 주소 공간과 자원 공유
- 꼬리(공유·독립): [필수] code·data·heap·open files 공유 / PC·register·stack 독립 [권장] TLS·스케줄링 상태
- 꼬리(context switch) **[심화]**: [필수] 양쪽 모두 PC·SP·register 등 실행 문맥 저장·복원 · 같은 프로세스의 스레드 전환은 주소 공간 유지 · 프로세스 전환은 주소 공간 문맥도 변경해 일반적으로 더 비쌈 · TLB는 ASID/PCID 태깅 또는 관련 엔트리 무효화 필요
- 꼬리(thread mapping) **[심화]**: [필수] Many-to-One=전체 블로킹 가능·멀티코어 병렬성 없음 · One-to-One=블로킹 격리·멀티코어 가능·커널 관리 비용 · Many-to-Many=여러 사용자 스레드를 여러 커널 스레드에 다중화·런타임 복잡성
- 꼬리(thread stack) **[심화]**: [필수] 같은 가상 주소 공간 안에 스레드별 독립 stack · guard page의 접근 권한 위반은 synchronous page fault · 배치·크기·성장 방향은 ABI·runtime·OS 의존
- [오답 시그널] 프로세스=정적 프로그램 / 스레드마다 독립 주소 공간 / 모든 사용자 스레드 모델을 동일하게 일반화 / page fault를 외부 interrupt로 설명

## [일반] Q2. 프로세스 상태와 생명주기
- [필수] New · Ready · Running · Waiting/Blocked · Terminated
- [필수] Ready=CPU만 받으면 실행 가능 · Waiting=사건·I/O 완료 전에는 실행 불가
- 꼬리(전이): [필수] Ready→Running=dispatch · Running→Ready=선점 · Running→Waiting=I/O·event wait · Waiting→Ready=완료 통지
- 꼬리(suspend) **[심화]**: [권장] 교재·OS마다 상태 모델이 다름 · Ready Suspended와 Blocked Suspended는 선택적 확장 모델 · suspension과 swap-out을 항상 동일시하지 않기
- 꼬리(queue): [권장] ready queue와 장치·이벤트별 wait queue · PCB/TCB에 상태와 큐 연결 정보 저장
- [오답 시그널] Idle을 보편적인 프로세스 생명주기 상태로 제시 / I/O 완료 후 무조건 즉시 Running

## [일반] Q3. 프로세스 생성: fork·exec·Copy-on-Write
- [필수] `fork`=자식 프로세스 생성 · 부모와 자식에 서로 다른 반환값 · 논리적으로 독립된 주소 공간
- [필수] `exec`=현재 프로세스 이미지 교체 · 새 프로세스 생성 아님 · 성공 시 기존 코드로 미복귀
- [필수] COW=흔한 구현 최적화이지 fork의 의미 자체는 아님
- 꼬리(COW): [필수] 같은 frame을 write-protected로 공유 · 쓰기 fault에서 필요 시 복사·PTE/TLB 갱신
- 꼬리(refcount=1) **[심화]**: [권장] 단독 참조면 복사 없이 writable 전환 가능
- 꼬리(FD) **[심화]**: [필수] FD table은 별도 · 상속 엔트리는 같은 open file description을 참조해 offset·일부 status flag 공유
- 꼬리(multithread) **[심화]**: [권장] POSIX fork 후 자식에는 호출한 스레드만 존재 · exec 성공 시 새 프로그램 이미지로 대체
- [오답 시그널] fork=thread 생성 / exec=new process / 모든 페이지 즉시 복사 / fork 후 파일 offset 독립

## [일반] Q4. 프로세스 간 통신(IPC)
- [필수] 독립 주소 공간 사이의 데이터·이벤트 교환과 실행 조정
- 꼬리(두 모델): [필수] shared memory=설정 후 낮은 data-path overhead, 별도 동기화 · message passing=커널 중재·버퍼링
- [필수] 공유 메모리도 생성·매핑·page fault 등에는 커널이 관여하므로 “커널을 전혀 거치지 않는다”는 표현 금지
- 꼬리(shared lock) **[심화]**: [필수] process-shared mutex·named semaphore처럼 양쪽이 동일 동기화 상태를 공유해야 함
- 꼬리(pipe/queue): [필수] pipe·FIFO=byte stream · message queue=메시지 경계 유지
- 꼬리(socket): [필수] Unix domain=로컬 · TCP/UDP=IP·port, 로컬·원격 가능
- 꼬리(design) **[심화]**: [권장] 데이터 크기·빈도·격리·동기화·네트워크 필요성에 따른 선택
- [오답 시그널] 프로세스별 일반 mutex 두 개로 동기화 / 모든 IPC가 메시지 경계를 보존

## [일반] Q5. CPU 스케줄링
- [필수] 실행 가능한 schedulable entity 중 다음 실행 대상 선택 · OS에 따라 kernel thread 등이 대상
- 꼬리(metric): [필수] utilization · throughput · turnaround · waiting · response · fairness
- [필수] turnaround=completion−arrival · response=first run−arrival
- 꼬리(preemption): [필수] timer interrupt 등으로 강제 CPU 회수 · 문맥 저장 후 scheduler 실행
- 꼬리(algorithms): [필수] FCFS=convoy · SJF/SRTF=짧은 작업 우대·starvation · RR=quantum trade-off
- [권장] SJF의 평균 waiting 최소 성질은 모든 작업이 준비됐고 burst를 안다는 등의 가정 아래 성립
- 꼬리(MLFQ) **[심화]**: [필수] 최근 CPU 사용 행태에 따른 우선순위 조정 · periodic boost/aging · 세부 규칙은 정책 의존
- 꼬리(계산): arrival과 CPU burst가 주어진 새 예제로 Gantt chart·turnaround·response를 직접 계산
- [오답 시그널] response=완료 시간 / 선점을 software interrupt 하나로만 설명 / 특정 MLFQ 규칙을 보편 법칙으로 단정

## [일반] Q6. 커널과 커널 진입
- [필수] 커널=특권 모드에서 실행되는 운영체제 핵심부 · CPU·메모리·프로세스·파일·장치 관리 · 보호·추상화·서비스 제공
- 꼬리(syscall): [필수] 사용자 프로그램의 제어된 커널 서비스 요청 · 번호·인자 준비 → 전용 명령 → 문맥 보존·검증·처리 → user mode 복귀
- 꼬리(mode/context): [필수] mode switch와 context switch 구분 · 같은 스레드가 계속 실행될 수 있음
- 꼬리(hardware/software interrupt): [필수] hardware interrupt=장치·타이머 등 외부 원인·보통 비동기 · software interrupt=일반 면접 문맥에서는 명령으로 의도적 발생·동기 · IPI·Linux softirq 등과 용어 혼동 주의
- 꼬리(exception classes) **[심화]**: [필수] CS:APP 기준 Interrupt=외부·비동기·다음 명령 복귀 · Trap=의도적·동기·다음 명령 · Fault=비의도적·동기·복구 후 현재 명령 재실행 가능 · Abort=치명적·동기·복귀 불가
- [심화] Intel식 분류는 Fault·Trap·Abort를 exception으로, interrupt를 별도로 다룬다는 용어 체계 차이
- 꼬리(blocking) **[심화]**: [필수] syscall이 block하면 복귀 문맥과 스케줄링 상태를 kernel-managed frame·stack·TCB 등에 보존 · 정확한 배치는 구현 의존
- 꼬리(architecture): [필수] monolithic=많은 서비스가 kernel space · microkernel=최소 핵심+user-space service · 직접 호출 vs IPC · 성능·격리·모듈화 trade-off
- [오답 시그널] 모든 시스템 콜=컨텍스트 스위치 / 모든 software interrupt=비동기 / page fault=외부 interrupt / Fault·Trap·Abort·Interrupt 분류를 모든 아키텍처의 보편 용어로 단정

## [일반] Q7. Race Condition과 Critical Section
- [필수] race condition=공유 가변 상태에 대한 동시 접근이 적절히 조정되지 않아 실행 순서·타이밍에 따라 결과가 달라지는 현상
- 꼬리(lost update): [필수] `count++`의 read-modify-write 분해와 갱신 소실
- [필수] Critical Section=공유 상태를 일관되게 다루기 위해 접근을 조정해야 하는 코드 영역
- 꼬리(prevention): [필수] 공유 가변 상태 축소·제거 · mutex/lock으로 임계구역 보호 · semaphore로 접근 수·순서 조정 · atomic operation · message passing·thread confinement 등
- [오답 시그널] 단순히 동시에 실행되기만 하면 race라고 단정 / 동기화 없이 실행 순서에만 의존 / 모든 상황에 하나의 동기화 도구만 고집

## [일반] Q8. Mutex와 Semaphore
- [필수] Mutex=소유권 기반 상호 배제 · 일반적으로 소유자가 unlock
- [필수] Semaphore=비소유권 permit counter · counting semaphore로 여러 동일 자원 관리
- 꼬리(P/V): [필수] wait/P=permit이 생길 때까지 원자적으로 대기 후 하나 소비 · signal/V=permit 반환과 필요 시 대기자 깨움
- [권장] 내부 count의 음수 허용 여부와 wake 시 증가 방식은 구현 표현이므로 한 방식만 보편화하지 않기
- 꼬리(binary): [필수] 값이 0/1이어도 ownership 부재 때문에 mutex와 동일하지 않음
- 꼬리(priority inversion) **[심화]**: [필수] high가 low의 lock을 대기 · medium이 low 실행을 방해해 지연 심화 · priority inheritance로 소유자 우선순위를 일시 상승
- [오답 시그널] binary semaphore와 mutex를 완전히 동일시 / semaphore에도 획득자 소유권이 있다고 설명 / priority inversion을 단순 starvation과 동일시

## [일반] Q9. 교착상태
- [필수] 진행에 필요한 자원·사건을 서로가 기다려 집합 전체가 진행하지 못하는 상태 · starvation과 구분
- [필수] Coffman 조건: Mutual Exclusion · Hold and Wait · No Preemption · Circular Wait
- 꼬리(strategy): [필수] 예방 · 회피 · 탐지 후 회복 · 무시
- 꼬리(prevention/avoidance): [필수] 예방=코프만 조건 중 하나를 제거 · 회피=자원 할당 시 안전 상태를 유지
- 꼬리(detection/ignore): [필수] 탐지 후 프로세스 종료·자원 선점 등으로 회복 · 무시=발생 가능성과 처리 비용을 고려해 별도 대응하지 않음
- [오답 시그널] 예방·회피·탐지를 혼용 / 회피를 교착상태 발생 후 복구라고 설명 / 무시를 교착상태가 절대 발생하지 않는다는 뜻으로 설명

## [일반] Q10. 가상 메모리
- [필수] 프로세스별 독립된 가상 주소 공간 · 가상 주소를 물리 주소에 매핑 · 보호·격리 · 비연속 물리 메모리 활용
- 꼬리(paging/translation): [필수] 가상 메모리를 page, 물리 메모리를 같은 크기의 frame으로 분할 · page number+offset · TLB 우선 조회 · miss 시 page table 확인 · frame number+offset
- 꼬리(present bit): [필수] 0이면 현재 물리 메모리에 유효한 frame으로 존재하지 않음을 의미 · 접근 시 page fault · 항상 swap-out을 뜻하지 않음
- [오답 시그널] page와 frame을 동일시 / TLB를 일반 데이터 캐시로 설명 / present=0을 항상 swap-out으로 단정

## [일반] Q11. Page Fault
- [필수] 현재 명령의 메모리 접근을 정상적으로 변환·허용할 수 없을 때 발생하는 synchronous exception
- [필수] CPU가 커널 handler로 진입 → 커널이 주소와 원인·유효성 확인 → 처리 가능한 경우 frame 준비·매핑 갱신 후 명령 재시작 → 잘못된 접근이면 오류 전달 또는 종료
- 꼬리(dirty victim): [필수] 빈 frame이 없어 교체할 victim이 dirty이면 재사용 전에 backing store에 기록 · anonymous page는 swap, file-backed page는 파일로 기록될 수 있음 · clean page는 보통 기록 없이 폐기 가능
- 꼬리(system call): [필수] 시스템 콜은 프로그램의 의도적인 커널 기능 요청 · page fault는 명령 실행 중 CPU가 감지한 예외
- [오답 시그널] page fault를 시스템 콜이라고 설명 / 모든 page fault가 디스크 I/O를 발생시킨다고 단정 / dirty page를 기록하지 않고 바로 폐기

## [일반] Q12. Thrashing
- [필수] 프로세스들의 working set에 필요한 frame이 부족해 page fault와 page 교체가 반복되고, 실제 명령 실행보다 paging에 더 많은 시간을 쓰는 현상
- [필수] page fault·저장장치 I/O 증가 · CPU 이용률과 처리량 저하 · 과도한 다중 프로그래밍이 원인이 될 수 있음
- 꼬리(mitigation): [필수] Working Set·Page Fault Frequency로 상태 판단 · frame 추가 배분 · 일부 프로세스 중단 등으로 다중 프로그래밍 정도 축소
- [오답 시그널] 단순히 메모리 사용량이 높은 상태라고 설명 / CPU 이용률이 낮다는 이유로 프로세스를 더 투입하면 항상 개선된다고 설명

## [일반] Q13. 파일 시스템
- [필수] 영속 저장장치의 데이터를 file·directory로 구조화 · 이름과 경로 · metadata · 공간 할당과 빈 공간 · 접근 권한 관리
- 꼬리(path lookup): [필수] 경로 구성요소별 directory entry 탐색 · Unix 계열 inode 기반 파일 시스템에서는 이름→inode number
- 꼬리(inode): [필수] 종류·권한·소유자·크기·시간·link count·데이터 위치 · 일반적으로 filename은 저장하지 않음
- 꼬리(link): [필수] hard link=같은 inode · symbolic link=다른 경로 문자열을 담는 별도 파일
- 꼬리(unlink/open): [필수] link count가 0이고 열린 참조도 없어야 최종 회수
- [오답 시그널] 파일 시스템을 파일 내용만 저장하는 구조로 설명 / inode에 filename 저장 / unlink하면 열린 파일 데이터도 즉시 사라진다고 설명

## [일반] Q14. Zombie와 Orphan 프로세스
- [필수] Unix 계열 기준 Zombie=종료했지만 부모가 종료 상태를 아직 회수하지 않은 자식
- [필수] Orphan=실행 중인데 부모가 먼저 종료한 자식
- 꼬리(zombie impact/handling): [필수] 실행·주소 공간 자원 대부분은 반납 · PID·종료 상태 등 최소 정보가 남아 대량 누적 시 프로세스 테이블 자원 고갈 가능 · 부모가 자식의 종료 상태를 회수하도록 처리
- 꼬리(orphan impact/handling): [필수] 계속 실행되므로 자원을 사용할 수 있고 기존 부모의 감독을 잃음 · 그 자체로 오류는 아님 · Unix 계열에서는 init 계열 프로세스나 subreaper에 재부모화되어 관리
- [오답 시그널] Zombie가 CPU를 계속 소비한다고 설명 / Orphan을 이미 종료된 프로세스라고 설명 / 모든 Orphan을 반드시 강제 종료해야 한다고 단정

## [일반] Q15. Blocking·Non-blocking과 Synchronous·Asynchronous
- [필수] Blocking/Non-blocking=호출한 실행 흐름이 기다리는지 즉시 돌아오는지 · Synchronous/Asynchronous=완료를 호출 흐름이 직접 확인하는지 나중에 통지받는지
- 꼬리(four cases): [필수] synchronous blocking=호출이 완료까지 대기 · synchronous non-blocking=즉시 반환 후 직접 반복 확인 · asynchronous non-blocking=요청 제출 후 즉시 반환, 나중에 완료 통지 · asynchronous blocking=비동기 요청을 제출했지만 호출 흐름이 완료 객체를 기다림
- 꼬리(readiness/completion): [필수] readiness=I/O를 시도할 수 있다는 통지 · completion=제출한 I/O 요청 자체가 완료됐다는 통지
- [권장] 네 조합의 명칭과 지원 형태는 API·플랫폼·문맥에 따라 달라질 수 있음
- [오답 시그널] Non-blocking과 Asynchronous를 동의어로 설명 / Non-blocking이면 I/O 전체가 즉시 완료된다고 설명 / 비동기 요청을 제출하자마자 기다리는 흐름을 Non-blocking이라고 설명

## [일반] Q16. 내부 단편화와 외부 단편화
- [필수] 단편화=사용 가능한 메모리가 있어도 할당 단위·배치 때문에 일부 공간을 효율적으로 사용하지 못하는 현상
- [필수] 내부 단편화=할당된 영역 내부의 낭비 · 외부 단편화=할당 영역 사이의 빈 공간이 조각나 큰 연속 영역을 만들지 못하는 상태
- 꼬리(cause/example): [필수] 고정 크기 할당 단위가 요청보다 크면 내부 단편화 · 가변 크기 연속 영역의 할당·해제가 반복되면 외부 단편화
- 꼬리(paging): [필수] 고정 크기 frame 할당으로 물리 메모리의 외부 단편화 완화 · 마지막 page 등에서 내부 단편화 가능
- 꼬리(mitigation): [필수] 내부 단편화는 할당 단위를 작게 하거나 요청 크기에 가깝게 배정 · 외부 단편화는 compaction·빈 공간 병합 또는 paging 같은 비연속 할당으로 완화 · 각 방법에는 관리·이동 비용 존재
- [오답 시그널] 내부·외부 단편화를 반대로 설명 / paging이 모든 메모리 낭비를 제거한다고 설명 / 빈 공간 총량만 충분하면 연속 할당도 항상 성공한다고 설명

## [일반] Q17. Polling과 Interrupt
- [필수] Polling=CPU가 장치 상태를 반복 확인 · 단순하지만 대기 중 CPU 시간 소비
- [필수] Interrupt=장치가 사건을 CPU에 통지 · CPU는 다른 일을 하다가 handler 실행
- 꼬리(trade-off): [필수] 낮은 빈도·긴 대기는 interrupt 유리 · 매우 높은 사건률에서는 interrupt overhead로 polling·혼합 방식이 유리할 수 있음
- 꼬리(polling/busy-wait): [필수] polling=상태 반복 확인 전략 · busy-wait=CPU를 반납하지 않는 대기 방식 · polling 사이에 sleep 가능 · spinlock도 busy-wait
- [오답 시그널] Polling은 언제나 비효율적이라고 설명 / Interrupt가 항상 더 빠르다고 설명 / Polling과 Busy-waiting을 완전한 동의어로 설명

## [일반] Q18. 계층적 페이지 테이블
- [필수] 단일 페이지 테이블은 넓고 희소한 가상 주소 공간에서도 모든 가상 page의 엔트리 공간을 준비해야 해 메모리 낭비가 큼
- [필수] 계층적 구조는 virtual page number를 여러 인덱스로 나누고 상위 테이블이 하위 테이블을 가리키며, 실제로 사용하는 주소 영역의 하위 테이블만 생성
- [필수] 여러 레벨을 사용하는 이유=페이지 테이블 메모리 절약 · 주소 공간 크기·page 크기·엔트리 크기·하드웨어 구조에 맞춘 단계적 주소 변환
- [필수] 레벨이 많아지면 TLB miss 시 page table walk의 메모리 접근 횟수가 늘어날 수 있으며 TLB가 반복 변환 비용을 줄임
- [오답 시그널] 계층적 페이지 테이블이 실제 데이터 page를 계층으로 나눈다고 설명 / 모든 하위 테이블을 항상 미리 생성한다고 설명 / 레벨이 많을수록 항상 빠르다고 설명
