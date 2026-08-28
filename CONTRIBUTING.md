# 협업 가이드 (CONTRIBUTING)

탑퀀트 대시보드에 함께 작업해 주셔서 감사합니다. **이 문서만 따라오시면 됩니다.**

---

## 0. 먼저 읽을 것

- **[`PROJECT_NOTES.md`](PROJECT_NOTES.md)** — 프로젝트 전체 맥락(투자 전략 프레임, 보드별 설계, 데이터 API, 알려진 제약). **작업 전에 꼭 한 번 읽어주세요.**
- AI(ChatGPT·Claude 등)에게 시킬 때는 이렇게 시작하면 좋습니다:
  > "https://raw.githubusercontent.com/topbanker99-ai/topquant-dashboards/main/PROJECT_NOTES.md 를 읽고, 그 규칙에 맞춰 수정해줘"

## 1. 이 프로젝트의 구조 (5초 요약)

- **빌드 도구가 없습니다.** 각 보드는 HTML 파일 하나에 CSS·JS가 전부 들어 있습니다. 파일을 고치면 그게 곧 배포물입니다.
- 데이터는 전부 `https://fred-proxy-nine.vercel.app` 프록시를 통해 브라우저에서 직접 호출합니다. **API 키는 저장소에 없습니다**(Vercel 환경변수에 보관).
- `main`에 머지되면 GitHub Pages와 Vercel에 자동 배포됩니다(1~2분).

```
index.html              허브(메인 페이지)
topquant_buy.html       매수 시점 보드
topquant_sell.html      매도 시점 보드
topquant_compare.html   글로벌 비교차트
topquant_fx.html        원/달러 방향 보드
topquant_*.html         기타 보드(매크로·국채·뉴스·실시간·시장맵·연금·버핏)
assets/                 이미지 에셋
PROJECT_NOTES.md        프로젝트 인수인계 노트
```

## 2. 작업 방법 (편한 것 하나 고르세요)

### 방법 A — GitHub 웹에서 바로 편집 (가장 쉬움)
1. 저장소에서 고칠 파일 클릭 → 오른쪽 위 **연필 아이콘(✏️)**
2. 내용 수정 (AI에게 받은 코드를 붙여넣어도 됩니다)
3. 아래 **Commit changes** → **Create a new branch** 선택 → **Propose changes**
   - ⚠️ "Commit directly to the main branch"는 **선택하지 마세요**
4. 자동으로 PR 작성 화면이 뜹니다 → 제목·설명 쓰고 **Create pull request**

### 방법 B — 로컬에서 작업
```bash
git clone https://github.com/topbanker99-ai/topquant-dashboards.git
cd topquant-dashboards
git checkout -b feat/무엇을-고쳤는지          # 브랜치 생성
# ... 파일 수정 ...
git add -A && git commit -m "feat(fx): 설명"
git push -u origin feat/무엇을-고쳤는지
# GitHub에 뜨는 "Compare & pull request" 버튼 클릭
```

## 3. 지켜주셨으면 하는 규칙

| 규칙 | 이유 |
|---|---|
| **`main`에 직접 푸시 금지 — 반드시 PR** | 검토 없이 실서비스에 나갑니다 |
| **브랜치 이름**: `feat/...`, `fix/...`, `docs/...` | 무슨 작업인지 한눈에 |
| **한 PR = 한 주제** | 리뷰·되돌리기가 쉬워집니다 |
| **PR 설명에 "무엇을·왜"** 를 적기 | 나중에 이력을 봤을 때 이해됩니다 |
| **디자인 토큰 유지** (`--bg`, `--teal`, `--rose` 등 CSS 변수 사용) | 12개 보드의 톤이 통일돼 있습니다 |
| **상단 네비게이션(topnav)을 고칠 땐 12개 파일 모두** | 한 곳만 고치면 메뉴가 어긋납니다 |

### 건드리기 전에 상의가 필요한 것
- **신호 판정 로직의 임계값**(매수·매도 보드의 숫자 기준) — 2년 백테스트로 정해진 값입니다. 바꾸려면 근거 데이터가 필요합니다. 자세한 내용은 `PROJECT_NOTES.md` §5-1.
- **프록시 엔드포인트 추가/변경** — 별도 저장소(`fred-proxy`)와 Vercel 배포가 얽혀 있습니다.
- `assets/og.png`, 파비콘 — 브랜드 자산입니다.

## 4. PR 올리기 전 셀프 체크

- [ ] 브라우저에서 해당 HTML 파일을 열어 **에러 없이 뜨는지** 확인 (F12 → Console에 빨간 에러 0)
- [ ] 화면이 깨지지 않는지 (모바일 폭에서도)
- [ ] 다른 보드로 이동하는 상단 메뉴가 정상인지
- [ ] 숫자·신호가 나오는 보드라면 값이 상식적인지

> 검증 환경이 마땅치 않으면 **그냥 PR을 올리고 설명에 "검증 부탁드립니다"라고 적어주세요.** 저장소 주인이 헤드리스 브라우저 + 실데이터로 검증한 뒤 머지합니다.

## 5. PR을 올린 뒤

- 저장소 주인이 검토하고 **머지(= 운영 반영)** 합니다. 머지 후 1~2분이면 라이브에 반영됩니다.
- 수정 요청이 달리면 **같은 브랜치에 추가 커밋**하면 PR에 자동 반영됩니다(새 PR 만들 필요 없음).
- 급하지 않은 아이디어는 **Issues** 탭에 남겨주셔도 좋습니다.

## 6. 라이브 주소

- 메인: https://topbanker99-ai.github.io/topquant-dashboards/
- 미러(더 빨리 반영): https://topquant-dashboards.vercel.app/

---

**막히면 그냥 물어보세요.** 잘못 올려도 되돌릴 수 있으니(PR revert) 부담 없이 시작하시면 됩니다.
