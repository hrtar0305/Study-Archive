# 자료구조·알고리즘 — 면접관용 키워드 체크리스트

> 용도: 스터디에서 면접관이 답변을 들으며 체크하는 용도. Notion 원본: 스터디 질문 리스트 > 자료구조·알고리즘 — 면접관용 키워드 체크리스트
> **[필수]** = 빠지면 감점·꼬리질문으로 유도 / **[권장]** = 나오면 상급, 안 나오면 힌트 소재 / **[오답 시그널]** = 이 말이 나오면 바로 파고들 지점.
> 공통 운영: 결론만 나오면 반드시 "왜?"를 묻고, 복잡도는 "무엇을 몇 번 하는지" 근거를 요구할 것.

## Q1. Big-O / Ω / Θ / case
- [필수] 상한(upper bound) · 점근적 성장률 · 상수·저차항 무시 · Ω=하한 · Θ=상하한 일치(tight bound) · 표기법과 best/avg/worst는 독립된 두 축
- [권장] formal 정의(∃c, n₀) · 퀵소트 이중 예시(worst=Θ(N²), avg=Θ(NlogN)) · "O(NlogN)=평균, O(N²)=최악"은 관행일 뿐
- [오답 시그널] "Θ는 평균 시간" → case 독립성 꼬리질문 / "Big-O는 최악의 경우를 의미" → 표기법·case 혼동

## Q2. Amortized 분석
- [필수] 연산 시퀀스 전체 총비용 ÷ N · 결정론적 보장(입력 순서 무관) · average case(확률적 기댓값)와의 구분 · 동적 배열 push_back 예시
- [권장] doubling이라 재할당이 기하급수적으로 드물어짐 · potential/banker's method 용어
- [오답 시그널] 확률·운으로 설명 → "최악 순서의 입력이어도 성립하나요?" 꼬리질문

## Q3. 정렬
- [필수] quick worst O(N²) · merge 공간 O(N) · heap 공간 O(1) · 안정: insertion/bubble/merge vs 불안정: selection/heap/quick
- [오답 시그널] quick best O(N) / insertion best O(1) → 즉시 정정 요구
- 꼬리(quick 최악): [필수] pivot 최솟/최댓값 편향 · 정렬된 입력+고정 pivot · median-of-three/랜덤은 완화일 뿐 보장 아님
- 꼬리(표준 라이브러리): [필수] Introsort 계열(깊이 초과 시 heapsort 전환, C++ 표준 라이브러리의 대표적 구현) · Timsort(Python 및 Java 객체 정렬) [권장] ipnsort(현재 Rust `sort_unstable`) · natural run · 소구간 insertion
- 꼬리(stable): [필수] 동일 키 상대 순서 보존 · 다중 키 정렬 [권장] radix 정확성의 전제
- 꼬리(캐시): [필수] quick=순차 스캔 캐시 친화 vs heap=인덱스 점프 캐시 미스 [권장] 캐시 라인 64B · prefetcher · Introsort가 평소 quick을 쓰는 이유
- 꼬리(counting): [필수] 값=인덱스 · O(N+K) · 비교 없음→Ω(NlogN) 하한 비적용 [권장] K 크면 비효율 · 이산 값 한정
- (참고) quick 공간 O(logN)은 "작은 파티션부터 재귀" 구현 전제 — 순진한 구현의 최악 재귀 깊이는 O(N)

## Q4. 해시 테이블
- [필수] 키 → 해시값 → 버킷 인덱스 · 조건부 평균 O(1) · 충돌 집중 시 최악 O(N)
- [오답 시그널] "항상 O(1)" / 해시값과 버킷 인덱스를 같은 것으로 설명
- 꼬리(충돌 해결): [필수] separate chaining=버킷당 여러 원소·α>1 가능 / open addressing=배열 내부 probing·α<1 · cache locality와 메모리 trade-off
- [오답 시그널] chaining을 반드시 linked list로만 구현한다고 단정
- 꼬리(load factor): [필수] α=N/M · N=저장된 전체 원소 수 · chaining은 α>1 가능 · open addressing은 α→1에서 급격히 악화
- [오답 시그널] 분자를 "점유된 버킷 수"로 정의 / 0.7을 절대 기준으로 암기
- 꼬리(clustering): [필수] linear=primary clustering · quadratic=secondary clustering 잔존 · double hashing=키별 탐사 간격
- [권장] Double hashing의 step과 테이블 크기 M이 서로소여야 전체 슬롯 탐사 가능
- [오답 시그널] primary와 secondary를 "첫 해싱/두 번째 해싱"으로 구분
- 꼬리(삭제): [필수] empty=탐색 종료 신호 · 단순 삭제 시 probing 경로 단절 · tombstone은 탐색 통과·삽입 재사용
- 꼬리(복잡도): [필수] 균등 분포 가정 · load factor 상수 제한 · 최악 O(N) · 동일 키 갱신과 서로 다른 키의 충돌 구분
- [오답 시그널] "테이블이 꽉 찰 때만 O(N)"
- 꼬리(rehashing): [필수] 새 배열 생성 · 인덱스 재계산 · 단일 rehash O(N) · 배수 확장 총비용 O(N) → 삽입 amortized O(1)
- 꼬리(hash flooding): [필수] 의도적 충돌로 서비스 거부 · 실행별 무작위 seed/keyed hash · 균형 BST treeification으로 최악 O(logN) [권장] 입력·요청 제한
- [오답 시그널] 해시 알고리즘 은닉만으로 충분 / 메모리 HashMap 버킷의 기본 전환 구조로 B-tree 제시

## Q5. 힙
- [필수] **완전** 이진 트리 · 부모-자식 국소 규칙(전역 정렬 아님) · min/max
- [오답 시그널] "이진 트리"라고만 → 완전성이 배열 표현의 전제임을 꼬리질문 / "힙은 정렬된 구조" → 형제 간 순서 반례
- 꼬리(배열): [필수] 인덱스 산술(0-index: 부모 (i-1)/2, 자식 2i+1·2i+2)
- 꼬리(삽입/삭제): [필수] sift-up/down · O(logN) · min heap은 두 자식 중 작은 쪽과 교환
- 꼬리(heapify): [필수] 역순 sift-down O(N) [권장] 리프 절반은 0칸 이동 · 급수 수렴 Σ(N/2^(h+1))·h
- [오답 시그널] "heapify도 O(NlogN)" → 리프의 이동 거리 꼬리질문
- 꼬리(d-ary): [권장] d가 커지면 높이 log_d N은 감소하지만 sift-down의 레벨당 자식 비교는 증가 · 삽입 Θ(log_d N), 삭제 Θ(d·log_d N) · workload에 따라 4-ary가 유리할 수 있음
- 꼬리(Top-K): [필수] 크기 K min-heap · O(NlogK) · 작업 메모리 O(K) [권장] 전체 N개를 저장할 필요 없는 스트리밍에 적합 · quickselect 평균 O(N) 대안

## Q6. BST / 균형 트리
- [필수] 왼<부모<오른쪽 재귀 규칙 · O(H)
- 꼬리(편향): [필수] 정렬 입력 순차 삽입 → skewed → O(N)
- 꼬리(self-balancing): [필수] AVL(높이차≤1) · Red-Black(색 규칙) · 회전으로 복원
- 꼬리(trade-off): [필수] AVL=낮은 높이·탐색 유리 vs RB=회전 상수 상한(삽입≤2·삭제≤3)·갱신 유리 [권장] 1.44logN vs 2logN · 라이브러리 대부분 RB · (정밀) AVL 삽입 회전은 최대 1회, 삭제 회전이 O(logN)회 전파 가능
- 꼬리(B-tree): [필수] 디스크는 블록 단위 I/O · 노드=블록 → 다진 → 높이 급감 → I/O 감소
- [오답 시그널] "B-tree는 높이가 낮아서"까지만 → "왜 다진으로 만들 수 있는가(블록)" 꼬리질문

## Q7. 그래프 표현·최단경로
- [필수] 인접 리스트 공간 O(V+E) · 행렬 O(V²)/연결확인 O(1) · sparse/dense 선택
- [오답 시그널] 리스트 공간을 O(E)라고만 → 정점 목록 자체 비용 지적
- 꼬리(BFS/DFS): [필수] 큐/스택 · 레벨 확장 vs 한 경로 끝까지
- 꼬리(BFS 보장): [필수] 삽입 순서=거리 순서 · 처음 도달=최단
- 꼬리(다익스트라): [필수] pop 시점 확정(그리디) · 음의 간선에서 확정 논리 붕괴
- 꼬리(벨만-포드/플로이드): [필수] O(VE) · O(V³) · 단일 출발 vs 전체 쌍
- [오답 시그널] 벨만-포드 O(V²) → "V번 반복 × 매번 무엇을 relax하나" 유도
- 꼬리(음의 사이클): [필수] 출발점에서 도달 가능한 음의 사이클과 그 이후 정점의 거리가 -∞로 발산 · Bellman-Ford의 V번째 이완 갱신은 출발점에서 도달 가능한 음의 사이클 탐지 [권장] 음의 간선≠음의 사이클 · dist[i][i]<0 · 환율 arbitrage

## Q8. 유니온-파인드
- [필수] find(대표)/union(병합) · 최악 O(N)(한 줄 트리)
- 꼬리(최적화): [필수] path compression(경로 노드→루트 직결) · union by rank/size — **작은/낮은 트리를 큰/높은 트리 아래로**
- [오답 시그널] union 방향 반대 → "큰 트리를 밑에 넣으면 무슨 일이 생기나" 꼬리질문 (본인 과거 약점)
- 꼬리(α): [필수] amortized O(α(N)) · 역 아커만 함수 · 상수 아님(사실상 상수, ≤4) [권장] 두 최적화 병행해야 보장
- [오답 시그널] "α는 수학 상수" → 아커만 함수와의 관계 꼬리질문

## Q9. 연결 리스트
- [필수] 노드+포인터 비연속 메모리 · random access 불가 O(N) · "연산 자체 O(1) vs 탐색 포함 O(N)" 분리
- 꼬리(O(1) 삭제): [필수] prev 필요 → 우회: next 값 복사+건너뛰기 · 한계: 꼬리 노드 불가 · 노드 identity 변경 및 제거된 next 노드에 대한 외부 참조가 dangling reference가 될 수 있음
- 꼬리(캐시): [필수] spatial locality · 캐시 라인 단위 로드 [권장] prefetcher · pointer chasing
- 꼬리(LRU): [필수] HashMap+이중 연결 · 해시맵→노드 O(1) 접근 · prev/next로 O(1) 분리·재연결 · 퇴거 시 해시맵도 함께 제거 [권장] LRU=recency vs LFU=frequency
- [오답 시그널] LRU를 빈도 기반으로 설명 → LFU와의 구분 꼬리질문

## Q10. 스택/큐/덱
- [필수] LIFO/FIFO(pop 순서 차이)
- 꼬리(배열 큐): [필수] shift O(N) · head 포인터 시 공간 낭비(false full)
- 꼬리(원형 큐): [필수] 모듈러 wrap-around · full/empty 구분(한 칸 비움 or size 변수)
- 꼬리(두 스택 큐): [필수] inbox/outbox · 이동 시 순서 역전 · amortized O(1)을 원소당 최대 3회로 정량화
- 꼬리(활용): [권장] 괄호 검증 · 모노토닉 스택 · 콜스택 · 후위표기식 · undo/redo
- 꼬리(DFS/BFS 이유): [필수] 최근 발견 우선=경로 지속 vs 발견 순=레벨 확장
- 꼬리(덱 고유 활용): [필수] 0-1 BFS(0→front, 1→back) 또는 슬라이딩 윈도우 모노토닉 덱
- 꼬리(0-1 BFS 불변식): [필수] 덱에는 정점이 들어가며 그 정점들의 거리 label이 비감소 순서이고 최대-최소≤1 · front 정점 u의 거리 d=dist[u] · 완화로 생기는 거리∈{d, d+1} [권장] BFS 큐의 레벨 k/k+1 공존과 동일 원리
- [오답 시그널] "정렬돼 있다고 가정하면 유지"(순환 논리) / 간선 가중치와 정점의 누적 거리 label 혼동 → "덱에 들어가는 것은 무엇이고 정렬되는 값은 무엇인가" (본인 과거 약점)

## Q11. 트라이
- [필수] prefix 특화 트리 · 노드=자식 맵+end 마커 · 삽입·탐색 O(L)
- 꼬리(해시셋 대비): [필수] prefix 질의(존재/개수/열거)가 차별점 — 해시셋은 멤버십만
- [오답 시그널] "해시셋보다 공간 효율이 좋다"로만 → "항상 그런가요?" 챌린지
- 꼬리(모든 prefix 저장): [필수] 단어당 O(L²)(1+2+…+L) vs 트라이 O(L)=조상 노드 공유
- 꼬리(카운트): [필수] 삽입 경로 노드마다 카운터 +1(추가 비용 없음)
- [오답 시그널] 세그먼트 트리식 역방향 갱신 → 과설계 지적
- 꼬리(삭제): [필수] end 마커만 지우면 유령 경로 → 카운터 0 지점부터 물리 제거
- 꼬리(공간): [필수] prefix 공유↑ 유리 / 공유↓ 노드 오버헤드로 불리
- 꼬리(압축): [필수] Radix Tree(Patricia) · 단일 자식 체인→문자열 간선 압축 · 분기 시 split [권장] 노드 수∝분기점 · IP 라우팅 최장 prefix 매칭
- (참고) 정렬 배열+이분 탐색도 prefix 범위 질의 가능(O(L logN), 정적 데이터) — 트라이는 O(L)+동적 삽입 유리

## Q12. 분할 정복
- [필수] divide/conquer/combine · merge sort 매핑
- 꼬리(점화식): [필수] T(N)=2T(N/2)+O(N) · 레벨당 O(N) × logN 레벨
- 꼬리(마스터 정리): [필수] aT(N/b)+f(N) · N^(log_b a) vs f(N) 비교 3케이스 · **Case 2=log 인자 추가** · merge sort=Case 2
- [오답 시그널] Case 2에서 "그냥 O(N)" → 방금의 recursion tree 결론과 모순 지적 (본인 과거 약점)
- 꼬리(대표 문제): [권장] 이진탐색 · 카라추바(곱셈 4→3) · 스트라센(8→7) · FFT · BFPRT · convex hull
- 꼬리(최근접 점 쌍): [필수] O(N²)→O(NlogN) · strip 폭 2δ · 점당 상수 개 비교(패킹 논증) · **분포 무관 worst-case 보장**
- [오답 시그널] "균일 분포 가정 하에" → 어떤 분포에서 깨지는지 반문 (본인 과거 약점)
- 꼬리(max subarray): [권장] D&C O(NlogN) vs Kadane O(N) — D&C가 항상 최선 아님

## Q13. 동적 프로그래밍 (DP)
- [필수] 부분 문제 답 저장·재사용 · overlapping subproblems · optimal substructure의 의미
- [권장] 최적화 외 counting·feasibility DP에서는 "부분 문제의 답으로 현재 상태를 구성할 수 있는가"로 일반화
- [오답 시그널] "재귀를 반복문으로 바꾸는 것" / 작은 문제로 나눌 수 있으면 모두 DP
- 꼬리(두 성질): [필수] overlapping=효율성 · optimal substructure=정확성 · Merge Sort는 비중복 · Fibonacci는 중복
- 꼬리(memo vs tabulation): [필수] top-down vs bottom-up · 필요한 상태만 계산 vs 의존 순서대로 채움 · 호출 스택 trade-off
- [권장] 희소 상태 · cache locality · tabulation의 rolling array
- [오답 시그널] "tabulation은 항상 메모리를 더 사용"
- 꼬리(설계 요소): [필수] 상태=부분 문제 식별 정보 · 점화식=전이 · base case=경계 정답 · 계산 순서=의존 상태 선계산
- [오답 시그널] 점화식만 말하고 상태 의미나 계산 순서를 설명하지 못함
- 꼬리(복잡도): [필수] 상태 수 × 상태당 전이 비용 · Coin Change O(kn), 공간 O(n)
- 꼬리(0/1 Knapsack): [필수] 2D·1D 점화식 · 0/1은 용량 내림차순 · 같은 단계 갱신값 재사용 방지 · Unbounded는 오름차순
- [오답 시그널] "DP는 항상 왼쪽부터 채운다" / 오염된다는 표현만 있고 무게 2·가치 3·용량 4 최소 반례를 못 듦
- 꼬리(rolling array): [필수] 제한된 과거 레이어 의존 · 덮어쓰기 순서 · 경로 복원 정보 손실 [권장] parent 저장 또는 재계산
- 꼬리(pseudo-polynomial): [필수] W의 숫자값 vs 표현 비트 수 logW · O(NW)는 입력 길이에 대해 지수 가능
- [오답 시그널] "상수가 커서 pseudo-polynomial"
- 꼬리(DP vs greedy): [필수] greedy choice property 추가 요구 · 동전 {1,3,4}, 금액 6에서 greedy=3개 vs 최적=2개
- 꼬리(LIS): [필수] O(N²) 상태·전이 · tails+binary search O(NlogN) · tails 자체는 실제 LIS가 아님 [권장] parent 추적으로 복원

## Q14. 배열·동적 배열
- [필수] 연속 메모리 · base+i×element_size · random access O(1) · 중간 shift O(N)
- [필수] 연결 리스트는 위치 탐색 O(N)과 포인터 재연결 자체 O(1)을 구분
- [오답 시그널] "배열 탐색은 O(N)"처럼 access와 search 혼동
- 꼬리(주소 계산): [필수] 고정 크기 원소 · base+i×w · N과 무관한 산술 계산 [권장] O(1)과 실제 latency 구분
- 꼬리(cache): [필수] cache line · spatial locality · 규칙적 stride와 prefetcher · pointer chasing · 의존적 cache miss
- [오답 시그널] "연속이라 빠르다"에서 하드웨어 메커니즘 설명이 끝남
- 꼬리(dynamic array): [필수] size vs capacity · 새 블록 할당 · 전체 복사·이동 O(N) · append worst O(N), amortized O(1)
- [권장] 재할당 후 기존 pointer·reference·iterator invalidation
- 꼬리(확장 증명): [필수] 배수 확장 등비급수 총복사 O(N) · 고정량 c 확장 총복사 Θ(N²/c) · c 상수면 append amortized Θ(N)
- [오답 시그널] 고정량 확장의 전체 비용을 확장 횟수 O(N/c) 또는 O(N)으로 계산
- 꼬리(축소): [필수] 경계에서 확장·축소 반복 thrashing · 서로 다른 임계값(hysteresis) [권장] full 시 2배, 사용률 1/4 이하에서 절반
- 꼬리(2차원 배열): [필수] row/column-major의 연속 방향 · 반대 방향은 큰 stride · C row-major · Fortran/MATLAB column-major
- [필수] Java 2차원 배열·Python 중첩 리스트는 전체가 하나의 연속 2차원 블록이라고 단정하지 않음
- 꼬리(tiling): [필수] 캐시 상주 블록 재사용 · temporal locality · O(N³)은 동일 · cache miss·memory traffic 감소

## Q15. 트리 기초
- [필수] 무방향 그래프에서 connected + acyclic · 동치 표현: 임의의 두 정점 사이 경로가 유일 · 정점 N개이면 간선 N-1개
- [오답 시그널] "간선이 N-1개면 트리"라고만 답함 → 연결 또는 비순환 조건이 없으면 반례가 있음을 확인
- 꼬리(용어): [필수] root=부모 없음 · parent/child/sibling · leaf=자식 없음 · depth=루트에서 해당 노드까지의 간선 수 · node height=해당 노드에서 가장 먼 leaf까지의 간선 수 · tree height=root height · rooted tree의 degree=자식 수
- [오답 시그널] node height를 root부터의 거리로 설명 / tree height를 root와 임의의 leaf 사이 거리로 설명 / degree를 parent까지 포함한 incident edge 수로만 설명
- 꼬리(예시 계산): [필수] A의 자식 B·C, B의 자식 D인 트리에서 B=(depth 1, height 1, degree 1), D=(depth 2, height 0, degree 0), tree height=2, B와 C는 sibling
- 꼬리(이진 트리 종류): [필수] full=모든 노드의 자식 수가 0 또는 2 · complete=마지막 레벨 전까지 가득 차고 마지막 레벨은 왼쪽부터 채움 · perfect=모든 내부 노드가 자식 2개이고 모든 leaf의 depth가 같음(=full+complete)
- [오답 시그널] full과 complete의 정의를 뒤바꿈 / complete를 "모든 노드의 자식이 2개"라고 설명
- 꼬리(순회): [필수] preorder=root-left-right · inorder=left-root-right · postorder=left-right-root · level-order=BFS+queue · 재귀 DFS는 call stack 사용, 반복 구현은 명시적 stack 사용
- [권장] preorder=top-down 처리·구조 정보/null marker를 포함한 직렬화 · inorder=BST에서 정렬 순서 · postorder=삭제·bottom-up 계산 · level-order=레벨별 처리
- [오답 시그널] preorder 값 순서만으로 임의의 이진 트리를 항상 유일하게 복원·직렬화할 수 있다고 단정
- 꼬리(표현): [필수] 포인터 기반=노드와 연결 저장 · 배열 기반=인덱스 산술로 부모·자식 계산 · complete binary tree에서 빈칸이 거의 없어 효율적 · sparse/skewed tree에서는 빈 슬롯 낭비
- [권장] 0-index에서 parent=(i-1)/2, children=2i+1·2i+2 / 1-index에서 parent=i/2, children=2i·2i+1
- 꼬리(증명): [필수] 연결된 N개 정점에는 최소 N-1개 간선 필요(새 정점을 연결 요소에 편입할 때마다 간선 최소 1개) · 연결된 N개 정점과 N-1개 간선에 cycle이 있다고 가정하면 cycle 간선 하나를 제거해도 연결되어 N-2개 간선으로 연결 가능해지는 모순
- [권장] acyclic이지만 disconnected이면 tree가 아니라 forest

## Q16. MST
- [필수] spanning=모든 정점 포함 · 가중치 합 최소 · N-1 간선 · (전제) 무방향·연결 그래프
- 꼬리(두 알고리즘): [필수] Kruskal=간선 정렬+union-find 사이클 판정 / Prim=정점 확장+우선순위 큐
- 꼬리(복잡도): [필수] Kruskal O(ElogE), 힙 기반 Prim O(ElogV) · sparse/dense 선택은 구현과 표현 방식에 의존 · dense에서는 배열 기반 Prim O(V²)이 특히 유리
- 꼬리(배열 Prim): [필수] dist[] V회 선형 탐색=O(V²) · dense(E≈V²)에서 힙 O(V²logV)보다 유리
- [오답 시그널] dense→Prim 결론만 암기 / 엉뚱한 알고리즘(플로이드 등)으로 샘 → "dist[]에 담기는 값이 무엇인가"부터 유도 (본인 과거 약점)

## Q17. 위상 정렬
- [필수] DAG 한정 · 사이클 시 선후 정의 불가
- 꼬리(구현): [필수] in-degree 계산 · 0인 정점 큐 · 꺼내며 이웃 감소
- 꼬리(사이클 판별): [필수] 처리 정점 수 < V
- 꼬리(복잡도): [필수] O(V+E)
- [오답 시그널] O(E)만 → 고립 정점 100개 반례 꼬리질문 (본인도 이 반례로 정정했던 지점)
- [권장] DFS 종료 시각 역순 방식도 존재 · Q18 Kosaraju와의 연결

## Q18. SCC
- [필수] 방향 그래프 · **경로를 통한** 상호 도달 가능성 · 최대 부분집합
- [오답 시그널] "모든 쌍 직접 간선" → 도달 가능성으로 유도 (본인 과거 약점) / "union-find로 풀면 된다" → 방향성 문제 지적
- 꼬리(naive): [필수] 전 정점 BFS/DFS=O(V(V+E))
- 꼬리(Kosaraju): [필수] ①DFS 종료 시각 스택 ②전치 그래프(SCC 보존) ③역순으로 전치에서 DFS=각 트리가 SCC · O(V+E) [권장] 역순 처리가 SCC 섞임 방지의 핵심 · Tarjan(low-link, DFS 1회)
- 꼬리(위상정렬 관련): [권장] condensation → 항상 DAG
