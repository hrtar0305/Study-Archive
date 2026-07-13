# 자료구조·알고리즘 — 모의면접 진행 현황

> 다른 PC에서 이어서 진행하기 위한 진도 트래커(git 추적). 세션을 진행하며 갱신한다.
> 최종 갱신: 2026-07-13

---

## 다룬 개념 (완료)

| 날짜 | 개념 | 이해도 | 핵심 약점 |
|---|---|---|---|
| 06-21 | 해시 테이블 | 🟢 충분 | probing 종류·clustering, load factor 정의 |
| 06-21 | 다익스트라 | 🟡 보통 | O(E log V) 유도, 비음 조건이 증명에 쓰이는 지점 (07-09 그래프 세션서 해소) |
| 06-21 | 정렬 | 🟡 보통 | worst-case O(NlogN) 보장(Introsort), Ω(NlogN) 하한 정량화, Radix sort |
| 06-22 | 그리디 | 🟡 보통 | Greedy Choice Property/Optimal Substructure 용어, 교환 논증 |
| 06-22 | DP | 🟢 충분 | overlapping subproblems 정의 정밀도 (해소됨) |
| 06-22 | 배열 (Array) | 🟢 충분 | 동적 배열 amortized O(1)을 바로 떠올리기, 행렬 곱 타일링 |
| 06-23 | 트리 기초 | 🟡 보통 | 순회(전위·중위·후위·레벨), 표현 방식 |
| 07-07 | Time Complexity | 🟡 보통 | **Θ를 "평균 시간"으로 혼동 (미해소)**, Θ=tight bound 정의 |
| 07-09 | BST / 균형트리(AVL·RB) / B-tree | 🟢 충분 | AVL vs RB 회전 정량 차이, B-tree=블록 I/O에 노드 크기 맞춤 |
| 07-09 | 그래프 (표현·BFS/DFS·최단경로) | 🟢 충분 | Bellman-Ford O(VE)를 바로 떠올리기, 인접 리스트 공간 O(V+E) |
| 07-09 | 유니온-파인드 | 🟡 보통 | union by rank/size 방향, α(N)=역아커만, 두 최적화 병행 필요 |
| 07-09 | 힙 (Heap) | 🟢 충분 | (거의 없음) 완전 이진 트리 용어, heapify O(N) 증명 |
| 07-11 | 연결 리스트 | 🟢 충분 | O(1) 삭제 우회 트릭의 노드 identity·dangling reference 한계 |
| 07-11 | 스택 / 큐 / 덱 | 🟡 보통 | **0-1 BFS 거리 불변식 증명 미해소** |
| 07-11 | Trie | 🟢 충분 | 압축 트라이(Radix/Patricia) 바로 떠올리기 |
| 07-11 | 분할 정복 | 🟡 보통 | **Master Theorem Case 2 미해소**, closest pair의 y좌표 순 유지·packing argument |
| 07-11 | MST / 위상정렬 / SCC | 🟡 보통 | **배열 기반 Prim O(V²), Kosaraju/Tarjan 미해소** |
| 07-13 | 해시 테이블 재면접 | 🟡 보통 | **load factor 정의, primary/secondary clustering, hash flooding 방어·treeification** |
| 07-13 | DP 재면접 | 🟡 보통 | **0/1 Knapsack 1차원 최적화의 내림차순 순회, Unbounded Knapsack과 구분** |
| 07-13 | 그리디 재면접 | 🔴 부족 | **greedy choice property 미회상, exchange argument를 조건과 혼동** |
| 07-13 | 배열·동적 배열 재면접 | 🟡 보통 | **고정량 c 확장 총복사 Θ(N²/c), cache prefetch·pointer chasing 설명** |
| 07-13 | 트리 기초 재면접 | 🟡 보통 | **depth·height·degree, full·complete 구분, N-1간선 비순환성 증명** |

---

## 남은 범위 (예정)

### 기본 자료구조
- [x] ~~Linked List~~ — 07-11 완료
- [x] ~~Stack / Queue / Deque~~ — 07-11 완료 (0-1 BFS 증명 복습 필요)
- [x] ~~Tree 기초~~ — 06-23 완료
- [x] ~~Graph 표현~~ — 07-09 완료 (인접 행렬 vs 리스트)

### 고급 자료구조
- [x] ~~BST / AVL / Red-Black Tree~~ — 07-09 완료
- [x] ~~B-tree / B+-tree~~ — 07-09 완료 (기초)
- [x] ~~Heap (Priority Queue)~~ — 07-09 완료
- [x] ~~Trie~~ — 07-11 완료
- [x] ~~Union-Find (Disjoint Set)~~ — 07-09 완료

### 알고리즘
- [x] ~~Time Complexity~~ — 07-07 완료 (**단, Θ 혼동 복습 필요**)
- [x] ~~Divide & Conquer~~ — 07-11 완료 (Master Theorem Case 2 복습 필요)
- [x] ~~Graph 알고리즘~~ — 07-11 완료 (배열 기반 Prim·SCC 알고리즘 복습 필요)
- [ ] **NP-completeness** — P vs NP, NP-hard/NP-complete, reduction

---

## 복습 우선순위 (🟡 이하 우선)
1. **그리디** — greedy choice property와 optimal substructure 구분, exchange argument는 증명 기법
2. **0-1 BFS** — 덱 안 정점의 거리 label이 d 또는 d+1로 유지되는 불변식 증명
3. **DP** — 상태·점화식·base case·계산 순서, 0/1 Knapsack 내림차순 vs Unbounded Knapsack 오름차순
4. **배열·동적 배열** — 고정량 c 확장 총복사 Θ(N²/c), cache line·prefetcher·pointer chasing
5. **트리 기초** — depth·height·degree, full·complete·perfect 구분, N-1간선 비순환성 증명
6. **분할 정복** — Master Theorem Case 2, Merge Sort의 f(N)=Θ(N)
7. **그래프 알고리즘** — 배열 기반 Prim O(V²), Kosaraju/Tarjan SCC
8. **해시 테이블** — load factor α=N/M, primary/secondary clustering, keyed hash와 균형 BST treeification
9. **Time Complexity** — Θ는 average case가 아니라 tight bound
10. **유니온-파인드** — union 방향, 역 아커만 함수
11. **정렬** — 비교 정렬 하한, BFPRT pivot 보장, Radix sort

> 기록 규칙은 [_PROTOCOL.md](_PROTOCOL.md) 참고. 각 개념은 Notion 개념 노트 ②와 학습 로그 ①에 누적됨.
