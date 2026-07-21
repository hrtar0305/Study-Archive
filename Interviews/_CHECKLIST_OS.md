# OS — 면접관용 키워드 체크리스트

> 용도: 스터디에서 면접관이 답변을 들으며 체크하는 용도.
> **[필수]** = 빠지면 감점·꼬리질문으로 유도 / **[권장]** = 나오면 상급 / **[오답 시그널]** = 바로 파고들 지점.

## Q1. 프로세스와 스레드
- [필수] 프로세스=실행 중인 프로그램의 인스턴스 · 자원 소유·보호 단위 · 독립 가상 주소 공간
- [필수] 스레드=실행·스케줄링 단위 · 같은 프로세스의 주소 공간·자원 공유
- [오답 시그널] 프로세스를 정적인 프로그램과 동일시 / 스레드마다 독립 주소 공간을 가진다고 설명
- 꼬리(공유·독립): [필수] code·data·heap·open files 공유 / PC·register·stack 독립 [권장] TLS·스케줄링 상태
- 꼬리(context switch): [필수] 실행 문맥 저장·복원 · 프로세스는 주소 공간·페이지 테이블 문맥도 변경
- [권장] CPU cache는 반드시 flush되지 않지만 working set 변화로 miss 증가 가능
- 꼬리(TLB 태그): [필수] ASID · x86 PCID · 주소 공간별 TLB 엔트리 태깅
- 꼬리(user vs kernel thread): [필수] user runtime scheduler vs kernel scheduler · 대응 모델에 따른 블로킹·멀티코어 차이
- 꼬리(many-to-one): [필수] 전체 블로킹 가능 · 단일 코어
- 꼬리(one-to-one): [필수] 블로킹 격리 · 멀티코어 · 커널 관리 비용
- 꼬리(M:N): [필수] 다중화 · 병렬성 · 런타임 복잡성
- [오답 시그널] 사용자 수준 스레드는 언제나 하나가 막히면 전체가 막힌다고 일반화

## Q2. 파일 시스템
- [필수] 물리 저장 블록→파일·디렉터리 추상화 · 이름·계층 구조 · 메타데이터 · 공간 할당 · 접근 권한
- 꼬리(구성 요소): [필수] file=논리적 byte sequence · directory=이름 매핑 · metadata=관리 정보
- 꼬리(directory entry): [필수] filename→inode number · 경로 구성요소별 탐색
- 꼬리(inode): [필수] 파일 종류·권한·소유자·크기·timestamps·link count·데이터 위치
- [필수] filename=directory entry · metadata=inode · contents=data blocks
- 꼬리(hard link): [필수] 여러 directory entry→동일 inode · unlink 시 link count 감소 · count 0에서 회수
- [오답 시그널] 확장자를 식별자로 제시 / 아이노드에 파일 이름이나 실제 전체 데이터가 저장된다고 설명

## Q3. CPU 스케줄링
- [필수] ready queue에서 다음 실행 대상 선택 · 대상은 kernel thread일 수 있음 · 효율·응답성·공정성
- 꼬리(평가 지표): [필수] utilization · throughput · turnaround · waiting · response · fairness
- [필수] turnaround=completion−arrival · response=first run−arrival · CPU burst는 workload 특성
- [오답 시그널] response를 완료까지 걸린 시간으로 설명 / CPU burst를 평가 지표로 분류
- 꼬리(preemption): [필수] 강제 CPU 회수 · hardware timer interrupt · context save · scheduler 실행
- [오답 시그널] 선점을 프로세스가 발생시키는 software interrupt로 설명
- 꼬리(FCFS): [필수] arrival order · non-preemptive · convoy effect
- 꼬리(SJF): [필수] shortest predicted burst · 평균 waiting 최소 · 교환 논증 · 미래 burst 추정 필요
- 꼬리(지수 평균): [필수] `τₙ₊₁=αtₙ+(1−α)τₙ` · α↑=최근값 민감 · α↓=과거 평활
- 꼬리(SRTF): [필수] preemptive SJF · remaining time 비교 · starvation · aging
- 꼬리(RR): [필수] circular queue · quantum · 큰 q→FCFS · 작은 q→context switch overhead
- 꼬리(MLFQ): [필수] feedback 승강 · CPU-bound 강등 · interactive 우선 · periodic boost · cumulative CPU allotment
- [오답 시그널] 큐마다 알고리즘이 다르다는 설명에서 종료 / 한 번의 조기 yield만 보고 높은 우선순위를 계속 유지
- 꼬리(계산): A=8, B=4, C=2, arrival=0에서 FCFS·SJF·RR(q=2)의 Gantt chart와 평균 turnaround·response 계산
- [필수] FCFS=34/3·20/3 / SJF=22/3·8/3 / RR=10·2

## Q4. 커널과 시스템 콜
- [필수] 커널=특권 핵심부 · CPU·메모리·프로세스·파일·장치 관리 · 보호된 추상화·서비스 제공
- [오답 시그널] 커널은 CPU에서 항상 실행됨 / 시스템 콜을 하드웨어와 직접 통신하는 함수로만 설명
- 꼬리(진입·복귀): [필수] syscall number·인자 준비 · privilege transition · kernel entry · 문맥 보존 · 인자·pointer·권한 검증 · return to user
- 꼬리(mode vs context switch): [필수] 같은 스레드 복귀는 mode switch만 발생 가능 · blocking 후 다른 스레드 선택 시 context switch
- 꼬리(trap frame): [필수] per-thread kernel stack · 사용자 PC·SP·flags·register 복귀 문맥 · user stack은 신뢰 불가 · TCB와 trap 문맥 구분
- [오답 시그널] 모든 시스템 콜=프로세스 전환 / 복귀 문맥을 user stack에 저장

## Q5. 교착상태
- [필수] 서로 상대방만이 발생시킬 수 있는 사건·자원을 영구 대기 · starvation과 구분
- 꼬리(Coffman): [필수] Mutual Exclusion · Hold and Wait · No Preemption · Circular Wait · 네 조건 모두 필요
- 꼬리(lock ordering): [필수] 전역 획득 순서 통일 · Circular Wait 제거
- 꼬리(RAG): [필수] 프로세스·자원 노드 · P→R=request · R→P=assignment · 단일 인스턴스 cycle⇔deadlock · 다중은 cycle만으로 확정 불가
- 꼬리(예방 vs 회피): [필수] prevention=Coffman 조건 제거 · avoidance=안전 상태만 허용 · maximum claim 필요
- 꼬리(safe state): [필수] safe sequence 존재 · unsafe≠deadlocked · Need=Maximum−Allocation · Available로 safety check
- 꼬리(은행원 계산): 총 10, P1=3/7, P2=2/4, P3=2/6에서 [필수] Need=4/2/4 · P2→P1→P3 · Available=3→5→8→10
- 꼬리(탐지·복구): [필수] process termination · rollback · resource preemption · victim cost · 반복 희생·starvation 방지
- 꼬리(타조): [필수] 범용 OS는 포괄적 처리를 생략할 수 있음 · 비용·maximum 요구량 정보 부족 · kernel lock·timeout·watchdog·DB rollback 등 하위 시스템별 대응은 존재
- [오답 시그널] 간선 방향은 임의 / 다중 인스턴스에서 cycle=deadlock 단정 / unsafe=deadlocked / 현대 OS는 모든 교착상태에 아무 대응도 안 함

## Q6. 가상 메모리
- [필수] 프로세스별 virtual address→physical memory 매핑 · 독립 주소 공간 · 보호·격리·재배치 · 비연속 프레임 활용 · demand paging
- 꼬리(주소 변환): [필수] VA=VPN+offset · MMU · TLB first · PTE가 VPN→PFN 매핑 · offset 유지 · ASID·PCID
- 꼬리(PTE): [필수] Page Table Entry · PFN · present·valid · R/W/X·user 권한 · accessed·reference · dirty
- 꼬리(page fault): [필수] system call이 아닌 synchronous exception · mapping·permission 검사 · backing data · frame 할당·교체 · dirty write-back · PTE·TLB 갱신 · instruction restart
- 꼬리(TLB shootdown): [필수] targeted invalidation · stale mapping 방지 · multicore IPI · remote TLB 무효화·동기화
- 꼬리(교체): [필수] FIFO=oldest loaded · LRU=least recently used · Clock=reference 1→0·skip, 0→victim · LRU 근사
- 꼬리(Belady): [필수] frames↑에도 faults↑ · FIFO 가능 · LRU 불가 · stack property
- 꼬리(thrashing): [필수] ΣWorking Set > available frames · page fault 급증 · CPU utilization 저하 · 다중 프로그래밍 증가 시 악화
- 꼬리(PFF): [필수] 상한 초과=프레임 추가·프로세스 중단 · 하한 미만=프레임 회수 · 필요 시 degree of multiprogramming 축소
- 꼬리(용어): [필수] page=가상 논리 단위 · frame=RAM 물리 공간 · disk=file block·swap slot의 bytes · backing data를 frame에 적재 · anonymous zero-fill 가능
- [오답 시그널] 페이지 테이블이 VPN·offset으로 구성 / page fault=프로세스의 system call / 디스크에서 frame을 가져옴 / Clock bit 처리 반대 / PFF=무조건 2배·절반
