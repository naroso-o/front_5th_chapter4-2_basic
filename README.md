# 바닐라 JS 프로젝트 성능 개선

- url: https://hanghae-plus-frontend-5th-4-2.web.app/

## 성능 개선 보고서

| 항목 | 개선 전 점수 | 개선 후 점수 | 개선 이유 | 개선 방법 |
|------|--------------|--------------|-----------|------------|
| LCP 이미지 처리 | 9.83초 | 3.31초 | Hero 이미지가 JPG + lazy로 제공되어 지연 발생 | `<picture>` + WebP + `fetchpriority="high"` + `width/height` 명시 |
| TBT 차단 자원 | 90ms | 0ms | main-thread를 점유하는 JS가 많았음 | JS 분할, `defer` 사용 (`main.js`, `products.js`) |
| 이미지 포맷 | JPG | WebP | 브라우저가 고효율 포맷(WebP) 사용 못함 | `<picture>` + `<source type="image/webp">` 구성 |
| 이미지 크기 명시 | 없음 | 있음 | CLS 발생 (레이아웃 변동) | 모든 `<img>`에 `width`, `height` 속성 명시 |
| 이미지 로딩 방식 | eager | lazy 적용 | 초반 이미지 로딩량 과도 | `loading="lazy"` 사용 (Hero 제외) |
| 렌더링 차단 리소스 | 있음 | 없음 | 외부 폰트 및 스크립트가 렌더링 차단 | `preconnect`, `preload`, `defer`, `async` 적용 |
| 폰트 처리 | 느림 | 개선 | Google Fonts 로딩 지연, 텍스트 FOUT | `font-display: swap`, preload 사용 |
| 웹 접근성 | 82% | 98% | label 누락, contrast 부족 등 | ARIA 라벨 추가, 텍스트 대비 개선 등 |
| SEO | 82% | 100% | 메타 태그 미비, 구조화 부족 | 메타 정보 보완, semantic 구조 개선 |

---

## 🧩 개선 후 향상된 지표 정리

- **Largest Contentful Paint (LCP)**: 9.83s → 3.31s → 이미지 포맷, priority 및 preload로 개선
- **Cumulative Layout Shift (CLS)**: 0.011 → 0.048 → 이미지 크기 명시 및 폰트 처리로 안정화
- **Total Blocking Time (TBT)**: 90ms → 0ms → JS 최적화 및 `defer` 처리
- **Performance 점수**: 72 → 92
- **Accessibility 점수**: 82 → 98
- **SEO 점수**: 82 → 100


*INP (Interaction to Next Paint)는 두 테스트 모두 N/A 상태로 측정되지 않음.