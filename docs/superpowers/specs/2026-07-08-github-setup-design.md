# 설계: EverProject GitHub 저장소 구성

- 날짜: 2026-07-08
- 상태: 승인됨

## 배경

홍익대 캡스톤 디자인 프로젝트. 기업이 심전도 데이터를 제공하고 동아리가 exe 프로토타입 앱을
자체 개발한다. 팀원 4명 이상(Git 경험 혼재), 개발 집중 기간 약 2주, 7/23 캡스톤 월간 보고서
제출(회의록·제작과정·증빙 포함). 기술 스택은 미정.

## 결정 사항

**GitHub Organization + 단일 private 모노레포** 방식을 채택한다.

- 코드·문서(회의록/보고서)·심전도 샘플 데이터를 한 저장소에서 관리
- 커밋 이력이 곧 제작과정 증빙이 되어 캡스톤 보고서 작성에 활용
- Organization 소유라 특정 개인 계정에 종속되지 않음
- 기업 데이터 포함으로 private 필수

### 검토했으나 채택하지 않은 방안

- **개인 계정 저장소**: 한 사람에게 종속, 인수인계 취약 → 기각
- **저장소 분리(app/docs/data)**: 초보 포함 소규모 팀에 관리 부담 과다 → 기각

## 폴더 구조

```
app/            exe 프로토타입 소스 (스택 확정 전까지 README만)
data/samples/   소용량 샘플 데이터만 커밋, 원본은 클라우드 링크
docs/meetings/  회의록 (YYYY-MM-DD-제목.md)
docs/reports/   캡스톤 보고서
docs/planning/  기능 기획, Figma·Affine 링크
```

## 협업 규칙

- `main` 보호: PR로만 병합, 팀원 1명 이상 approve (단순 문서는 셀프 머지 허용)
- 브랜치 이름: `feat/기능명`, `docs/문서명`
- 커밋 메시지: `feat:`, `fix:`, `docs:` 타입 접두어 + 한글 허용

## 데이터 관리

- 저장소에는 파일당 수 MB 이내 샘플만 커밋
- `.gitignore`로 `data/raw/`, 압축파일, 빌드 산출물(exe 포함) 제외
- 빌드된 exe는 GitHub Releases로 배포
- 저장소 private 유지, 팀 외부 공유 금지

## 세팅 절차

1. 로컬: 폴더 구조 + README/.gitignore 생성, `git init`, 첫 커밋 — 완료 대상
2. GitHub 웹: Organization·저장소 생성, 팀원 초대, 브랜치 보호 — `docs/github-setup-guide.md` 참고
3. 팀원: clone 후 브랜치 기반 작업 시작

## 범위 외 (필요 시 추후 도입)

- GitHub Issues/Projects 보드
- Git LFS (샘플 데이터가 커질 경우)
- CI/CD (빌드 자동화)
