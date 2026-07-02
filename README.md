# 탑퀀트 대시보드 (TopQuant Dashboards)

금융 시장 모니터링용 단일 페이지 대시보드 모음.

## 구성
- **topquant_macro.html** — 매크로·유동성 (FRED 30개 지표 + 클릭 해석). Vercel 프록시(fred-proxy) 연동
- **topquant_treasury.html** — 미국채 발행·소화 + 국가부채 (TreasuryDirect·FiscalData)
- **topquant_news.html** — 시장 영향 인물 18인 뉴스 브리핑 (Google News RSS)
- **topquant_realtime.html** — 실시간 가격 보드 (코인 Upbit + 주식 KIS)
- **topquant_compare.html** — 글로벌 비교차트 (지수 7종+환율+연준금리 토글 오버레이, 기간 시작 대비 정규화)
- **index.html** — 위 4개로 가는 허브 페이지

## 데이터
- 매크로: 회장님 Vercel 프록시 `fred-proxy-nine.vercel.app/api/fred` (키는 서버 보관)
- 국채/뉴스/가격: 공개 API 또는 공개 프록시 (브라우저에서 직접)

## 수정
이 저장소를 Claude Code(웹/PC)로 열어 수정 요청 → PR → 머지하면 반영됩니다.
