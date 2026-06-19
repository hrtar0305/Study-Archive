# 모의면접 질문 깊이 & 과목 레퍼런스

출처: **KAIST 전산학부 입시(석사 구술면접) 학습자료 2024**. 원본 docx는 `Materials/`(git 제외).
목적: 질문을 **그대로 쓰기 위함이 아니라**, 모의면접에서 도달할 **질문의 깊이(천장)와 과목별 범위**를 보정하기 위함.

> 로컬에 `Materials/_extracted.txt`가 있으면 더 풍부한 질문 풀로 참고. 없으면(타 PC) 이 문서만으로 충분.

---

## 질문 깊이 사다리

각 개념은 **L1에서 시작해 답변에 따라 한 단계씩 깊어진다.** 천장 = **L4(KAIST 구술 수준) 또는 거기서 한 단계 더**(why·증명·반례·실무 연결).

| 레벨 | 성격 | 질문 형태 | 자료 기반 예시 |
|---|---|---|---|
| **L1** 정의·개념 | 용어를 아는가 | "X가 무엇인가?" | "Critical section이란?", "Thread와 process의 차이는?" |
| **L2** 원리·비교 | 어떻게/왜 동작하나 | "어떻게? 왜? A vs B?" | "context switching 과정", "TCP vs UDP" |
| **L3** trade-off·한계 | 장단점·조건·엣지 | "장단점은? 언제 유불리? 한계는?" | "캐시 block size 크게/작게 trade-off", "LRU의 단점" |
| **L4** 적용·증명·계산·설계 | 새 상황 적용·정량 | 시나리오/수식/복잡도/증명/설계 | "Amdahl 계산", "support vector 아닌 데이터 제거 시 SVM 차이", "MST T에 임의 두 정점 최단경로가 반드시 포함되나?" |

**진행 규칙**
- **첫 질문은 항상 L1**(기본 개념)에서 가볍게 연다.
- 답이 충분하면 곧장 **다음 레벨로 꼬리질문**. 꼬리질문 수는 고정하지 않는다 — 천장에 닿거나 사용자가 더 못 들어갈 때까지.
- 막히면: 가벼운 힌트 1회 → 그래도 막히면 **약점 표시 후** 다음 개념으로. (면접 중 정답 강의 금지)
- **깊이 우선**: 한 세션에 개념 1~3개를 천장까지 파는 게 얕은 질문 여러 개보다 낫다.

**에스컬레이션 패턴** (자료의 `→` 체인 그대로):
- "조건부 독립이 무엇인가(L1) → markov chain엔 어떤 조건부 독립이 쓰이나(L2) → 그게 문제가 되는 예시(L4)"
- "SVM 동작 원리(L2) → support vector 아닌 데이터를 모두 제거하고 학습하면 차이는?(L4)"

---

## 과목별 범위 & 천장 앵커

첫 질문은 각 과목 키워드 중 하나를 L1으로. **앵커** = 그 과목에서 끌고 갈 L4 수준 예시.

### OS
키워드: Kernel / Process·Thread·Scheduling / Virtual Memory / Paging·Swapping / Concurrency(Lock·Semaphore·CV) / File System·Crash Consistency
앵커: "paging 시 메모리 2회 참조 문제와 TLB", "hierarchical/inverted page table이 유리한 환경", "세마포어 개념→연산 2가지→구현"

### Architecture (컴퓨터구조)
키워드: ISA / Pipeline·Hazard / Memory Hierarchy·Cache / Virtual Memory / ILP(Superscalar·OoO) / Cache coherence / Multi-core / I/O
앵커: "effective access time 계산", "캐시 block size·associativity trade-off", "Amdahl: 코어 10/∞개, 직렬 20%일 때 speedup"

### 네트워크
키워드: Delay·Loss·Throughput / HTTP·DNS·Streaming / UDP / TCP·Congestion Control / IP·Routing·BGP / Link Layer·Wireless / Network Security
앵커: "congestion 발생을 어떻게 감지하나", "flow control vs congestion control", "checksum용 해시와 무결성용 해시가 interchangeable한가"

### DB
키워드: Relational Model / SQL / ER Model / Normalization / Complex Types / Big Data·NoSQL·Vector DB
앵커: "B+-tree 인덱스로 질의가 빨라지는 원리", "3NF vs BCNF trade-off", "벡터DB가 RAG에 쓰이는 원리"

### 데이터 엔지니어링 *(KAIST 자료 외 보강 항목)*
키워드: ETL vs ELT / 배치 vs 스트리밍 / 분산처리(MapReduce·Spark) / Data Warehouse vs Lake vs Lakehouse / 차원 모델링(Star·Snowflake schema) / OLTP vs OLAP / 파티셔닝·셔플 / 메시지큐·Kafka / 오케스트레이션(Airflow) / CDC / 컬럼너 포맷(Parquet) / 데이터 품질·거버넌스
앵커: "배치 vs 스트리밍 trade-off와 exactly-once 보장", "Spark에서 shuffle이 비싼 이유와 줄이는 법", "OLAP 웨어하우스에서 굳이 비정규화(star schema)를 쓰는 이유"

### 자료구조·알고리즘
키워드: Time Complexity / Sorting / Divide&Conquer / DP / Greedy / Graph algorithms / Advanced DS / NP-completeness
앵커: "quicksort를 worst-case O(n lg n)으로 만들기", "DP로 풀리는데 greedy로 안 되는 예시와 증명", "MST T에 임의 두 정점 최단경로가 반드시 포함되는가"

### PL / Compiler (→ '기타' 분야로 기록)
키워드: Syntax·Semantics / First-class Function / Lazy Evaluation / GC / Type System·Inference / Polymorphism / IR
앵커: "Rust/Java가 C/C++ 메모리 한계를 각각 어떻게 극복했나", "type system의 sound/complete 의미", "var vs let 스코프 차이로 실행결과가 갈리는 이유"

### AI / ML
키워드: Search·CSP / FOL·Planning / ML(Decision Tree·Regression·SVM·Bayesian) / DL(CNN·RNN·Transformer) / RL / NLP·CV / Graph ML / 기초수학(PCA·Cross Entropy·Eigenvalue)
앵커: "Self-Attention의 Q/K/V 역할과 RNN 대비 장점", "On-policy vs Off-policy와 대표 알고리즘", "overfitting 시 polynomial degree를 어떻게·왜"

### 컴퓨터구조 외 — Software Engineering (→ '기타')
키워드: Process Model(Agile·DevOps) / UML·Modeling / Requirements / SE Principles(모듈화·Cohesion·Coupling) / Quality / Testing(black/white-box)
앵커: "화이트박스 테스팅이 무결함을 보장 못 하는 이유", "Cohesion·Coupling 평가", "Verification vs Validation"

### 정보보호 (→ '기타')
키워드: Confidentiality(IV·Nonce) / Integrity(Hash) / Public-key(Diffie-Hellman) / Blockchain / Access Control / Web Security(XSS·CSP) / Buffer Overflow / Program Analysis
앵커: "Diffie-Hellman과 MITM 취약성", "CSP로 XSS를 완벽 방어 가능한가, 아니면 왜", "브라우저로 사이트 접속까지 동작하는 보안기술 전체 순서"

### 이산수학·확률·통계 (→ '기타')
키워드: 논리·증명 / Program Verification(Loop Invariant·Pre/Postcondition) / 집합·관계(동치·순서) / 함수(Bijection) / 귀납법(Strong·Structural) / Counting / 이산확률 / 그래프·트리
앵커: "partial vs total correctness", "Inclusion-Exclusion으로 onto function 개수", "Dijkstra 전제조건"

### 그래픽스 (→ '기타')
키워드: Transformation(Affine·Rigid) / Rotation(Euler·Quaternion·Gimbal lock) / Interpolation / Viewing·Projection / Rasterization / Ray Tracing·BRDF / Shading
앵커: "Gimbal lock과 quaternion", "2D 마우스 입력으로 3D object selection", "BRDF"

### HCI & Human-AI Interaction (→ 'AI·ML' 또는 '기타')
키워드: 인지(Mental Model) / Interaction(Affordance·Signifier·Feedback·Mapping) / Usability·UX·Accessibility / UCD·Iterative Design / Evaluation(A/B·Think-aloud) / Human-AI(Explainability·Trust·Human-in-the-loop·Mixed-initiative) / AI Issues(Bias·Fairness·Overtrust)
앵커: "Affordance vs Signifier", "fairness와 accuracy trade-off를 인터페이스가 어떻게", "Human-in-the-loop가 필요한/불필요한 상황 구분"
