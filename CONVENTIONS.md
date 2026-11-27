# 레포 공통 컨벤션

이 문서는 `leeclaire506` 계정에서 만드는 모든 레포지토리에 공통으로 적용하는
커밋 / 브랜치 / PR 컨벤션을 정의합니다. 이 레포(`.github`)는 GitHub 특수 레포로,
여기에 둔 공통 설정과 템플릿이 다른 레포의 기본값으로 쓰입니다.

---

## 1. 커밋 컨벤션 (Conventional Commits)

### 형식

```
<type>(<scope>): <subject>

<body>

<footer>
```

- **type** — 필수. 아래 표 참고.
- **scope** — 선택. 변경 범위 (예: `auth`, `api`, `ui`). 생략 가능.
- **subject** — 필수. 50자 이내, 명령형 현재시제, 마침표 없음. (예: `add login validation`)
- **body** — 선택. "무엇을/왜" 설명. 72자에서 줄바꿈.
- **footer** — 선택. 이슈 참조(`Closes #12`), Breaking change 등.

### type 목록

| type       | 용도                                             |
| ---------- | ------------------------------------------------ |
| `feat`     | 새 기능                                          |
| `fix`      | 버그 수정                                        |
| `docs`     | 문서만 변경                                      |
| `style`    | 포맷·세미콜론 등 동작에 영향 없는 변경           |
| `refactor` | 기능 변화 없는 코드 구조 개선                    |
| `perf`     | 성능 개선                                        |
| `test`     | 테스트 추가·수정                                 |
| `build`    | 빌드 시스템·의존성 변경 (npm, gradle 등)         |
| `ci`       | CI 설정 변경 (GitHub Actions 등)                 |
| `chore`    | 그 외 잡무 (설정, 스크립트 등)                   |
| `revert`   | 이전 커밋 되돌리기                               |

### 예시

```
feat(auth): add email verification on signup
fix(api): handle null response from payment gateway
docs: update README setup steps
refactor(ui): extract Button into shared component
```

### Breaking change

푸터에 `BREAKING CHANGE:` 를 명시하거나 type 뒤에 `!` 를 붙입니다.

```
feat(api)!: drop support for v1 endpoints

BREAKING CHANGE: /v1/* 경로가 제거되었습니다. /v2/* 를 사용하세요.
```

---

## 2. 브랜치 컨벤션

### 기본 브랜치

- **`main`** — 항상 배포 가능한 상태. 직접 push 금지, PR을 통해서만 머지.

### 작업 브랜치

`main` 에서 분기하는 짧게 유지되는 브랜치를 사용합니다.

```
<type>/<short-description>
<type>/<issue-number>-<short-description>
```

- **type** — 커밋 type과 동일 (`feat`, `fix`, `docs`, `chore` 등).
- **description** — kebab-case, 영문 소문자.
- 이슈가 있으면 번호를 앞에 붙입니다.

### 예시

```
feat/user-profile
fix/42-login-redirect
docs/contributing-guide
chore/update-deps
```

---

## 3. PR 컨벤션

- **제목** — 커밋 컨벤션과 동일한 형식 사용. (예: `feat(auth): add email verification`)
- **본문** — `.github/pull_request_template.md` 템플릿을 채웁니다.
- **크기** — 리뷰 가능한 단위로 작게. 가능하면 변경 400줄 이내.
- **머지 전략** — **Squash and merge** 권장. 머지 커밋 메시지는 PR 제목(컨벤션 형식)을 그대로 사용.
- **머지 조건** — 최소 1명 리뷰 승인 + CI 통과.
- **머지 후** — 작업 브랜치 삭제.

### 리뷰 체크리스트 (리뷰어)

- [ ] 변경이 PR 설명과 일치하는가
- [ ] 테스트가 추가/수정되었는가
- [ ] 네이밍·구조가 기존 코드와 일관적인가
- [ ] 불필요한 로그·주석·디버그 코드가 없는가

---

## 4. 적용 방법

새 레포를 만들 때:

1. 이 컨벤션을 따르면 `.github` 레포의 공통 템플릿(PR 템플릿 등)이 자동 적용됩니다.
2. 레포별로 다른 규칙이 필요하면 해당 레포에 템플릿을 두어 오버라이드합니다.
3. `main` 브랜치 보호 규칙(PR 필수, 리뷰 필수)을 설정하는 것을 권장합니다.
