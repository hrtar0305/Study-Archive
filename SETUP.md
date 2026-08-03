# SETUP — 다른 PC / 계정에서 동일하게 구성하기

이 학습 아카이브 시스템을 새 환경에서 재현하는 절차다.

## 0. 사전 준비
- Windows + Claude 데스크톱 앱 (**Code** 표면 사용)
- 저장소 클론: `git clone https://github.com/hrtar0305/Study-Archive.git`

## 1. 작업 폴더에서 Claude Code 실행
클론한 폴더를 Claude Code에서 연다. `.claude/settings.json`의 권한 잠금이 자동 적용된다.
> ⚠️ 드라이브 문자/경로가 다르면 `.claude/settings.json`의 `deny` 경로를 본인 환경에 맞게 수정.

## 2. Notion 연결

연결 방식이 두 가지이고, **Claude 계정이 개인 것이냐에 따라 갈린다.**

### 2-A. 개인 Claude 계정일 때 — 앱 커넥터
Claude 앱 → 설정 → 커넥터에서 **Notion** 연결 (OAuth).
- 간편하지만 **승인 기록이 Claude 계정에 저장**되어 같은 계정으로 로그인한 모든 기기·사용자에게 따라간다.

### 2-B. 공용·조직 Claude 계정일 때 — 로컬 MCP (권장)
계정이 아니라 **이 PC에만** 연결을 남긴다.

```bash
claude mcp add --scope local --transport http notion https://mcp.notion.com/mcp
claude mcp login notion
```

- `--scope local` = `~/.claude.json`의 **이 프로젝트 경로 아래**에만 저장. 저장소에 커밋되지 않고 다른 기기로 따라가지 않는다.
- `claude mcp login`은 브라우저 OAuth를 띄운다. **Notion 계정 로그인은 본인이 직접** 한다.
- 확인: `claude mcp get notion` → `Status: ✔ Connected`
- 정리: `claude mcp logout notion` (자격증명만 삭제) / `claude mcp remove notion -s local` (설정까지 삭제)

> ⚠️ **`--scope project`는 쓰지 말 것.** `.mcp.json`을 만들어 공유 저장소에 올린다. (`.gitignore`에 차단해 뒀다)
> ⚠️ MCP 서버는 **세션 시작 시 로드**된다. 추가·로그인 후에는 세션을 새로 열어야 도구가 보인다.

### GitHub
커넥터·`gh` CLI 없이 **git + HTTPS**만으로 충분하다. Windows 자격 증명 관리자가 자격증명을 보관한다.
> ⚠️ 공용 PC라면 떠날 때 **Windows 자격 증명 관리자 → `git:https://github.com` 항목을 삭제**할 것.

## 2-1. 이탈 시 정리 체크리스트 (공용 PC·공용 계정)
- [ ] `claude mcp logout notion` — Notion 자격증명 삭제
- [ ] `claude mcp remove notion -s local` — 서버 설정까지 삭제
- [ ] Windows 자격 증명 관리자에서 `git:https://github.com` 삭제
- [ ] Claude 앱 로그아웃

## 3. Notion DB 2개 생성 (새 계정이면 필수)
새 워크스페이스엔 DB가 없으므로 새로 만든다. Claude Code에 이렇게 요청:
> "최상위에 'CS & 면접 학습 아카이브' 페이지를 만들고, 그 아래에 'CS 학습 로그'와 '개념 노트' DB를 SETUP.md 스키마대로 만들어줘. 두 DB는 Relation으로 연결해줘."

**① CS 학습 로그 (세션 기록)**
- 제목(Title), 날짜(Date)
- 유형(Select): `자료정리` / `모의면접`
- 분야(Select): `OS` / `네트워크` / `DB` / `자료구조·알고리즘` / `컴퓨터구조` / `AI·ML` / `데이터 엔지니어링` / `기타`
- 이해도(Select): `🔴 부족` / `🟡 보통` / `🟢 충분`
- 약점·복습포인트(Text), 블로그 후보(Checkbox)

**② 개념 노트 (복습용)**
- 제목(Title, 개념명), 분야(Select: ①과 동일)
- 이해도(Select: 🔴/🟡/🟢)
- 핵심요약(Text), 복습포인트(Text)
- 관련 세션(Relation → CS 학습 로그, 양방향)
- 블로그 후보(Checkbox), 최종수정(Last edited time)

## 4. CLAUDE.md의 ID 갱신
생성 후 받은 **두 Data source ID**(학습 로그 ①, 개념 노트 ②)를 [CLAUDE.md](CLAUDE.md)의 각 `Data source ID:` 줄에 덮어쓴다.
(이 ID들은 워크스페이스마다 다르다.)

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
| DB ① 학습 로그 | https://app.notion.com/p/bcb3b2fc7184470cbe3fdfbb3c5268de |
| Data source ID ① | `8f362694-fac3-46a7-9e89-f39f77693caf` |
| DB ② 개념 노트 | https://app.notion.com/p/f58e8d2b344a4c7d925c7c7d9a57e56d |
| Data source ID ② | `643b30c2-48b4-454e-bbc6-05df11ca873a` |
