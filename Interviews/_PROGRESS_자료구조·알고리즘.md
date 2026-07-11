# 자료구조·알고리즘 — 모의면접 진행 현황

> 다른 PC에서 이어서 진행하기 위한 진도 트래커(git 추적). 세션을 진행하며 갱신한다.
> 최종 갱신: 2026-07-09

---

## 다룬 개념 (완료)

| 날짜 | 개념 | 이해도 | 핵심 약점 |
|---|---|---|---|
| 06-21 | 해시 테이블 | 🟢 충분 | probing 종류·clustering, load factor 정의 |
| 06-21 | 다익스트라 | 🟡 보통 | O(E log V) 유도, 비음 조건이 증명에 쓰이는 지점 (07-09 그래프 세션서 해소) |
| 06-21 | 정렬 | 🟡 보통 | worst-case O(NlogN) 보장(Introsort), Ω(NlogN) 하한 정량화, Radix sort |
| 06-22 | 그리디 | 🟡 보통 | Greedy Choice Property/Optimal Substructure 용어, 교환 논증 |
| 06-22 | DP | 🟢 충분 | overlapping subproblems 정의 정밀도 (해소됨) |
| 06-22 | 배열 (Array) | 🟢 충분 | 동적 배열 amortized O(1) 즉시 상기, 행렬 곱 타일링 |
| 06-23 | 트리 기초 | 🟡 보통 | 순회(전위·중위·후위·레벨), 표현 방식 |
| 07-07 | Time Complexity | 🟡 보통 | **Θ를 "평균 시간"으로 혼동 (미해소)**, Θ=tight bound 정의 |
| 07-09 | BST / 균형트리(AVL·RB) / B-tree | 🟢 충분 | AVL vs RB 회전 정량 차이, B-tree=블록 I/O에 노드 크기 맞춤 |
| 07-09 | 그래프 (표현·BFS/DFS·최단경로) | 🟢 충분 | 벨만-포드 O(VE) 즉시 상기, 인접 리스트 공간 O(V+E) |
| 07-09 | 유니온-파인드 | 🟡 보통 | union by rank/size 방향, α(N)=역아커만, 두 최적화 병행 필요 |
| 07-09 | 힙 (Heap) | 🟢 충분 | (거의 없음) 완전 이진 트리 용어, heapify O(N) 증명 |

---

## 남은 범위 (예정)

### 기본 자료구조 — **다음 진행 예정: 연결 리스트부터**
- [ ] **Linked List** (단일·이중·원형) — 배열과의 trade-off, 캐시 측면
- [ ] **Stack / Queue / Deque** — 구현 방식, 활용
- [x] ~~Tree 기초~~ — 06-23 완료
- [x] ~~Graph 표현~~ — 07-09 완료 (인접 행렬 vs 리스트)

### 고급 자료구조
- [x] ~~BST / AVL / Red-Black Tree~~ — 07-09 완료
- [x] ~~B-tree / B+-tree~~ — 07-09 완료 (기초)
- [x] ~~Heap (Priority Queue)~~ — 07-09 완료
- [ ] **Trie** — 문자열 탐색
- [x] ~~Union-Find (Disjoint Set)~~ — 07-09 완료

### 알고리즘
- [x] ~~Time Complexity~~ — 07-07 완료 (**단, Θ 혼동 복습 필요**)
- [ ] **Divide & Conquer** — 마스터 정리, 대표 문제
- [ ] **Graph 알고리즘** — MST(크루스칼·프림), 위상 정렬, SCC (최단경로는 07-09 완료)
- [ ] **NP-completeness** — P vs NP, NP-hard/NP-complete, reduction

---

## 복습 우선순위 (🟡 이하 우선)
1. **Time Complexity — Θ ≠ 평균시간** (07-07 미해소, 최우선)
2. **유니온-파인드** — union 방향(작은 트리 → 큰 트리 아래), α(N)=역아커만
3. **트리 기초** — 순회 표현
4. **정렬** — Introsort/하한 정량화/Radix sort
5. **그리디** — 교환 논증 (DP 세션에서 일부 해소)

> 기록 규칙은 [_PROTOCOL.md](_PROTOCOL.md) 참고. 각 개념은 Notion 개념 노트 ②와 학습 로그 ①에 누적됨.
