# Monad Standard Flake Templates

Monad 팀의 개발 환경을 표준화하기 위한 `flake.nix` 템플릿 레포지토리입니다.

이 레포지토리는 프로젝트 분야별(Web / Backend / App / Infra 등)로 공통 개발 환경을 제공하며,
모든 팀원이 동일한 도구/버전/의존성으로 개발할 수 있도록 설계되었습니다.

---

## 1. 목적

본 레포지토리는 다음 목표를 가집니다.

- 팀 전체 개발 환경의 표준화
- "내 컴퓨터에서는 되는데" 문제 제거
- 프로젝트별 의존성 차이 최소화
- CI(GitHub Actions)와 로컬 개발환경 일치
- 배포 환경과 개발 환경 정합성 강화

---

## 2. 기본 원칙

- 모든 신규 프로젝트는 이 레포의 템플릿 중 하나를 기반으로 생성하는 것을 원칙으로 합니다.
- 모든 프로젝트는 Nix 기반 빌드/실행이 가능해야 합니다.
- CI에서는 Nix 기반 빌드가 존재해야 하며, Actions 성공을 merge 기준으로 삼습니다.
- 포맷팅(Formatting) 체크 실패 시 merge는 불가합니다.

---

## 3. 디렉토리 구조(예시)

이 레포는 아래와 같은 형태로 템플릿을 관리합니다.

- `templates/`
  - `web/`
    - `flake.nix`
    - `README.md`
  - `backend/`
    - `flake.nix`
    - `README.md`
  - `app/`
    - `flake.nix`
    - `README.md`
  - `infra/`
    - `flake.nix`
    - `README.md`
- `modules/`
  - 공통 모듈(devShell, formatter, lint 등)을 재사용 가능한 형태로 관리
- `.github/workflows/`
  - 템플릿 검증 및 CI 실행

실제 구조는 팀 운영 방식에 맞게 확장 가능합니다.

---

## 4. 포함되는 표준 구성

템플릿은 아래 요소들을 포함하는 것을 목표로 합니다.

- `devShell` 제공 (개발용 쉘 환경)
- 팀에서 사용하는 표준 도구 제공
  - formatter
  - linter
  - build toolchain
  - language runtime (Node / Python / Rust 등)
- `nix flake check` 지원
- CI에서 그대로 사용 가능한 구성

---

## 5. 사용 방법

### 5.1 빠른 진입(devShell)

프로젝트 루트에 `flake.nix`가 존재한다면 아래로 개발 환경 진입이 가능합니다.

```bash
nix develop
