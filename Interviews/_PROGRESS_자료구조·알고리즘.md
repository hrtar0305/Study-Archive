# 자료구조·알고리즘 — 모의면접 진행 현황

> 다른 PC에서 이어서 진행하기 위한 임시 진도 트래커. 세션을 진행하며 갱신한다.
> 최종 갱신: 2026-06-22

---

## 다룬 개념 (완료)

| 날짜 | 개념 | 이해도 | 핵심 약점 |
|---|---|---|---|
| 06-21 | 해시 테이블 | 🟢 충분 | probing 종류·clustering, load factor 정의 |
| 06-21 | 다익스트라 | 🟡 보통 | O(E log V) 유도, 비음 조건이 증명에 쓰이는 지점 |
| 06-21 | 정렬 | 🟡 보통 | worst-case O(NlogN) 보장(Introsort), Ω(NlogN) 하한 정량화, Radix sort |
| 06-22 | 그리디 | 🟡 보통 | Greedy Choice Property/Optimal Substructure 용어, 교환 논증 |
| 06-22 | DP | 🟢 충분 | overlapping subproblems 정의 정밀도 (해소됨) |
| 06-22 | 배열 (Array) | 🟢 충분 | 동적 배열 amortized O(1) 즉시 상기, 행렬 곱 타일링 |

---

## 남은 범위 (예정)

### 기본 자료구조 — **다음 진행 예정: 연결 리스트부터**
- [ ] **Linked List** (단일·이중·원형) — 배열과의 trade-off, 캐시 측면
- [ ] **Stack / Queue / Deque** — 구현 방식, 활용
- [ ] **Tree 기초** — 순회(전위·중위·후위·레벨), 표현 방식
- [ ] **Graph 표현** — 인접 행렬 vs 인접 리스트

### 고급 자료구조
- [ ] **BST / AVL / Red-Black Tree** — 균형 유지, 회전
- [ ] **B-tree / B+-tree** — 디스크 기반, DB 인덱스 연결
- [ ] **Heap (Priority Queue)** — 힙 연산, 힙 정렬 연결
- [ ] **Trie** — 문자열 탐색
- [ ] **Union-Find (Disjoint Set)** — 경로 압축, union by rank

### 알고리즘
- [ ] **Time Complexity** — Big-O/Ω/Θ, amortized 분석 종합
- [ ] **Divide & Conquer** — 마스터 정리, 대표 문제
- [ ] **Graph 알고리즘** — BFS/DFS, MST(크루스칼·프림), 위상 정렬, SCC, 최단경로 종합
- [ ] **NP-completeness** — P vs NP, NP-hard/NP-complete, reduction

---

## 복습 우선순위 (🟡 이하 우선)
1. **다익스트라** — O(E log V) 유도, 비음 조건 증명 지점
2. **정렬** — Introsort/하한 정량화/Radix sort
3. **그리디** — 교환 논증 (DP 세션에서 일부 해소)

> 기록 규칙은 [_PROTOCOL.md](_PROTOCOL.md) 참고. 각 개념은 Notion 개념 노트 ②와 학습 로그 ①에 누적됨.
