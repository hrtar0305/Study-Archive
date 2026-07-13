# 2026-07-07 자료구조·알고리즘 — 모의면접 (Time Complexity, Sorting)

- **유형**: 모의면접
- **분야**: 자료구조·알고리즘
- **날짜**: 2026-07-07

---

## 개념: Time Complexity

### Q1. Big-O란 무엇인가
- **내 답변 요약**: 알고리즘 실행 시간의 상한을 표기하는 것. O(N²)이면 어떤 경우에도 N²보다 적거나 같은 시간.
- **평가**: 상한이라는 방향은 정확. "어떤 경우에도"라는 표현은 Big-O가 특정 case와 무관하게 그 case 안에서의 상한임을 뜻한다는 점에서 약간 느슨.

### Q2. Ω과 Θ의 차이
- **내 답변 요약**: Ω는 하한, Θ는 "그 사이".
- **평가**: Ω=하한은 정확. Θ를 "사이"로 답했으나 정확히는 "상한과 하한이 같은 차수로 조여진 상태"(tight bound).

### Q3. Θ = 평균 시간? (핵심 약점)
- **내 답변 요약**: Θ를 "평균적인 시간을 표현하는 방법"이라고 답변. 힌트(표기법과 case가 같은 축인지) 이후에도 "표기법은 worst case를 가정한 것"이라는 식으로 부분적 혼동 지속.
- **모범답안**: O/Ω/Θ(표기법)와 best/average/worst case(입력 시나리오)는 서로 독립적인 두 축. 예: 퀵소트는 worst case가 Θ(n²), average case가 Θ(n log n) — worst에도 average에도 모두 Θ(tight bound)를 쓸 수 있다는 것이 두 축이 독립적이라는 증거. 관용적으로 "O(n log n)"이라 하면 보통 average case를, "O(n²)"이라 하면 보통 worst case를 캐주얼하게 가리키는 관행일 뿐, 표기법 자체의 정의는 아니다.
- **보충 예시 (사용자 요청)**:

| 알고리즘 | best case | average case | worst case |
|---|---|---|---|
| 선형 탐색 | Θ(1) | Θ(n) | Θ(n) |
| Quicksort (첫 원소 pivot) | Θ(n log n) | Θ(n log n) | Θ(n²) (정렬된 입력) |
| BST 탐색 (불균형 가능) | Θ(1) | Θ(log n) (균형 가정) | Θ(n) (편향 트리) |

  - Formal 정의: O(f(n)) = ∃ c>0, n₀ s.t. n≥n₀일 때 T(n) ≤ c·f(n) (상한만). Ω(f(n)) = 하한만. Θ(f(n)) = 둘 다 동시 성립.

### 약점·복습포인트 (Time Complexity)
- 표기법(O/Ω/Θ)과 case(best/avg/worst)를 같은 축으로 혼동 — "Θ = 평균"이라는 오해
- Θ는 "상한=하한이 같은 차수로 조여진 tight bound"이지 case를 지칭하는 말이 아님
- 관용적 O 사용(캐주얼하게 worst/average 지칭)과 형식적 정의를 구분할 것

### 이해도: 🟡 보통

---

## 개념: Sorting

### Q1. 정렬 알고리즘 분류
- **내 답변 요약**: O(N²) 그룹(insertion/selection/bubble) vs O(NlogN) 그룹(heap/merge/quick).
- **평가**: 정확.

### Q2~Q3. quicksort worst-case
- **내 답변 요약**: quicksort는 항상 O(NlogN)이 아니며 최악의 경우 O(N²).
- **평가**: 정확.

### Q4. 고정 pivot + 정렬된 입력, 완화책
- **내 답변 요약**: 첫 원소 고정 pivot + 정렬된 입력 → 매 단계 1개만 분리되어 비효율. 완화책으로 median-of-three(첫·중·끝 median을 pivot).
- **평가**: 정확.

### Q5. median-of-three가 worst-case를 보장하는가
- **내 답변 요약**: 보장 안 됨, 완화책일 뿐. quicksort는 pivot 랜덤성 전제상 성능 이슈를 완전히 피할 수 없어 실제로는 일정 깊이 이상에서 다른 정렬로 전환.
- **평가**: 정확하고 우수(스스로 짚음).

### Q6. 전환 기법의 이름 (약점 → 정정됨)
- **내 답변 요약**: 처음 "Powersort"라 답 → 힌트("intro-로 시작, in-place 보장 알고리즘") 후 "Introsort, heap sort로 전환"으로 정정. Timsort가 insertion sort를 쓴다는 것도 구분해냄.
- **모범답안**: Introsort(Musser, 1997) — quicksort로 시작, 재귀 깊이가 `2⌊log₂N⌋`를 초과하면 그 구간만 **heap sort**로 전환해 worst-case O(NlogN)을 보장한다. 배열 재배치는 in-place지만 재귀 스택은 일반적으로 O(logN)이다. 작은 부분배열은 **insertion sort**로 전환한다. Timsort(Python/Java 객체 정렬)는 natural run을 활용해 병합하는 별개의 안정 정렬 하이브리드다. Powersort는 CPython에서 run 병합 순서를 정하는 정책이다.

### Q7. Stable의 정의
- **내 답변 요약**: 정렬 이후 기존 상대적 순서가 유지되는 성질.
- **평가**: 정확.

### Q8. Stable이 왜 중요한가 (약점)
- **내 답변 요약**: "DB에서의 스캔 성능" → 힌트(다중 키 정렬 시나리오) 후에도 "2차 키로 재정렬 시 1차 키 순서가 깨지면 range query 결과를 원하는 대로 못 얻음"이라는 식으로 순서가 다소 뒤바뀐 채 설명.
- **모범답안**: 안정 정렬의 실무 가치는 **다중 키 정렬(multi-key sort)**. 덜 중요한 키로 먼저 정렬 → 더 중요한 키로 나중에 안정 정렬하면, 같은 키 값 안에서 이전 정렬 순서가 보존되어 커스텀 비교자 없이 다중 키 정렬이 가능해짐. 이건 성능이 아니라 **순서의 정확성/일관성** 문제.

### Q9. Ω(NlogN) 하한 (반복 약점)
- **내 답변 요약**: "N의 시간과 logN 깊이" 정도로만 어렴풋이 답 → 힌트 후에도 "각 단계 최대 절반으로 나뉜다" 정도만 기억 → 결정 트리가 실행 중 가지치기인지, 각 노드가 뭘 비교하는지 반문.
- **모범답안**: 결정 트리는 실행 중 자료구조가 아니라, **어떤 고정된 알고리즘이 모든 가능한 입력에 대해 가질 수 있는 모든 실행 경로를 미리 펼쳐 그린 이론적 증명 도구**. 각 내부 노드는 그 알고리즘이 그 시점에 수행하는 비교 하나(다음 비교 대상은 알고리즘 코드가 정함), 리프는 확정된 하나의 순열. N개 원소의 가능한 순열이 N!가지이므로 최소 N!개의 리프 필요 → 이진트리 높이 `h`는 `2^h ≥ N!` → `h ≥ log₂(N!) = Θ(NlogN)`. 트리 높이 = worst-case 비교 횟수.
- **예시(N=3, a·b·c)**: root에서 a vs b 비교 → 결과에 따라 b vs c 또는 a vs c로 분기 → 최종 6(=3!)개 리프에서 6가지 순열이 각각 확정.
- **재복습 필요**: 이 개념은 이전 세션에서도 헷갈렸던 반복 약점.

### Q10~Q12. 하한을 깨는 방법, Bucket vs Counting sort (명칭 혼동 → 정정됨)
- **내 답변 요약**: 비교 없이 값 자체를 인덱스로 쓰는 정렬(counting/bucket 등)로 하한 회피 가능 — 방향 정확. 처음 "bucket sort"라 설명한 것이 실제로는 counting sort(값마다 카운터 하나, O(N+K))였음 → 힌트 후 스스로 정정. 이어서 진짜 bucket sort(구간별 버킷에 담아 내부 정렬 후 이어붙임)도 정확히 설명.
- **모범답안**: Counting sort = 값 하나당 카운터 하나(이산 도메인, O(N+K)). Bucket sort = 값을 구간(버킷)으로 나눠 각 버킷 내부를 별도 정렬(보통 insertion sort) 후 이어붙임 — 균등 분포 실수 데이터에 유리.

### 사용자 질문 — 정렬의 캐시 효율성
- **캐시 친화적**: Insertion sort(작은 window 순차 접근), Quicksort(양끝→안쪽 순차 스캔, in-place).
- **캐시 비친화적**: Heap sort — sift-down/up의 인덱스(i, 2i, 2i+1) 관계가 배열이 커지면 메모리상 멀리 떨어져 캐시 미스 빈번. O(NlogN) worst-case 보장·O(1) 공간에도 실측 성능은 quicksort보다 떨어짐.
- Merge sort는 merge 자체는 순차적이나 O(N) 보조 배열 복사 비용 있음.
- **실무 함의**: Introsort가 평상시 quicksort(캐시 친화적)를 쓰고 worst-case 보장이 필요할 때만 heap sort로 전환하는 이유 — 이론상 동일 Θ(NlogN)이어도 캐시 효율 차이로 실측 성능이 크게 갈림.

### 약점·복습포인트 (Sorting)
- Ω(NlogN) 결정 트리 증명을 스스로 유도하지 못함 (반복 약점, 재복습 필요)
- Stable 정렬의 실무 가치(다중 키 정렬)를 성능 문제로 오해
- Counting sort와 Bucket sort 명칭 혼동
- (해소됨) quicksort worst-case 조건, Introsort/Timsort/Powersort 구분, 캐시 효율성

### 이해도: 🟡 보통
