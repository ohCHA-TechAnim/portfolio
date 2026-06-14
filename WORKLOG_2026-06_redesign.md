# 포트폴리오 작업 로그 — 2026-06 리디자인 세션

> 이 문서는 Claude(채팅)와의 작업 세션 기록입니다. Claude Code가 이어서 작업할 때 컨텍스트로 사용하세요.

## 대상 파일
- `portfolio.html` — 단일 파일 트릴링궐(KO/EN/ZH) TA 포트폴리오
- `og_thumb.png` — 링크드인/OG 썸네일 (1200×630, 미니멀 모노톤)

## 배포
- GitHub Pages: https://ohcha-techanim.github.io/portfolio/portfolio.html
- Cloudflare Pages: 연결 시도 중 (파일당 25MB 제한 이슈 → WebP 전환으로 해결)
- 캐시버스팅: URL에 `?v=N` 증가

---

## 이번 세션 변경 내역 (요약)

### 구조
- 탭: 커리어(기본) / 플러그인 / 리깅 / 애니메이션
- **애니 탭**: 01 First Descendant(넥슨게임즈, 유튜브 B619JNrayFo, "언리얼 피직스 세컨더리 애니메이션") / 02 IP 콜라보 / 03 캐릭터 스킨 리타게팅(가로 캐러셀 #skinTrack) / 04 인게임 / 05 아웃게임 / 06 데모릴 — 전부 유튜브 facade
- **리깅 탭**: 01 커스텀 페이셜 리그(step player, 초기 STEP4) + R&D 아코디언 / 02 커스텀 바디 리그(2열 그리드, 07·08 풀폭 feature)

### 미디어
- **모든 GIF → WebP 전환 완료** (body 8 + facial 4 + plugin 8 = 20개). HTML 경로 `.gif`→`.webp` 치환됨. 로고는 PNG 유지.
- 퍼스트 디센던트는 344MB GIF → 유튜브 임베드로 대체
- 유튜브 8개 전부 facade 방식(썸네일 + 클릭 시 iframe 주입, 초기 iframe 0)

### 리디자인 (portfolio_redesign_spec.md Phase 0~4 전체 반영)
- **Phase 0**: 디자인 토큰 (배경 3단계 #0d1117/#151b23/#1c242e, 보더 2단계, 악센트 #6fd3c7, 간격 토큰)
- **Phase 1**: 글로우 전부 제거, 전화번호 삭제, SVG 스프라이트(유니코드 UI 제거), 🏆→배지, 中→ZH
- **Phase 2**: 라이트박스(클릭 확대/ESC/배경클릭), 캡션 가독성, 유튜브 facade, alt 전수 입력
- **Phase 3**: 히어로 축소, 메트릭 리스타일(큰 숫자 위로), 라벨 PROBLEM/SOLUTION/IMPACT 통일, 바디 2열 그리드, 배너 타이포배너(워터마크 숫자), 사이드내비 1440 이하 숨김
- **Phase 4**: 미니 푸터(한 줄 연락처 — CTA 제거, 아웃바운드 컨택용이므로)

### 텍스트 수정
- 플러그인 01: "이터널 리턴에서 캐릭터 스킨 70종을 LOD 단계별로 각각 두 개씩..." (한국어; EN/ZH도 반영됨)
- 플러그인 03: "바이패드 Fig 파일을 리스트업한 후 관리해..."
- 한자 이름 수정: 车昇炫 → **车胜炫** (수레車·이길勝·밝을炫의 간체)

---

## 알려진 후속 작업 (TODO)
- [ ] WebP 전환 후 Cloudflare Pages 재배포 확인 (25MB 통과되는지)
- [ ] `og_thumb.png`를 PortfolioWeb 루트에 push (OG 메타태그가 이 경로 참조)
- [ ] 스킨 리타게팅 캐러셀(#skinTrack)에 추가 영상 채우기 — 현재 아이작 1개 + 주석 템플릿
- [ ] 영어/중국어 플러그인 설명을 최신 한국어 디테일과 완전 동기화 (일부 구버전 잔존 가능)
- [ ] (선택) 본문 히어로의 경력 배지 — 시한부 정보라 "2020~" 시작연도 표기 검토

## 기술 메모
- Python은 `py -3` (bare python은 2.7)
- 업데이트: `Copy-Item Downloads\portfolio.html PortfolioWeb\ -Force` → git add/commit/push
- 배포 검증: `Select-String -Path portfolio.html -Pattern "키워드"`
- file:// 로컬은 WebP/이미지 보안차단 → http 서버나 GitHub Pages 필요
