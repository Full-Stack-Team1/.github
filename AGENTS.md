# Full Stack Team1 공동작업규칙 — 기존 다이어리 원문 보존 및 팀 규칙 통합

작성: @vscodereader(최성원, 팀장) · 통합일: 2026-11-20

- 팀 조직: https://github.com/Full-Stack-Team1
- AI 전달 파일: https://github.com/Full-Stack-Team1/.github/blob/main/AGENTS.md
- `profile/README.md`는 조직 첫 화면의 프로젝트 소개·과업·팀 구성·협업 요약이다. 상세 규칙은 이 `AGENTS.md`에서 관리하며 요약에서 링크한다. 루트 README를 중복 생성하지 않는다.
- 아래는 기존 다이어리 AGENTS.md 전체를 바탕으로 현재 팀 규칙을 합친 문서다. **0~3·5~9절의 다이어리 이름·경로·스택·운영 주소·과거 상태는 원본 프로젝트의 내용이다.** 블로그 CMS의 폴더나 제품 기능으로 자동 확정하거나 존재하지 않는 상대 링크/명령을 실행하지 않는다. 공통 개발 원칙은 유지하고, 프로젝트 고유 항목은 해당 개발 저장소의 실제 구조·설계와 대조한다. 차이가 있다고 임의로 삭제하지 말고 차이를 보고한다.
- 4절은 사용자 요청의 팀 구성·브랜치·리뷰·경로별 변경 기록 규칙으로 갱신했다. 10절에 이전 누락 및 추가·변경 내역을 모두 기록했다.

---

# 로그(다이어리) — 공통 개발 지침

이 저장소에서 일하는 사람과 AI(Claude Code·Codex)가 **가장 먼저 읽는 파일**이다. 이 파일과 아래 폴더별 규칙만 읽으면 이전 대화 없이 같은 방식으로 이어서 일할 수 있어야 한다. 사용자의 새 지시가 이 파일과 다르면 지시를 따르고 이 파일을 함께 고친다.

## 0. 먼저 읽을 것

| 작업 위치 | 규칙 파일 |
| --- | --- |
| 전체 공통(이 파일) | `AGENTS.md` (Claude는 `CLAUDE.md` → 이 파일) |
| 웹 앱(화면·API·테스트) | [apps/web/AGENTS.md](apps/web/AGENTS.md) |
| 공통 화면 부품·토큰 | [packages/ui/AGENTS.md](packages/ui/AGENTS.md) |
| 순수 규칙·스키마 | [packages/core/AGENTS.md](packages/core/AGENTS.md) |
| DB 스키마·마이그레이션 | [packages/db/AGENTS.md](packages/db/AGENTS.md) |
| 외부 제공처 호출(지도·검색·경로) | [packages/api/AGENTS.md](packages/api/AGENTS.md) |
| 설계서(todo·finish) | [docs/design/log-diary/AGENTS.md](docs/design/log-diary/AGENTS.md) |
| 남은 일 / 끝난 일 | [todo/README](docs/design/log-diary/todo/README.md) / [finish/README](docs/design/log-diary/finish/README.md) |

새 규칙 파일은 이 표에 있는 위치에만 둔다. 같은 내용을 여러 파일에 반복하지 않고 링크한다.

## 1. 프로젝트

- 이름: **로그**(Diary Project). GitHub `vscodereader/Diary-Project`(비공개). 로컬 폴더 이름은 `diary`(예: `C:\Users\chois\diary`).
- **중심은 다이어리다.** 사진 중심으로 하루(날짜) 아래 로그를 쌓고, 고른 사람에게 하루 단위로 VIEW/EDIT 공유한다.
- 여행 웹앱 **하루길**(`vscodereader/harugil`) 코드를 복사해 시작했다. 하루길 코드는 다이어리를 만들 때 필요한 것을 가져다 쓰는 **재료**일 뿐 주 기능이 아니다(사용자, 2026-11-01). 남아 있는 옛 여행 화면(지도·일정·준비·지출·발자취·캘린더·초대한 사람)을 지울지는 사용자가 정한다. 그 전까지 지우지 않고, 새 작업 시간을 들여 다듬지도 않는다.
- 웹 우선(PC·노트북), 휴대폰은 같은 웹. `android-app`은 WebView 껍데기다.
- 로그인: **Google 계정만**. 게스트·카카오·Apple 없음.
- 만들지 않는 것: 광고·구독·결제·할인·선물·보상·이벤트·친구 초대·출석. 기술적 파일 크기·저장 용량 제한은 만든다.
- 운영: Vercel 프로젝트 `diary`(https://diary-vert-psi.vercel.app), DB는 Neon PostgreSQL(하루길과 다른 DB). 운영 DB·배포·환경 변수는 프로젝트 주인(vscodereader)이 관리한다.

## 2. 일하는 순서 (모든 기능·수정에 똑같이)

1. **설계서 먼저.** 할 일을 [todo](docs/design/log-diary/todo/README.md)에서 찾거나, 새 요청이면 해당 설계서(00~07) 절에 계약을 적는다. 쓰는 법은 [설계서 규칙](docs/design/log-diary/AGENTS.md).
   - '제안'·'미정'을 확정처럼 구현하지 않는다. 결정이 필요하면 **구현 전에 사용자에게 묻는다**(질문은 결정에 필요한 것만).
   - 원본 앱 관찰과 사용자 요구가 다르면 사용자 요구가 우선이다.
2. **이슈와 브랜치.** 4절 Git 규칙대로 이슈를 만들고 브랜치를 판다.
3. **구현.** 5절 코드 규칙과 폴더별 규칙을 지킨다. 새 부품을 만들기 전에 기존 공통 부품으로 되는지 먼저 본다.
4. **테스트 케이스를 같이 넣는다.** 사전 조건·입력·기대 결과, 경계값·실패·권한·저장 후 재조회를 포함한다. 위치와 방법은 [apps/web/AGENTS.md](apps/web/AGENTS.md) "테스트".
5. **자동 검사:** `pnpm check` → `pnpm test` → (DB를 건드렸으면) `pnpm test:db` → `pnpm build`. 결과 숫자를 그대로 보고한다.
6. **localhost에서 직접 확인.** 테스트 DB로 개발 서버를 켜고 임시 사용자로 로그인해 **넓은 화면(약 1280px)과 휴대폰 폭(375px) 둘 다** 본다. 방법은 [apps/web/AGENTS.md](apps/web/AGENTS.md) "localhost에서 로그인한 화면 확인". 확인 못 한 것은 못 했다고 쓴다.
7. **문서 정리.** 끝난 일은 finish(원래 문제 → 수정 → 검증 결과 → 제한), 남은 일만 todo에 둔다.
8. **커밋·PR.** 4절 형식. 화면이 바뀐 PR은 확인한 폭과 결과를 본문에 쓴다.
9. **병합·배포**는 리뷰어 승인 뒤. main 병합·운영 DB 마이그레이션·Vercel 배포는 **프로젝트 주인의 지시나 승인**이 있어야 한다.

중간에 임의로 멈추지 않는다. 멈춰야 하면 이유를 말한다. 오래 걸리면 지금 무엇을 하는지 한 줄로 알린다. 시킨 일만 하고, 관련 문제를 발견하면 고치지 말고 알린다.

## 3. 사용자(프로젝트 주인) 선호

- 답은 **한국어**, 짧고 쉬운 말. 전문 용어는 짧게 풀어 쓴다.
- 사용자가 예상 시간을 자주 묻는다. 범위와 미정 결정을 보고 분 단위로 답한다.
- 사용자가 "직접 하겠다"고 하면 명령어만 알려 준다(PowerShell 문법: `$env:NAME = "값"; 명령`).
- 데스크톱·휴대폰이 같은 기능을 보여야 한다.

## 4. Git 규칙 (2026-11-20 팀 공통규칙)

### 파트와 담당자

| 파트 | GitHub 계정 |
| --- | --- |
| 프론트 | @erka246000, @minhyeonhong086-maker(민현홍), @vscodereader |
| 백엔드 | @PswHp(Harry Park), @minseongdeveloper(저장소 생성자), @vscodereader |

`vscodereader`는 팀장이며 프론트와 백엔드를 모두 맡는다.

### 이번 팀의 필수 실행 안내 — 처음 GitHub를 사용하는 팀원도 동일하게 적용

**프론트 담당 @erka246000, @minhyeonhong086-maker(민현홍), @vscodereader는 아래 순서대로 반드시 작업한다.** 민현홍은 표시 이름이며 사진에서 확인한 실제 GitHub 아이디는 `minhyeonhong086-maker`다. 백엔드 담당 @PswHp, @minseongdeveloper, @vscodereader도 `front` 대신 `backend`를 기준으로 같은 절차를 따른다.

- Git은 내 컴퓨터에서 코드 변경 이력을 관리하는 도구이고, GitHub는 팀이 코드를 공유하고 검토하는 사이트다. 브랜치는 작업 공간을 나누는 것이며, PR(Pull Request)은 내 변경 내용을 다른 브랜치에 합쳐 달라는 검토 요청이다. 커밋은 내 컴퓨터에 변경 이력을 기록하고, push는 그 커밋을 GitHub에 올리는 것이다. **push만 했다고 작업 완료나 병합이 된 것은 아니다.**
- 처음에는 팀 공용 개발 저장소 `minseongdeveloper/blog-cms`를 clone(내 컴퓨터에 내려받기)하고 설치 안내를 따른다. 이 규칙의 원본을 보관한 `blog-create`·`Diary-Project`를 팀 작업 저장소와 혼동하지 않는다. 이미 clone했다면 새로 받을 필요 없다.
- 작업 전 이슈를 만들고 담당자를 본인으로 지정한다. 현재 브랜치와 미저장·미커밋 변경을 확인한 뒤, 최신 파트 브랜치에서 기능 브랜치를 만들고 그 아래 본인 세부 작업 브랜치를 만든다. 같은 이름의 기능 브랜치가 이미 있으면 새로 중복 생성하지 말고 해당 브랜치를 기준으로 한다.
- 본인 세부 작업 브랜치에서만 수정한다. 다른 사람이 쓰는 브랜치를 임의로 바꾸거나 `main`·`front`·`backend`에 직접 push하지 않는다. 작업 브랜치의 이름은 아래 예시처럼 작업 내용이 드러나게 정하고, 같은 작업이 겹치면 이슈에서 먼저 담당 범위를 나눈다.
- `localhost`는 **본인 컴퓨터에서 실행하는 개발 화면**이다. 코드를 고친 다음 개발 서버를 켜서 실제 화면·버튼·입력·이동·저장·오류 상황과 휴대폰 폭을 직접 확인한다. 검사·테스트도 실행한다. 문제를 수정하고 다시 확인한 뒤 변경한 파일만 확인하여 커밋하고 본인 작업 브랜치를 push한다. 비밀 키나 `.env`는 올리지 않는다.
- GitHub의 팀 저장소에서 **Pull requests → New pull request**를 연다. `base`는 합칠 대상인 기능 브랜치, `compare`는 본인 세부 작업 브랜치로 선택한다. 변경 파일이 본인 작업 범위인지 확인하고 제목·내용·이슈 번호·검증 결과·화면 증거를 적어 **Create pull request**를 누른다.
- PR 오른쪽 **Reviewers**에서 아래 표의 사람을 **모두** 지정한다. 본인 아이디는 지정할 수 없으므로 본인 검토 결과를 PR 본문에 적는다. **본문에 @아이디를 적는 것과 Reviewers로 지정하는 것은 다르다. 태그만 적고 리뷰어 지정을 생략하면 안 된다.** 리뷰어 선택이 안 되면 팀장에게 알리고 지정된 것을 확인한다.

| PR 작성자 | 프론트 작업 시 반드시 지정할 리뷰어 | 백엔드 작업 시 반드시 지정할 리뷰어 |
| --- | --- | --- |
| @erka246000 | @minhyeonhong086-maker, @vscodereader | 백엔드 변경도 있으면 백엔드 전원 추가 |
| @minhyeonhong086-maker | @erka246000, @vscodereader | 백엔드 변경도 있으면 백엔드 전원 추가 |
| @vscodereader | @erka246000, @minhyeonhong086-maker | @PswHp, @minseongdeveloper |
| @PswHp | 프론트 변경도 있으면 프론트 전원 추가 | @minseongdeveloper, @vscodereader |
| @minseongdeveloper | 프론트 변경도 있으면 프론트 전원 추가 | @PswHp, @vscodereader |

양쪽 변경이면 두 파트의 대상자를 합치되 본인은 제외하고 같은 사람을 중복 지정하지 않는다.

- 리뷰 요청을 받은 사람은 PR의 **Files changed**에서 모든 변경 내용을 읽고, PR에 적힌 확인 방법으로 동작과 검사 결과를 확인한다. 줄별 의견은 해당 줄의 `+`로 남긴다. **Review changes → Comment**는 의견, **Request changes**는 수정 요청, **Approve**는 병합해도 된다는 최종 승인이다. 단순 코멘트는 승인으로 세지 않는다.
- 작성자는 리뷰 내용을 읽고 같은 작업 브랜치에서 수정·재검증·커밋·push한다. 기존 PR에 수정 내용이 반영되므로 같은 작업의 PR을 중복 생성하지 않는다. 답변과 변경 내용을 남기고 다시 검토를 요청한다. 지적 사항을 해결하지 않고 대화만 닫거나 병합하지 않는다.
- 본인을 제외한 필수 리뷰어 전원 승인, 미해결 의견 없음, 필수 검사 통과, 충돌 없음이 확인되어야 병합한다. 충돌이나 실패 원인을 모르면 임의로 덮어쓰지 말고 팀장에게 알린다.
- 병합 완료 표시를 확인한 뒤 **Delete branch**로 사용이 끝난 원격 세부 작업 브랜치를 삭제한다. 로컬에서도 부모 브랜치로 전환하고 최신 병합 내용을 받은 다음 안전 삭제(`git branch -d 작업브랜치`)한다. 삭제가 거절되면 강제 삭제하지 말고 병합 상태를 확인한다. 다른 사람이 쓰거나 하위 PR의 기준이 된 브랜치는 정리될 때까지 삭제하지 않는다.
- 기능 브랜치 → `front`/`backend`, 파트 브랜치 → `main`도 PR과 같은 리뷰 절차를 거친다. `main` 병합·배포는 팀장 @vscodereader의 승인을 받는다. `main`, `front`, `backend`는 유지한다.

### 브랜치 구조와 생성

```text
main
├── front                         # main에서 분기한 프론트 통합 브랜치
│   └── feat/front-main-page       # front에서 분기한 메인 페이지 기능 브랜치
│       ├── feat/front-main-page-components  # 기능 브랜치에서 분기한 공통 컴포넌트 작업
│       └── feat/front-main-page-css         # 기능 브랜치에서 분기한 스타일 작업
└── backend                       # main에서 분기한 백엔드 통합 브랜치
    └── feat/backend-auth         # backend에서 분기한 인증 기능 브랜치
        └── feat/backend-auth-login         # 기능 브랜치에서 분기한 로그인 세부 작업
```

- `front`와 `backend`는 최신 `main`에서 각각 만든 장기 유지 브랜치다. 해당 파트의 기능 브랜치는 최신 파트 브랜치에서, 세부 작업 브랜치는 최신 기능 브랜치에서 만든다.
- 작업 전에 범위·범위 밖·확인 방법을 적은 이슈를 만든다. 이슈 하나당 작업 브랜치 하나를 사용한다.
- `main`, `front`, `backend`, 기능 통합 브랜치에 코드를 직접 올리지 않는다. 세부 작업 브랜치에서 구현하고 PR로 합친다.
- 이름은 `<종류>/<파트>-<기능>-<세부>`처럼 영문 소문자와 하이픈으로 쓴다. 기능 브랜치에는 세부 부분을 생략한다. 종류는 실제 변경 목적에 맞춘다.
- 공유된 이력에 rebase·강제 push를 하지 않는다. 다른 사람 작업을 덮어쓰지 않는다.

### 종류 이름의 뜻

| 종류 | 의미 | 예시 |
| --- | --- | --- |
| `feat` | 이전에 없던 기능 추가 | 메인 페이지, 로그인, 공통 버튼 추가 |
| `fix` | 잘못 동작하는 기존 기능 수정 | 로그인 실패, 버튼 잘림, API 오류 수정 |
| `refactor` | 사용자에게 보이는 동작을 유지하며 내부 구조 개선 | 중복 코드 공통화, 함수·파일 분리 |
| `docs` | 문서만 변경 | 개발규칙, 설치 안내, API 설명 수정 |
| `chore` | 기능 개발 외 설정·도구·유지보수 | 린트·빌드 설정, 의존성 관리 |

새 화면의 CSS 구현은 `feat`, 기존 화면의 깨진 CSS 수정은 `fix`다. CSS 파일이라는 이유만으로 종류를 정하지 않는다.

### 메인 페이지 작업 예시와 완료 절차

1. 최신 `front`에서 `feat/front-main-page`를 만든다.
2. 그 기능 브랜치에서 `feat/front-main-page-components`를 만들어 공통 컴포넌트를 구현한다. 스타일 등 별도 작업도 같은 방식으로 작은 브랜치를 만든다.
3. 작은 브랜치에서 구현·검사를 마치고 `localhost`에서 화면과 동작을 직접 확인한다. 정상 동작뿐 아니라 오류·경계 상황, 관련 화면과 반응형도 확인하고 발견한 문제를 모두 수정한다. 백엔드는 로컬 API와 관련 통합 동작을 확인한다.
4. 완료한 작은 브랜치에서 기능 브랜치를 대상으로 PR을 만든다. 변경 내용, 확인 방법, 실행한 검사와 결과, 화면 변경 증거를 적고 아래 규칙대로 리뷰어를 전원 지정한다.
5. 리뷰어 전원이 변경 내용을 확인한다. 코멘트나 변경 요청이 있으면 작성자가 수정·답변하고 다시 검증한다. 필요한 최종 승인을 모두 받은 뒤 기능 브랜치에 병합한다.
6. 병합이 확인된 작은 브랜치는 로컬과 원격에서 삭제한다. 미병합 작업이 없고 다른 사람이 사용 중이지 않은지 먼저 확인한다. 강제 삭제하지 않는다.
7. 기능의 모든 세부 작업이 모이면 기능 브랜치 전체를 `localhost`에서 다시 확인한다. 기능 브랜치 → `front` PR도 같은 리뷰 절차를 거친다. 병합 후 기능 브랜치를 삭제한다.
8. 백엔드도 기능 브랜치 → `backend` 순서로 동일하게 진행한다. 파트 브랜치 → `main`은 양쪽 통합 확인과 리뷰를 마친 뒤 팀장이 승인하여 병합한다. `main`, `front`, `backend`는 삭제하지 않는다.

### 폴더·파일 생성과 변경 기록

- 작업 전에 저장소의 기존 폴더 구조, 파일 이름, 공통 컴포넌트, 유사 페이지를 확인한다. 기존 구조와 부품을 활용하고, 요청한 작업에 필요한 폴더와 파일만 생성한다. 임의의 새 구조나 중복 페이지·컴포넌트, 빈 폴더, 사용하지 않는 파일을 만들지 않는다.
- 새 경로가 필요하면 기존 구조 안에서 자연스러운 위치에 만들고, 왜 필요한지 변경 내역에 적는다. 아래 경로는 형식을 설명하는 예시이며 실제 프로젝트 구조로 확정한 것이 아니다.
- 경로는 저장소 루트 기준 `/front/...`처럼 적는다. 개인 PC의 `C:\...` 절대 경로나 실제로 존재하지 않는 경로를 쓰지 않는다. 파일 작업은 확장자를 포함한 파일 경로까지 적는다. 폴더 경로만 적어 파일별 작업을 뭉뚱그리지 않는다.

### 커밋 메시지

- 제목: `<종류>(<범위>): <대표 실제 경로> <무엇을 했는지 한국어로>`. 마침표 없이 한 줄로 쓴다. 파일 하나면 파일 경로, 여러 파일이면 대표 폴더 경로와 전체 작업 요약을 적는다.
- 범위는 `web`·`ui`·`core`·`db`·`api`·`docs` 중 바뀐 곳이다. 여러 범위라면 생략할 수 있지만 **경로는 생략하지 않는다.**
- 본문에는 **추가·수정·삭제·이동한 모든 파일을 한 파일당 한 줄씩** 적고, 각 줄에 작업 종류·전체 상대 경로·구체적인 변경 내용을 적는다. 이동은 이전 경로 → 새 경로를 둘 다 적는다. 관련된 새 폴더도 별도 줄로 경로·용도를 적는다. Git은 빈 폴더를 추적하지 않으므로 필요한 파일이 들어 있는 폴더만 만든다.
- 새 파일/페이지가 8개면 8개 경로를 **8줄로 각각** 적는다. 새 폴더도 있다면 폴더 설명 줄을 추가한다. `외 7개`, `관련 파일 수정`, `컴포넌트 등 추가`처럼 생략하지 않는다. 8줄을 채우려고 파일별로 커밋을 8개로 나눌 필요는 없다.
- 예시(파일 8개를 만드는 경우, 아래 폴더는 이미 존재한다고 가정):

```text
feat(web): /front/pages/userpages/mainpage 메인 페이지와 공통 컴포넌트 추가

- [추가] /front/pages/userpages/mainpage/MainPage.tsx: 메인 페이지 조합과 데이터 표시 구현
- [추가] /front/pages/userpages/mainpage/MainPage.css: 메인 페이지 반응형 스타일 구현
- [추가] /front/components/common/Button.tsx: 공통 버튼 컴포넌트 구현
- [추가] /front/components/common/Button.css: 공통 버튼 상태별 스타일 구현
- [추가] /front/components/common/Header.tsx: 공통 헤더와 메뉴 구현
- [추가] /front/components/common/Header.css: 공통 헤더 반응형 스타일 구현
- [추가] /front/components/common/Footer.tsx: 공통 하단 영역 구현
- [추가] /front/components/common/Footer.css: 공통 하단 영역 스타일 구현

검증: 실제 실행한 검사·테스트·빌드 결과와 localhost 확인 내용을 기재
남은 일: 실제 남은 항목 또는 없음
```

- 새 폴더를 함께 만들었다면 예를 들어 `- [폴더 추가] /front/pages/userpages/mainpage/: 메인 페이지 파일 배치에 필요`를 추가한다. 수정·삭제한 파일도 위 형식으로 전부 기록한다. 검증 결과와 남은 일을 파일별 목록과 구분하여 적는다.
- 설계서 변경과 코드 변경은 **커밋을 나눈다**(설계/문서 커밋 → 구현 커밋 순서).
- 세부 작업 브랜치를 기능 브랜치에 합칠 때 merge 커밋 제목은 `merge: <대표 실제 경로> <요약>`으로 쓴다.
- `.env*` 값, 비밀번호·토큰·API 키, 개인 파일은 절대 커밋하지 않는다.

### PR

- 세부 작업 → 기능 → 해당 파트(`front` 또는 `backend`) → `main` 순서로 PR을 올린다. 각 PR의 대상 브랜치를 반드시 확인한다.
- **PR 목록에 보이는 제목도 커밋 제목과 동일하게 실제 경로를 포함한다.** 예: `feat(web): /front/pages/userpages/mainpage 메인 페이지 공통 컴포넌트 추가`.
- PR 제목은 한 줄이므로 모든 파일 목록은 본문의 **변경** 절에 적는다. PR 전체의 실제 diff를 기준으로 추가·수정·삭제·이동한 모든 파일을 한 줄씩, 새 폴더도 별도 줄로 적는다. 여러 커밋에서 같은 파일을 수정했으면 해당 파일 한 줄에 최종 변경을 설명한다. 8개 파일이면 8줄이며 파일을 생략하지 않는다.
- **요약·변경·검증·리뷰는 필수**다. 배포 전·범위 밖은 해당할 때 추가한다. 이슈를 마무리하는 PR에는 `Closes #이슈번호`를 적는다.

```markdown
Closes #이슈번호

## 요약
전체 작업의 목적과 결과

## 변경
- [폴더 추가] /실제/새폴더/: 폴더가 필요한 이유 (새 폴더가 있는 경우)
- [추가] /실제/경로/파일명.확장자: 구현한 내용
- [수정] /실제/경로/파일명.확장자: 수정한 내용과 이유
- [삭제] /실제/경로/파일명.확장자: 삭제한 이유
- [이동] /이전/파일명.확장자 → /새/파일명.확장자: 이동한 이유

## 검증
실행한 명령과 실제 결과, localhost에서 확인한 기능·화면 폭과 증거

## 배포 전
해당할 때만 작성

## 범위 밖
해당할 때만 작성

## 리뷰
작성자 자체 점검 결과와 리뷰어가 집중해서 확인할 사항
```

- 위 양식의 예시 줄은 실제 변경한 항목으로 교체한다. 작성하지 않은 작업을 예시 그대로 남기지 않는다. PR 작성자는 **Files changed**와 변경 목록을 대조하고, 리뷰어도 경로·파일 누락 여부를 확인한다.

### 리뷰어와 병합 조건

- 프론트 코드가 포함된 PR은 프론트 인원 전원, 백엔드 코드가 포함된 PR은 백엔드 인원 전원을 검토 대상으로 한다. 두 파트를 함께 변경하면 두 파트 인원의 합집합을 대상으로 한다. 공통규칙 등 양쪽에 영향을 주는 문서도 양쪽이 검토한다.
- **작성자도 자체 검토에 반드시 참여한다.** 단, GitHub는 작성자 본인을 자기 PR의 리뷰어로 지정하거나 자기 PR을 승인하는 것을 허용하지 않는다. 작성자는 PR 본문에 자체 점검 결과를 남기고, 본인을 제외한 대상 인원 전원을 실제 리뷰어로 지정한다. `vscodereader`가 두 파트에 속해도 중복 지정하지 않는다.
- 예: `PswHp`의 백엔드 PR은 `minseongdeveloper`, `vscodereader`를 지정한다. `vscodereader`의 프론트 PR은 `erka246000`, `minhyeonhong086-maker`를 지정한다.
- 각 리뷰어는 변경 파일과 동작·검증 결과를 모두 확인한 뒤 코멘트, 변경 요청(Request changes), 승인(Approve) 중 적절한 리뷰를 남긴다. 확인 없이 형식적으로 승인하지 않는다.
- **코멘트만 남겼다고 병합 가능해지는 것은 아니다. 작성자를 제외한 해당 파트 리뷰어 전원의 최종 승인이 있어야 한다.** 지적 사항을 해결하고 대화를 정리한 뒤 승인받는다. 변경 요청이 남아 있거나 한 명이라도 검토·승인이 누락되면 병합하지 않는다.
- 리뷰 후 코드가 바뀌면 바뀐 내용을 다시 검토받는다. 이전 승인만 근거로 병합하지 않는다. 필수 검사 실패, 미해결 코멘트, 충돌이 있으면 해결 후 다시 확인한다.
- `main` 병합과 배포는 위 조건을 충족하고 팀장의 승인까지 받은 뒤 진행한다.
- 이 절은 팀의 공통 개발규칙이다. GitHub에서 병합을 기술적으로 차단하려면 별도로 브랜치 보호/Ruleset과 필수 승인·대화 해결·검사를 설정해야 한다. 문서 수정만으로 설정이 적용됐다고 간주하지 않는다.

## 5. 코드 규칙 (beyondsoft-kr/moneyroad-app 방식)

- **한 파일에 한 부품.** 파일명은 kebab-case(`date-range.tsx`), 부품 이름은 PascalCase(`DateRange`), 훅은 `use-*.ts`.
- 모양 차이는 새 부품을 만들지 않고 `variant`·`size` prop이나 CSS 변수로 고른다. 비슷한 부품을 여러 개 만들지 않는다.
- 여러 화면이 쓰는 부품은 `packages/ui`, 다이어리 전용 조합은 `apps/web/src/components/diary`.
- **하드코딩 금지:** px·색·z-index·투명도·시간(ms)·간격을 코드나 CSS에 숫자로 쓰지 않는다. `packages/ui/src/tokens.css`·`theme.ts`의 토큰을 쓰고, 없으면 토큰을 추가한다. 코드 속 정책 숫자는 이름 붙은 상수로 둔다. `packages/ui/test/no-hardcoded.test.ts`가 지키며, 이 테스트를 끄거나 예외를 늘려 우회하지 않는다.
- 쓰지 않는 코드·파일을 남기지 않는다(`noUnusedLocals`). re-export만 하는 묶음 파일(barrel)을 새로 만들지 않는다.
- import는 `@/` 별칭. `../../..` 깊은 상대경로를 쓰지 않는다.
- 주석은 '왜'를 짧게. 코드 주석은 영어, 테스트 이름·설명은 한국어(기존 코드와 같은 밀도).
- 타입은 `any` 대신 `unknown`과 좁히기. 들어오는 JSON은 zod 스키마로 검증한다.
- 리팩터링·공통화는 **화면이 이전과 똑같아야** 한다. 바꾼 뒤 화면을 비교해 확인한다.
- 큰 파일을 고칠 때도 주변 코드의 이름·형식·주석 밀도를 따른다.

## 6. 보안·데이터

- `.env*` 값을 출력·커밋하지 않는다. 키 발급 안내는 `apps/web/.env.example`. 제공처 비밀 키는 서버에만 둔다(공개 지도 브라우저 키 예외).
- 모든 데이터는 DB에만 저장한다. 브라우저 저장소(localStorage 등)·로컬 `data/` 파일 금지. 예외: 로컬 개발의 동작 로그 `active_log/log.YYYY-MM-DD`(git 제외), 운영은 DB `activity_logs`.
- 운영 DB를 테스트에 쓰지 않는다. 운영 DB에 테스트 사용자를 만들지 않는다. 데이터를 영구 삭제하는 동작은 사용자 확인 후.
- 실제 응답이 없는 경로·시간·가격은 비워 둔다(지어내지 않는다). 실패한 실제 호출을 데모로 몰래 바꾸지 않는다.
- Google 경로 선은 Google 지도에서만 그린다.
- 참고용으로 받은 다른 저장소는 읽기만 하고 설치·실행하지 않는다.
- Graphify(로컬 도구)를 쓰면 키·`.env*`·개인 사진·DB 내용을 넘기지 않고, `graphify-out/`은 커밋하지 않는다.

## 7. 설치·실행

Node.js 22.14 이상, pnpm 11.3.0, Docker(로컬 테스트 DB). 주 개발 환경은 Windows.

```powershell
pnpm install --frozen-lockfile   # 설치 뒤 Prisma 클라이언트가 자동 생성된다
pnpm run setup                   # apps/web/.env.local 생성(키 이름만, SESSION_SECRET 자동)
# apps/web/.env.example 안내대로 키를 발급해 apps/web/.env.local 에 채운다
pnpm dev                         # http://localhost:3000
pnpm check; pnpm test; pnpm build
pnpm doctor                      # 키가 채워졌는지만 확인(값 출력 없음)
pnpm dev:user create             # 로컬 테스트 DB에 임시 로그인 사용자(apps/web/AGENTS.md)
```

- 키가 없어도 화면·테스트·빌드는 돌아간다. 지도·검색·로그인 같은 그 키를 쓰는 기능만 안 된다.
- 로컬 테스트 DB 준비와 개발 서버를 테스트 DB로 켜는 법: [apps/web/AGENTS.md](apps/web/AGENTS.md).
- 배포(프로젝트 주인 승인 후): `$env:VERCEL_TELEMETRY_DISABLED = "1"; pnpm dlx vercel@latest deploy --prod --yes --non-interactive`. 운영 DB 마이그레이션: [packages/db/AGENTS.md](packages/db/AGENTS.md).

## 8. 자주 만난 문제와 해결 (트러블슈팅)

| 증상 | 원인 | 해결 |
| --- | --- | --- |
| 새로 받은 저장소에서 `pnpm check`가 타입 오류 수백 개 | Prisma 클라이언트가 안 만들어짐 | `pnpm install`(postinstall이 생성) 또는 `pnpm db:generate` |
| `pnpm build`·설치 중 `EPERM`(Prisma DLL) | Windows에서 개발 서버가 Prisma 엔진 파일을 잡고 있음 | 개발 서버를 끄고 실행 |
| 빌드 뒤 개발 서버에서 일부 API가 404(HTML) | 남은 `apps/web/.next/dev` | 그 폴더를 지우고 다시 `pnpm dev` |
| 테스트 DB 접속이 멈춤 | WSL이 IPv6 `localhost:55432`를 잡음 | 주소를 `127.0.0.1:55432`로 |
| 로컬 화면에서 저장(POST)이 403 | 같은 출처 검사. `127.0.0.1:3000`에서 쓰기 요청 | 브라우저는 `http://localhost:3000`으로 연다 |
| Windows 개발 서버가 갑자기 꺼짐(`ERR_DLOPEN_FAILED`, sharp) | sharp 두 버전이 한 프로세스에 로드 | 앱의 sharp를 Next와 같은 버전으로 맞춤(지금 0.35.5). sharp를 올릴 때 Next 버전과 함께 확인 |
| 화면 테스트가 가끔 실패(`Unable to find…`) | 부하가 크면 1초 기본 대기가 부족, 글이 먼저 보이고 버튼은 아직 없음 | 대기 시간은 `apps/web/test/setup-tokens.ts`의 상수. 누를 요소 자체를 `findBy*`로 기다린다 |
| 용량 확인 중 사진을 올려도 DB 크기가 안 늘어남 | 테스트 DB에 지운 행의 빈 공간이 많음(물리 크기 기준 검사는 정상) | 확인할 때만 테스트 DB에서 `VACUUM FULL diary_photos` |
| 인앱 브라우저가 숨겨진 상태에서 화면이 멈춘 듯함 | 숨은 탭은 렌더가 늦음 | 스크린샷보다 DOM 값(JS)으로 확인 |
| `routes-social` DB 테스트 10개 실패 | 테스트 DB에 발자취 지리 데이터가 없음 | 데이터 문제. 필요하면 `pnpm db:geography` |
| Git Bash `node -e`로 고친 정규식의 `\`가 사라짐 | 셸이 백슬래시를 먹음 | 정규식이 들어간 수정은 편집 도구로 |
| 문서 줄바꿈이 통째로 바뀐 diff | 파일마다 CRLF/LF가 다름 | 고칠 때 그 파일의 줄바꿈을 유지 |

새로 해결한 문제는 이 표에 한 줄로 더하고, 자세한 기록은 finish/06에 남긴다.

## 9. 지금 상태 (2026-11-01)

- 00~06 단계는 main 병합·운영 DB 마이그레이션·Vercel 배포까지 끝났다. 단계별 기록: [finish/README](docs/design/log-diary/finish/README.md), 예전 인계 이력: [finish/07 §14](docs/design/log-diary/finish/07-delivery-and-decisions.md).
- 남은 일과 사용자 확인 대상: [todo/README](docs/design/log-diary/todo/README.md).
- 하루 영상·AI 자동 생성·영상/음성·받아쓰기는 하고 싶지만 계획 단계만(todo/07 §14). 정밀 디자인은 요청이 올 때마다 고친다.
- 옛 여행 기능 정리(08 단계)는 사용자 결정 대기.
- 진행 중: `refactor/team-setup`(이슈 #1~#4: 새 저장소 설치 오류, 키 발급 안내, 이 규칙 문서들, 다이어리·공통 코드 정리).

<!-- BEGIN:turborepo-agent-rules -->

# This is NOT the Turborepo you know

Turborepo configuration, task behavior, and CLI commands can vary between installed versions and may differ from your training data. Resolve the `turbo` package from this file's directory or relevant workspace; in monorepos, it may not be visible from the repository root. For example, run `node -p "require.resolve('turbo/package.json')"` from a workspace that depends on `turbo`.

Read `docs/README.md` inside that installed package first, then read the relevant pages from its `docs/` directory before changing Turborepo configuration or commands. Heed deprecation notices. These bundled docs match the installed package version and are available without network access.

This block is written and re-added by `turbo` before repository-scoped commands when an AI agent is detected. In the Turborepo source repository, its template is defined in `crates/turborepo-cli/src/cli/agent_guidance.rs`. Removing the managed block while updates are enabled means a later qualifying invocation will add it again. Set `"agentGuidance": false` in the root `turbo.json` or `turbo.jsonc` to opt out; this does not remove an existing block. Keep the block committed with your work to avoid an uncommitted change on the next agent invocation.
<!-- END:turborepo-agent-rules -->

## 로컬 확인과 AI 작업 원칙

- 실제 프로젝트의 설치·실행·검사 명령은 프로젝트에 정의된 명령을 확인해서 사용합니다. 아직 정의되지 않은 명령을 실행했다고 적거나 임의의 성공 결과를 만들지 않습니다.
- PR에는 직접 확인한 localhost 주소·화면/기능, 실행한 검사·테스트·빌드 결과를 적습니다. 확인하지 못한 항목은 이유와 함께 명시하며 완료한 것으로 표시하지 않습니다.
- AI도 작업 범위 밖의 코드·설정·다른 사람 작업을 임의로 변경하지 않습니다. 변경 내용과 검증 결과를 작성자가 직접 확인한 뒤 PR을 올립니다.
- 문서의 규칙과 실제 권한 설정은 별개다. 현재 조직의 기본 권한은 Write이며 비공개 저장소 포크를 조직 차원에서 허용했다. 실제 브랜치 생성·브랜치 보호·개별 저장소 포크 설정은 별도로 확인한다.

## 10. 공동작업규칙 이관 누락·추가·변경 대조 (2026-11-20)

### 내가 이전 조직 문서에서 누락한 내용 — 이번에 복원

- 원문 도입부: 사람과 AI가 가장 먼저 전체 규칙을 읽고, 새 사용자 지시가 다르면 문서도 함께 고친다는 원칙.
- 0절 전체: 작업 위치별 AGENTS.md·CLAUDE.md·설계서·todo/finish 안내 표, 새 규칙 파일 위치 제한, 중복 대신 링크 사용.
- 1절 전체: 로그의 목적, 하루/로그/공유 구조, 하루길 코드의 재료 역할과 옛 화면 변경 제한, PC·모바일·WebView 범위, Google 로그인, 제외 기능과 용량 제한, Vercel·Neon 및 운영 관리 담당.
- 2절의 설계 우선·미정 확인·사용자 요구 우선, 기존 부품 우선 재사용, 테스트의 사전 조건·입력·기대 결과·경계·실패·권한·재조회 요건, 정해진 자동 검사 순서와 실제 숫자 보고, 테스트 DB·임시 로그인 및 PC/모바일 폭 직접 확인, finish/todo 정리 방식, 화면 PR 증거, 운영 DB 변경 승인. 이슈·브랜치·리뷰와 일반적인 로컬 확인은 이전 문서에도 있었지만 이 구체적인 기준은 누락했다.
- 2절 마지막: 임의 중단 금지, 중단 사유·진행 알림, 지시한 범위만 작업하고 관련 문제는 임의 수정 대신 보고.
- 3절 전체: 한국어·쉬운 설명, 예상 시간 안내, 사용자가 직접 할 때 PowerShell 명령만 안내, PC와 휴대폰 기능 동일.
- 5절 전체: 한 파일 한 부품, 파일/컴포넌트/훅 이름, variant·size·CSS 변수 재사용, 공통/전용 부품 위치, 하드코딩 금지와 토큰·이름 붙은 상수·검사 우회 금지, 미사용 코드·파일·barrel 금지, import 별칭, 주석 언어·설명 기준, unknown·타입 좁히기·zod 검증, 리팩터링 전후 화면 동일·비교, 주변 코드 형식 유지.
- 6절: 비밀 값의 출력 금지와 서버 보관(커밋 금지는 이전에도 있었음), DB만 영속 저장·브라우저/로컬 저장 금지와 로그 예외, 운영 DB 테스트·테스트 사용자 금지와 영구 삭제 확인, 경로·시간·가격 조작/데모 대체 금지, Google 선의 지도 제한, 참고 저장소 설치·실행 금지, Graphify 민감 정보 금지·산출물 제외.
- 7절 전체: Node·pnpm·Docker·Windows 환경, 설치·setup·개발·검사·doctor·임시 사용자 명령, 키가 없을 때의 동작, 테스트 DB 안내, 승인 후 배포·마이그레이션 안내.
- 8절 전체 12개 문제 해결 기록: Prisma 생성, DLL 잠금, Next 개발 캐시, WSL IPv6, localhost 출처, sharp 버전, 테스트 대기, DB 물리 용량, 숨은 인앱 탭, 지리 데이터 부족, 셸 백슬래시, 줄바꿈 차이. 새 해결 내용을 표와 finish에 남기는 규칙도 복원.
- 9절 전체: 원문 기준일의 완료·남은 일·보류 기능·진행 브랜치 기록. 현재 블로그 개발 상태로 오해하지 않도록 원문 이력임을 명시.
- Turborepo 관리 블록 전체: 설치 버전의 번들 문서 확인, 설정·명령 변경 전 관련 문서 확인, 관리 블록 유지와 해제 방식.
- 이관 중 커밋 예시의 AI 공동작성 표시 줄도 제외했었다. 원문 예시는 보존하되 실제 사용하지 않은 AI 이름·버전을 작성자로 쓰지 않는다: `Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com>` (원문의 예시이며 AI가 만든 커밋에만 적용).

### 내가 추가하거나 구체화한 내용 — 사용자 요청에 따른 것

- 프론트/백엔드 담당자 실명·GitHub 아이디, vscodereader의 팀장·양쪽 겸임, @멘션과 작성자별 리뷰어 표.
- main → front/backend → 기능 → 세부 작업의 4단계 구조, 최신 부모 기준 분기, 직접 push 금지와 이름 예시.
- feat·fix·refactor·docs·chore의 뜻과 사례, CSS도 변경 목적에 따라 종류를 정한다는 설명.
- Git/GitHub/브랜치/커밋/push/PR 용어, clone·이슈·작업·localhost·push·PR 화면의 base/compare·Reviewers 지정 절차.
- 공통 컴포넌트·CSS 세부 작업 → 로컬 확인·수정 → PR·리뷰 → 부모 병합 → 병합된 작업 브랜치 삭제, 기능 통합 후 재검증과 파트/main 병합 순서.
- 기존 구조·기존 공통 부품을 먼저 확인하고 필요한 폴더·파일만 생성, 불필요/중복/빈 폴더·파일 금지.
- 커밋 및 PR 제목에 실제 대표 경로, 본문에 전체 상대 파일 경로와 추가/수정/삭제/이동별 작업, 새 폴더 용도, 8개 파일이면 8줄이며 생략 금지. Files changed와 대조.
- 같은 파트 전원 리뷰, 양쪽 변경이면 합집합, 작성자 자체 점검, 지적 사항 수정·답변·재검증·재검토, 전원 최종 승인과 검사·대화·충돌 해소, 팀장의 main·배포 승인.

### 내가 추가한 운영 설명과 기존 설명을 바꾼 부분

- GitHub에서는 작성자 자신에게 리뷰 요청/자기 승인이 불가능하므로 본인은 자체 점검, 나머지 대상자 전원은 실제 Reviewers로 지정하도록 설명했다. 태그만 남기는 것은 리뷰 요청을 대신하지 않는다.
- 코멘트와 승인 차이를 설명하고 코멘트만으로 병합하지 않도록 명시했다. 수정 후 이전 승인만으로 병합하지 않는 조건, 문서와 실제 브랜치 보호 설정의 차이를 추가했다.
- 원래의 main → 큰 브랜치 → 작은 브랜치 설명은 사용자 요청의 front/backend 4단계 구조로 대체했다. 원래의 동기 아이디 미정/서로 한 명 지정 설명은 실제 파트 전원 리뷰로 대체했다.
- 커밋/PR의 짧은 제목·선택적 본문 안내는 사용자 요청의 경로 포함 제목·파일별 전체 내역으로 구체화했고, 요약·변경·검증·리뷰를 필수로 했다. merge 제목에도 대표 경로를 넣었다.
- 규칙 원본 저장소와 실제 개발 저장소 구분, 조직 주소·작성자·기준일, README/AGENTS/profile 동일 유지, AI 전달 파일 다운로드 안내를 추가했다.
- 정의되지 않은 검사 명령/결과를 만들지 않기, 미확인 항목 명시, AI 결과의 작성자 직접 검토를 추가했다. 원문의 실제 명령·구조를 임의로 없애는 근거로 사용하지 않는다.
- 이전 조직 문서의 '제품/다이어리 내용은 포함하지 않는다'는 범위 제한은 내가 임의로 붙인 것이므로 철회한다. 기존 다이어리 원문을 보존하며 프로젝트 고유 내용이라는 안내만 붙인다.
- 이번 변경은 문서만 갱신한다. 제품 코드·팀원 권한·브랜치 보호·배포는 변경하지 않는다.

## 11. 조직 소개와 상세 규칙의 구분 (2026-11-20)

- 선정 주제는 블로그 및 콘텐츠 관리 시스템 구축이다. 조직 소개는 `profile/README.md` 한 곳에 두고 선정 과업과 협업 요약만 간단히 표시한다.
- 상세 공동작업규칙과 원문 대조 이력은 이 파일에 보존한다. 앞의 10절에 나온 README/AGENTS/profile 동일 유지 설명은 당시 변경 이력이며, 현재는 이 절의 문서 구분을 따른다.
- 중복 루트 `README.md`는 제거한다. 기존 개발 저장소를 옮기거나 제품 코드·권한을 변경하는 작업은 이번 수정에 포함하지 않는다.
