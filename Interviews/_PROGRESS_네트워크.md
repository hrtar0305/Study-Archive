# 네트워크 — 모의면접 진행 현황

> 다른 PC에서 이어서 진행하기 위한 진도 트래커.
> 최종 갱신: 2026-08-03 (07-25 ~ 07-30 세션 13건을 역으로 정리)
> ⚠️ 네트워크는 **외부 스터디에서 면접자로 참여**한 세션이 대부분이라 면접관용 질문 세트(`_CHECKLIST_네트워크.md`)는 작성하지 않았다. 이 파일은 진도·약점 추적 전용.

---

## 다룬 개념

| 날짜 | 개념 | 이해도 | 핵심 약점 |
|---|---|---|---|
| 07-25 | DNS | 🟡 보통 | 스텁·재귀 리졸버 역할 반대로 답변, 재귀 질의와 반복 질의 구간, UDP·TCP 53번, TC 비트와 TCP fallback, 캐시 포이즈닝의 트랜잭션 ID·출발지 포트 |
| 07-25 | TCP 신뢰성·혼잡 제어 | 🟡 보통 | rwnd·cwnd·MSS·ssthresh·RTO 용어, 중복 ACK 3회의 의미, Fast Retransmit·Fast Recovery, AIMD의 cwnd·ssthresh 조정, SRTT·RTTVAR 기반 RTO |
| 07-26 | OSI 7계층·TCP/IP 모델 | 🟡 보통 | 네트워크 계층과 인터넷 계층 명칭, 세션·표현 계층 역할, TCP 연결과 애플리케이션 세션 구분, PDU 순서, 두 모델의 비대응 |
| 07-26 | IP 주소와 라우팅 | 🔴 → 🟡 | 면접 시 🔴, 후속 학습 후 🟡. IP는 호스트가 아닌 인터페이스에 할당, 라우팅과 포워딩 차이, Longest Prefix Match, ARP·이웃 테이블 구분, CIDR·서브넷 계산 |
| 07-26 | 이더넷 스위칭 | 🔴 부족 | L2 스위치와 L3 라우터 비교, ARP와 MAC 학습의 주체 혼동, 출발지 MAC 학습·목적지 MAC 전달, unknown unicast flooding과 브로드캐스트 구분, 충돌·브로드캐스트 도메인 |
| 07-26 | DHCP | 🔴 부족 | DHCP와 NAT 역할 혼동, DORA 메시지 이름·목적, Request가 브로드캐스트되는 이유, UDP 67·68번, 임대 갱신·만료, Relay Agent |
| 07-26 | NAT | 🟡 보통 | NAT와 NAPT·PAT 용어, NAT 테이블의 프로토콜·IP·포트 매핑, 동적 매핑과 포트 포워딩 차이, IPv4 헤더 체크섬 범위, TCP·UDP 체크섬의 의사 헤더 |
| 07-26 | HTTP와 HTTPS | 🟡 보통 | request line·status line 구분, stateless와 서버 세션의 양립, 301·302·307·308, 인증서 체인과 CA, 서버 인증(개인키)과 ECDHE 키 합의 구분, HTTP/2 TCP HOL과 HTTP/3 QUIC, ETag·조건부 요청 |
| 07-27 | 네트워크 성능(지연·손실·처리량) | 🟡 보통 | 처리·큐잉·전송·전파 지연 명칭, 전송 지연 L/R과 전파 지연 d/s, 단위 변환, 사용률 100%와 버퍼 포화 구분, 파이프라이닝의 첫 패킷 지연과 도착 간격, 병목 링크 |
| 07-30 | 라우팅과 포워딩 | 🔴 부족 | 라우팅을 출발지에서만 수행한다고 오해, 동적 라우팅과 패킷별 재계산 혼동, 제어 평면·데이터 평면, RIB와 FIB 역할 분리, 장애 감지와 라우팅 메시지 전파 |
| 07-30 | BGP | 🔴 부족 | AS·ASN, eBGP·iBGP, 정책 우선 경로 선택, TCP 179와 메시지 4종, NLRI·NEXT_HOP·LOCAL_PREF·AS_PATH·MED, AS_PATH 루프 방지, iBGP full mesh와 Route Reflector, RPKI |
| 07-30 | 무선 네트워크와 Wi-Fi | 🔴 부족 | 공유 채널·airtime과 스위치드 이더넷 차이, 송신 중 충돌 감지 불가 이유, CSMA/CA, 숨은·노출 단말과 RTS/CTS·NAV, SSID·BSSID, 대역·채널 폭 trade-off, WPA2·WPA3, MIMO·OFDMA |
| 07-30 | 포트와 소켓 | 🟡 보통 | 포트를 프로세스 고정 주소로 표현, 소켓을 API 이름으로만 이해, multiplexing·demultiplexing 방향, 리스닝 소켓과 연결 소켓, UDP의 recvfrom·sendto |
| 07-30 | SOP와 CORS | 🟡 보통 | Origin = scheme+host+port(초기엔 IP·포트만 답변), 교차 출처 form 제출 허용 범위, Origin·Access-Control-Allow-Origin 헤더와 preflight 미답변, SOP를 서버 방어선이 아닌 브라우저 격리 경계로 이해 |

## 재면접·재학습 필요

- [ ] **BGP** — 07-30 최초 노출, 전 범위 설명형으로 진행. 학습 후 실전 답변으로 재검증 필요
- [ ] **라우팅과 포워딩** — 07-30 🔴. 제어/데이터 평면·RIB/FIB 재학습 후 재면접
- [ ] **무선 네트워크와 Wi-Fi** — 07-30 🔴. 추가 범위를 설명형으로 기록했으므로 실전 재평가 필요
- [ ] **이더넷 스위칭** — 07-26 🔴. ARP와 MAC 학습 주체 구분부터 재확인
- [ ] **DHCP** — 07-26 🔴. DORA·포트·Relay 재학습 후 재면접

## 남은 범위 (잠정)

> 네트워크는 외부 스터디 일정에 따라 주제가 정해지므로 아래는 확정 커리큘럼이 아니라 **아직 다루지 않은 것으로 확인된 주제** 목록이다. 스터디 진행에 맞춰 갱신할 것.

- [ ] TCP 연결 종료와 상태 전이 — 4-way handshake, TIME_WAIT, 좀비 연결 (3-way handshake는 07-25에 다룸)
- [ ] IPv6 — 주소 체계, 전환 기술 (07-26 IP 세션은 IPv4 중심)
- [ ] 로드 밸런싱·리버스 프록시·CDN — L4/L7 분기, 캐시 계층
- [ ] VPN·터널링 — 캡슐화, IPsec
- [ ] 방화벽·패킷 필터링 — stateful inspection (NAT는 07-26에 다룸)
- [ ] QUIC 상세 — 07-26 HTTP/3 문맥에서만 언급, 핸드셰이크·스트림 독립성은 미검증
- [ ] TLS 핸드셰이크 상세 — 07-26에 인증서·ECDHE는 다뤘으나 1.2/1.3 절차 차이는 미검증

## 복습 우선순위

1. **라우팅과 포워딩** — 각 라우터가 자기 관점에서 경로를 계산, 제어 평면(RIB)과 데이터 평면(FIB) 분리, RIB → FIB 설치 → 패킷별 LPM
2. **BGP 기본 구조** — AS·ASN, eBGP와 iBGP, 최단거리가 아닌 정책 기반 경로 선택
3. **BGP 속성과 동작** — AS_PATH 루프 방지, NEXT_HOP의 IGP 해석, withdraw와 수렴, Route Reflector
4. **CSMA/CA와 무선 매체** — 송신 중 충돌 감지가 어려운 이유, carrier sense·랜덤 backoff·ACK, 숨은 단말과 RTS/CTS·NAV
5. **L2 스위칭** — 출발지 MAC으로 학습하고 목적지 MAC으로 전달, unknown unicast flooding과 브로드캐스트의 차이
6. **ARP vs MAC 주소 테이블** — ARP는 호스트가 IP→MAC을 묻는 것, MAC 테이블은 스위치가 MAC→포트를 학습하는 것
7. **DHCP DORA** — Discover·Offer·Request·Ack의 목적, Request가 브로드캐스트되는 이유, UDP 67(서버)·68(클라이언트)
8. **CIDR·서브넷 계산** — prefix와 마스크, 네트워크·브로드캐스트·호스트 범위, 같은/다른 서브넷의 IP·MAC 목적지 차이
9. **Longest Prefix Match** — 목적지 IP 기준 최장 일치, BGP 경로 선택과 혼동하지 말 것
10. **TCP 혼잡 제어 정량** — Slow Start의 ssthresh 도달은 선형 증가 전환, 중복 ACK 3회와 타임아웃의 cwnd·ssthresh 조정 차이
11. **RTO 계산** — SRTT·RTTVAR 기반 산출, 중복 ACK와 타임아웃의 신호 강도 차이
12. **DNS 리졸버 구조** — 스텁 리졸버(OS)와 재귀 리졸버(ISP·공용), 재귀 질의와 반복 질의의 구간
13. **DNS 전송** — UDP·TCP 모두 53번, TC 비트 시 TCP 재질의, zone transfer는 TCP
14. **DoH vs DNSSEC** — 경로 암호화(기밀성)와 출처·무결성 검증은 서로 다른 문제
15. **네트워크 지연 4요소** — 처리·큐잉·전송(L/R)·전파(d/s)의 결정 요인과 단위 변환
16. **처리량과 병목** — 정의, 병목 링크 판정, 파이프라이닝의 첫 패킷 지연과 이후 도착 간격 구분
17. **NAT 테이블** — 변환 전후 튜플을 숫자로 제시하기, 동적 매핑과 포트 포워딩의 방향 차이
18. **체크섬 범위** — IPv4 헤더 체크섬은 헤더만, TCP·UDP 체크섬은 의사 헤더 포함
19. **HTTPS 키 교환** — 인증서 개인키의 서버 인증과 ECDHE 세션 키 합의는 별개, forward secrecy
20. **HTTP 상태 코드** — 301·302와 307·308의 메서드 보존 차이, 304와 조건부 요청(ETag·Last-Modified)
21. **HTTP/2 vs HTTP/3** — TCP 레벨 HOL blocking과 QUIC 스트림 독립성
22. **포트와 소켓** — 포트는 소켓을 찾는 헤더 값, 소켓은 커널이 관리하는 상태·버퍼를 가진 객체
23. **연결 식별** — 프로토콜 + 양 끝 IP·포트, 리스닝 소켓과 accept()가 반환한 연결 소켓 구분
24. **CORS 헤더** — Origin(브라우저)과 Access-Control-Allow-Origin(서버), 비단순 요청의 OPTIONS preflight
25. **SOP의 성격** — 요청 전송 차단이 아니라 응답·DOM 읽기 제한, 서버 방어선이 아닌 브라우저 내부 격리 경계
26. **OSI·TCP/IP 대응** — 네트워크 계층과 인터넷 계층 명칭, 세션·표현 계층, 두 모델은 일대일 대응이 아님

> 질문 깊이 기준은 [_DEPTH_REFERENCE.md](_DEPTH_REFERENCE.md), 기록 규칙은 [_PROTOCOL.md](_PROTOCOL.md) 참고.
