# 바닐라 JS 프로젝트 성능 개선

- url: https://hanghae-plus-frontend-5th-4-2.web.app/

## 성능 개선 보고서

(작성 필요)
| 항목 | 개선 전 점수 | 개선 후 점수 | 개선 이유 | 개선 방법 | 개선 후 향상된 지표 |
|------------------|--------------|--------------|---------------------------------------------------------------------------|------------------------------------------------------------------------------------------|---------------------------------------------|
| 이미지 | 0.67초 | 0.42초 | JPG만 사용하고 있었으며, WebP가 존재해도 브라우저가 활용하지 않음 | `<picture>` 태그와 `source` 태그를 사용하여 WebP 우선 제공 | Largest Contentful Paint 개선 |
| 이미지 크기 | N/A | N/A | `width`, `height` 속성이 없는 이미지로 인해 레이아웃 시프트 발생 | 모든 `<img>` 태그에 `width`, `height` 명시 | Cumulative Layout Shift 개선 |
| 이미지 로딩 | - | - | 초기 렌더링에 불필요한 이미지가 로딩됨 | `<img loading="lazy">` 속성 추가 | First Contentful Paint, TTI 개선 |
| JS 리소스 최적화 | 2.3MB | 850KB | 모든 JS 파일이 한 번에 로딩되어 초기 로딩이 지연됨 | 코드 스플리팅, 필요 리소스만 import | Time to Interactive, Total Blocking Time 개선 |
| 폰트 로딩 | - | - | Google Fonts 로딩이 느림 | `preconnect`, `preload` 추가 | First Contentful Paint 개선 |
| 애니메이션 | N/A | N/A | `transform`, `opacity` 사용 없이 애니메이션 처리 | `will-change` 또는 `transform/opacity` 기반으로 수정 | Animation 성능 개선 |
