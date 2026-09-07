# TextFlow — 사이트 (textflow-widget)

> **⚠️ 동시 세션 주의** — 툴·서버·사이트 세션이 동시에 돌 수 있다. 작업 시작 전 `@~/textflow-ops/LOCKS.md` 를 읽고,
> 커밋은 **자기가 편집한 파일만 이름으로 명시**(`git add -A` 금지), 커밋 직전 `git status`로 남의 작업분 섞였는지 확인.

@~/textflow-ops/LOCKS.md

랜딩/다운로드/데모 사이트. GitHub Pages, 도메인 **textflow.co.kr**.

## 위치 / 배포
- 리포: GitHub `charlie71037853-maker/textflow-widget` (branch `main`). push → GitHub Pages 자동배포(1~3분).

## 릴리스 배포 (플러그인 새 버전마다)
1. 빌드된 installer 2개(`.pkg`/`.exe`)를 리포 루트에 복사.
2. `index.html` 다운로드 링크 **6곳** 버전 갱신 (예 `Installer-v1.7.243` → `1.7.244`).
   ※ Win exe는 310부터 파일명에 `Installer` 없음 → `TextFlowPro-v<ver>-trial.exe` (Mac pkg는 `Installer` 유지).
3. **★.git 재비대화 방지**: 이전-이전 버전 installer는 `git rm` (워킹트리에 **[현재 + 롤백 1개]만** 유지). 예: 320 배포 시 318 installer는 `git rm`, 319는 롤백으로 남김.
4. `git add index.html <새 pkg> <새 exe>` (+`git rm <옛 installer>`) → commit → push.
5. 라이브 확인: `https://textflow.co.kr/TextFlowPro-Installer-v<ver>-trial.pkg` (200). Pages 빌드가 느리면 라이브 SHA 직접 폴링.

## 함정 / 주의
- **`.git` 히스토리 정리됨 (2026-09-07: 9.1GB→256MB, filter-repo)** — 과거 installer 블롭 전량 제거·force-push 완료. **재발 방지 = 위 배포 3번(옛 installer `git rm`)을 지킬 것.** installer는 GitHub 50MB 권장 초과 경고만 뜨고 통과(하드리밋 100MB, 우리 50~59MB). 절차=`~/textflow-ops/HANDOFF_site_git_cleanup.md`.
- **Cloudflare gzip → exe "file corrupt"**: 압축이 exe 손상 → **Compression Rule을 none**으로(해결됨). 재발 시 확인.
- GitHub Pages **Enforce HTTPS** 확인.
- 정적 다운로드 링크는 갱신되지만, "새 버전 배지"는 서버 `/api/version/latest`(= server `/admin` 게시) 후에 뜸.

## index.html 구성
- 다운로드 버튼(mac/win 6곳) + 설치 안내(`setInstallOS`/`showInstallGuide`)
- 자막삽입 인터랙티브 데모(iframe) · 공지판(N배지)·장애배너 · '프리미어 무료강의' 탭(`LECTURES` 배열)
- 요금제/크레딧 카드 · 다크모드
- 방문/전환 추적: `sendBeacon` → 백엔드 `/api/visit` (마케팅 퍼널 소스)

## 규칙
- 이모지 금지(사용자 선호). git 커밋 끝: `Co-Authored-By: Claude Opus 4.8 <noreply@anthropic.com>`.
- 크로스도메인(플러그인/서버/광고) 지식은 `~/textflow-ops` 참조.
