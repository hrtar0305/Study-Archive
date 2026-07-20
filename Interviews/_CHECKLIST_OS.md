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
