# GitHub 세팅 가이드 (웹에서 직접 할 것들)

저장소: https://github.com/Hongik-SemiColon/EverProject

로컬 저장소와 원격 연결은 완료되어 있습니다. 아래는 GitHub 웹사이트에서 팀장이 직접 해야 하는 절차입니다.

## 1. 팀원 초대

1. Organization(`Hongik-SemiColon`) → **People** → **Invite member** — 팀원 GitHub 계정 초대
2. 저장소 → **Settings** → **Collaborators and teams**에서 팀원 권한을 **Write**로 설정

## 2. 기본 브랜치를 develop으로 변경

평소 작업 PR이 `develop`으로 향하도록 기본 브랜치를 바꿉니다.

1. 저장소 → **Settings** → **General** → **Default branch**
2. 연필 아이콘 클릭 → `develop` 선택 → 저장

## 3. 브랜치 보호 설정 (⭐ 머지에 리뷰 1명 필수)

`main`과 `develop` 두 브랜치 모두 보호합니다.

1. 저장소 → **Settings** → **Rules** → **Rulesets** → **New ruleset** → **New branch ruleset**
2. Ruleset name: `protect-main-develop`
3. Enforcement status: **Active**
4. Target branches → **Add target** → **Include by pattern**으로 `main`과 `develop` 각각 추가
5. Rules(Branch rules)에서 체크:
   - ✅ **Require a pull request before merging**
     - Required approvals: **1**
6. **Create** 클릭

> 이 설정 후에는 `main`·`develop`에 직접 push가 불가능하고,
> 팀원 1명 이상이 approve한 PR만 머지할 수 있습니다.
>
> 참고: Free 플랜의 **private** 저장소는 ruleset/branch protection이 적용되지 않을 수 있습니다.
> 설정이 동작하지 않으면 (a) 저장소를 public으로 전환하거나(기업 데이터 주의 — 비추천),
> (b) "직접 push 금지 + 리뷰 후 머지"를 팀 규칙으로 운영하세요.

## 4. 팀원 각자 할 일

```
git clone https://github.com/Hongik-SemiColon/EverProject.git
```

이후 작업 흐름은 [CONTRIBUTING.md](../CONTRIBUTING.md) 참고:

```
git switch develop
git pull origin develop
git switch -c feat/#이슈번호-제목
# ... 작업 후 ...
git add .
git commit -m "feat: 기능 설명"
git push -u origin feat/#이슈번호-제목
# GitHub 웹에서 develop 대상으로 Pull Request 생성 → 팀원 1명 approve → merge
```
