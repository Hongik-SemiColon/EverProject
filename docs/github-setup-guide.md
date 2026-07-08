# GitHub 세팅 가이드 (웹에서 직접 할 것들)

로컬 저장소는 이미 준비되어 있습니다. 아래는 GitHub 웹사이트에서 팀장이 직접 해야 하는 절차입니다.

## 1. Organization 생성

1. github.com 우측 상단 `+` → **New organization**
2. **Free 플랜** 선택
3. Organization 이름 입력 (예: `everproject-team`) — 나중에 바꾸기 번거로우니 신중히
4. 소속: 개인 계정으로 생성

## 2. 저장소 생성

1. Organization 페이지 → **New repository**
2. 이름: `everproject`
3. **Private** 선택 (기업 데이터 포함이므로 필수)
4. README, .gitignore는 **추가하지 않음** (로컬에 이미 있음)

## 3. 로컬 저장소와 연결 (팀장 PC에서)

```
cd C:\Users\skc59\Documents\EverProject
git remote add origin https://github.com/<organization이름>/everproject.git
git push -u origin main
```

## 4. 팀원 초대

1. Organization → **People** → **Invite member** — 팀원 GitHub 계정 초대
2. 저장소 → Settings → Collaborators and teams에서 팀원 권한을 **Write**로 설정

## 5. main 브랜치 보호 설정

1. 저장소 → **Settings** → **Branches** → **Add branch ruleset** (또는 Add rule)
2. 대상 브랜치: `main`
3. 체크할 항목:
   - ✅ Require a pull request before merging
   - ✅ Required approvals: **1**
4. 저장

> 참고: Free 플랜의 private 저장소는 브랜치 보호 기능이 제한될 수 있습니다.
> 설정이 안 되면 "main에 직접 push 금지"를 팀 규칙으로만 운영해도 됩니다.

## 6. 팀원 각자 할 일

```
git clone https://github.com/<organization이름>/everproject.git
```

이후 작업 흐름:

```
git switch -c feat/기능명     # 새 브랜치 만들기
# ... 작업 후 ...
git add .
git commit -m "feat: 기능 설명"
git push -u origin feat/기능명
# GitHub 웹에서 Pull Request 생성 → 팀원 1명 approve → merge
```
