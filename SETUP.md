# SETUP — 다른 PC / 계정에서 동일하게 구성하기

이 학습 아카이브 시스템을 새 환경에서 재현하는 절차다.

## 0. 사전 준비
- Windows + Claude 데스크톱 앱 (**Code** 표면 사용)
- 저장소 클론: `git clone https://github.com/hrtar0305/Study-Archive.git`

## 1. 작업 폴더에서 Claude Code 실행
클론한 폴더를 Claude Code에서 연다. `.claude/settings.json`의 권한 잠금이 자동 적용된다.
> ⚠️ 드라이브 문자/경로가 다르면 `.claude/settings.json`의 `deny` 경로를 본인 환경에 맞게 수정.

## 2. 커넥터 연결
Claude 앱 → 설정 → 커넥터에서 **Notion**(필요하면 GitHub도) 연결 (OAuth).

## 3. Notion DB 생성 (새 계정이면 필수)
새 워크스페이스엔 DB가 없으므로 새로 만든다. Claude Code에 이렇게 요청:
> "최상위에 'CS & 면접 학습 아카이브' 페이지를 만들고, 그 아래에 'CS 학습 로그' DB를 아래 스키마로 만들어줘."

**스키마(속성):**
- 제목(Title), 날짜(Date)
- 유형(Select): `자료정리` / `모의면접`
- 분야(Select): `OS` / `네트워크` / `DB` / `자료구조·알고리즘` / `컴퓨터구조` / `AI·ML` / `기타`
- 이해도(Select): `🔴 부족` / `🟡 보통` / `🟢 충분`
- 약점·복습포인트(Text)
- 블로그 후보(Checkbox)

## 4. CLAUDE.md의 ID 갱신
생성 후 받은 **Data source ID**를 [CLAUDE.md](CLAUDE.md)의 `Data source ID:` 줄에 덮어쓴다.
(이 ID는 워크스페이스마다 다르다.)

## 5. 완료
이제 동작한다:
- **"시작"** → 지난 진도·약점 브리핑
- **"자료정리"** 또는 자료 업로드 → 구조화 정리
- **"모의면접"** → 면접 연습 + 약점 진단
- **"기록"** → Notion + 로컬에 저장

---

## 현재 환경 참고값 (원본 계정)
| 항목 | 값 |
|---|---|
| Notion 워크스페이스 | JY의 Notion HQ |
| 허브 페이지 | https://app.notion.com/p/38415050b8b081c5ac98d1db6573cc8b |
| DB | https://app.notion.com/p/bcb3b2fc7184470cbe3fdfbb3c5268de |
| Data source ID | `8f362694-fac3-46a7-9e89-f39f77693caf` |
