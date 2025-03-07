# 마라맵 (MaraMap)

대한민국 마라톤 대회 일정을 한국 지도에 표시하여 사용자가 쉽게 확인할 수 있는 웹 애플리케이션입니다.

## 프로젝트 개요

마라맵은 마라톤 참가자, 러너, 마라톤에 관심 있는 일반인들이 전국의 마라톤 대회 일정을 한눈에 확인할 수 있도록 도와주는 서비스입니다. 한국 지도에 각 지역의 마라톤 대회를 시각적으로 표시하고, 대회 유형별로 구분하여 사용자가 손쉽게 원하는 정보를 찾을 수 있습니다.

## 주요 기능

- **한국 지도 기반 대회 표시**: 메인 화면에 한국 지도를 띄우고, 각 지역의 마라톤 대회를 마커로 표시
- **대회 세부 정보 제공**: 지도 마커를 클릭하면 대회 이름, 일정, 장소, 등록 링크 등 제공
- **필터링 기능**: 대회 날짜, 유형, 지역별 필터링 기능
- **다양한 뷰 제공**: 지도 뷰, 리스트 뷰, 캘린더 뷰 제공

## 기술 스택

- **백엔드**: Ruby on Rails 8.0.1
- **데이터베이스**: SQLite (개발), PostgreSQL (배포)
- **프론트엔드**: Rails 뷰 (ERB), Stimulus.js, Turbo
- **지도 구현**: SVG 기반 한국 지도
- **배포**: Docker, Kamal

## 설치 및 실행 방법

### 요구사항

- Ruby 3.3.0 이상
- Rails 8.0.1
- SQLite3

### 로컬 개발 환경 설정

1. 저장소 클론
   ```bash
   git clone https://github.com/yourusername/maramap.git
   cd maramap
   ```

2. 의존성 설치
   ```bash
   bundle install
   ```

3. 데이터베이스 설정
   ```bash
   bin/rails db:create
   bin/rails db:migrate
   bin/rails db:seed
   ```

4. 서버 실행
   ```bash
   bin/rails server
   ```

5. 브라우저에서 `http://localhost:3000` 접속

## 프로젝트 문서

자세한 정보는 다음 문서들을 참고하세요:

- [상세 PRD](detailed_prd.md) - 상세 제품 요구사항
- [기술 명세서](technical_spec.md) - 기술적 구현 세부사항
- [UI/UX 가이드라인](ui_ux_guidelines.md) - 디자인 가이드라인
- [개발 로드맵](development_roadmap.md) - 개발 진행 계획
- [데이터 소스](data_sources.md) - 데이터 수집 전략

## 라이센스

이 프로젝트는 MIT 라이센스를 따릅니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

## 기여 방법

1. 이 저장소를 포크합니다.
2. 새로운 브랜치를 생성합니다 (`git checkout -b feature/amazing-feature`).
3. 변경사항을 커밋합니다 (`git commit -m 'Add some amazing feature'`).
4. 브랜치에 푸시합니다 (`git push origin feature/amazing-feature`).
5. Pull Request를 생성합니다.

## 연락처

프로젝트 관리자: [이메일 주소]

---

마라맵을 통해 더 많은 사람들이 마라톤의 즐거움을 경험할 수 있기를 바랍니다! 🏃‍♂️🏃‍♀️
