# AGENTS.md

이 저장소에서 작업하는 AI 코딩 에이전트(Claude Code, Codex, Warp 등)를 위한 안내.

## 이 저장소는 무엇인가

전부 Markdown으로 구현된 이식 가능한 에이전트 스킬이다. 런타임 산출물은 `SKILL.md` 하나다: 에이전트가 YAML frontmatter와 편집자 프롬프트를 읽는다. 빌드 단계는 없으며, 특정 하네스 한두 개에만 묶이는 표현은 피한다.

[blader/humanizer](https://github.com/blader/humanizer)의 포크이며, 패턴 전체를 한국어 텍스트 전용으로 재설계했다. upstream의 패턴 추가·수정은 그대로 병합하지 말고, 한국어에 유효한지 판단해 선별 번안한다.

## 주요 파일

- `SKILL.md` — 스킬 본체. 500줄 예산이 차 있어 긴 보조 절은 `references/`로 뺀다(지금은 발표 대본용 `references/spoken-scripts.md`와 학술 원고용 `references/academic-papers.md`). 이식 가능한 YAML frontmatter(`name`, `description`, `license`, `metadata.version`)와 번호 붙은 패턴 목록(Before/After 예시 포함). **이 파일이 진실의 원천이다.**
- `README.md` — 사람용: 설치, 사용법, 패턴 요약 표, 버전 이력. 한국어 우선, 영어 요약 병행.
- `.claude-plugin/plugin.json` — 선택적 Claude Code 플러그인 매니페스트.
- `.claude-plugin/marketplace.json` — `/plugin marketplace add IsaacEryn/humanizer-ko`가 동작하게 하는 단일 저장소 마켓플레이스 항목.
- `scripts/validate-package.py` — 로컬과 CI에서 쓰는 의존성 없는 패키지·동기화 검사.

## 유지보수 계약

`SKILL.md`와 `README.md`는 동기화를 유지해야 한다. 동작이나 내용을 바꿀 때:

- **패턴:** 스킬은 현재 **37개 번호 패턴**을 정의한다. 추가·삭제·번호 변경 시 README 패턴 표와 「37개 탐지 패턴」 제목, 본문의 모든 상호 참조(§N)를 같은 변경에서 함께 고친다. 의도적인 재번호가 아니면 번호를 유지한다. 검증 스크립트가 패턴 번호를 순서까지 비교하므로 새 패턴은 마지막 번호 뒤에 붙인다.
- **버전:** `SKILL.md` frontmatter의 `metadata.version`, `README.md`의 「버전 이력」, `.claude-plugin/plugin.json`의 `version` 세 곳을 함께 올린다. 스킬 버전은 `metadata` 아래에 둔다. 최상위 `version` 키는 Agent Skills 호스트 간 이식성이 없다. (`marketplace.json`은 의도적으로 버전을 생략해 `plugin.json`이 패키지의 단일 출처가 되게 한다.)
- **호환성:** 설치·사용 문구를 하네스 중립으로 유지한다. Markdown 스킬 지침을 읽을 수 있는 어떤 하네스에서도 동작해야 하며, Claude Code·OpenCode·Codex 등은 예시이지 한계가 아니다.
- **검증:** 게시 전에 `python3 scripts/validate-package.py`, `npx skills add . --list`, `claude plugin validate .`를 실행한다.
- **까다로운 수정:** 특정 실패 양상(반복되는 오교정, 예상 밖의 톤 변화)을 잡으려고 프롬프트를 고쳤다면, 무엇을 왜 고쳤는지 README 버전 이력에 짧게 남긴다.

## SKILL.md 편집

- 유효한 YAML frontmatter(형식과 들여쓰기)를 보존한다.
- frontmatter 아래 프롬프트가 곧 제품이다. 코드가 아니라 신중한 지침 문서로 다룬다.
- 예시는 전부 한국어를 유지한다. 감시 표현은 실제 한국어 LLM 출력에서 관찰되는 것이어야 하며, 영어 티의 직역이어서는 안 된다.
