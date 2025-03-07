# 마라맵 - 기술 명세서 (Technical Specification)

## 1. 시스템 아키텍처

### 1.1 전체 아키텍처
- **프레임워크**: Ruby on Rails 8.0.1
- **아키텍처 패턴**: MVC (Model-View-Controller)
- **배포 환경**: Docker 컨테이너 (Kamal을 통한 배포)

### 1.2 주요 컴포넌트
- **프론트엔드**: Rails 뷰 (ERB/HAML), Stimulus.js, Turbo
- **백엔드**: Ruby on Rails 컨트롤러 및 모델
- **데이터베이스**: SQLite (개발), PostgreSQL (배포)

## 2. 데이터베이스 설계

### 2.1 엔티티 관계도 (ERD)
- **Marathon (마라톤 대회)**
  - id: integer (PK)
  - name: string (대회 이름)
  - date: date (개최 일자)
  - location: string (개최 지역/장소명)
  - location_x: float (지도 상 X 좌표)
  - location_y: float (지도 상 Y 좌표)
  - race_type: string (대회 유형 - 풀마라톤, 하프마라톤 등)
  - registration_link: string (대회 등록 링크)
  - fee: string (참가비)
  - capacity: integer (참가 인원 제한)
  - deadline: date (등록 마감일)
  - course_map: text (코스 정보)
  - created_at: datetime
  - updated_at: datetime

### 2.2 인덱스
- Marathon 테이블:
  - date (검색 최적화)
  - race_type (필터링 최적화)
  - location (지역별 검색 최적화)

## 3. 백엔드 설계

### 3.1 컨트롤러
- **MarathonsController**
  - index: 대회 목록 표시 (지도 및 리스트 뷰)
  - show: 특정 대회 상세 정보 표시
  - filter: 필터링된 대회 목록 반환 (AJAX 요청 처리)

### 3.2 모델
- **Marathon 모델**
  - 유효성 검증
  - 범위 지정 메서드 (날짜별, 유형별, 지역별 필터링)
  - 검색 메서드

### 3.3 API 설계 (내부용)
- **GET /marathons.json** - 모든 대회 정보 반환
- **GET /marathons/filter.json?date_start=X&date_end=Y&race_type=Z&location=W** - 필터링된 대회 목록 반환

## 4. 프론트엔드 설계

### 4.1 페이지 구성
- **메인 페이지 (/)**: 
  - 한국 지도 + 마라톤 대회 마커
  - 필터링 옵션
- **대회 상세 페이지 (/marathons/:id)**:
  - 대회 상세 정보
  - 등록 링크
- **목록 페이지 (/marathons/list)**:
  - 대회 리스트 형태 보기
- **캘린더 페이지 (/marathons/calendar)**:
  - 대회 일정 캘린더 형태로 보기

### 4.2 컴포넌트
- **지도 컴포넌트**: SVG 기반 한국 지도 + 마커 표시
- **필터 컴포넌트**: 날짜/유형/지역별 필터링 UI
- **대회 카드 컴포넌트**: 대회 정보 요약 표시
- **상세 정보 컴포넌트**: 대회 상세 정보 표시

### 4.3 자바스크립트
- **Stimulus 컨트롤러**:
  - map_controller.js: 지도 상호작용 처리
  - filter_controller.js: 필터링 처리
  - calendar_controller.js: 캘린더 처리

## 5. 지도 구현 상세

### 5.1 SVG 지도
- 간략화된 한국 지도 SVG 파일
- 지역별 path 요소에 ID 부여 (예: `<path id="seoul" ...>`)
- 클릭 가능한 지역 구현

### 5.2 마커 표시
- 대회 위치에 따라 SVG 상에 마커 배치
- 마커 위치 좌표 계산 방식:
  - SVG 좌표계 (0, 0)은 지도의 좌상단
  - location_x, location_y는 0.0 ~ 1.0 사이의 값으로 상대적 위치 표현

### 5.3 인터랙션
- 마커 클릭: 해당 대회 상세 정보 모달 표시
- 지역 클릭: 해당 지역 대회 목록 필터링
- 확대/축소: SVG viewBox 조정으로 구현

## 6. 데이터 관리

### 6.1 초기 데이터 로드
- 기본 마라톤 대회 데이터 시드 파일 작성
- db/seeds.rb를 통한 초기 데이터 생성

### 6.2 데이터 업데이트
- Rake 태스크를 통한 주기적인 데이터 업데이트 가능성
- 외부 API 연동 방안 (향후 확장)

## 7. 성능 최적화

### 7.1 데이터베이스 최적화
- 적절한 인덱싱
- N+1 쿼리 방지

### 7.2 프론트엔드 최적화
- 이미지/자산 최적화
- 클라이언트측 캐싱

## 8. 보안 고려사항

### 8.1 데이터 보안
- 외부 링크 보안 검증
- CSRF 보호

### 8.2 입력 검증
- 모든 사용자 입력에 대한 유효성 검증
- XSS 방지

## 9. 테스팅 전략

### 9.1 단위 테스트
- 모델 테스트: 유효성 검증, 범위 메서드
- 컨트롤러 테스트: 응답 상태, 뷰 렌더링

### 9.2 통합 테스트
- 사용자 흐름 테스트
- JavaScript 기능 테스트

## 10. 배포 전략

### 10.1 배포 환경
- Docker 컨테이너
- Kamal을 통한 배포 자동화

### 10.2 모니터링
- 예외 모니터링
- 성능 모니터링

---

이 기술 명세서는 개발 과정에서 계속 업데이트됩니다. 