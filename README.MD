# ✈ Travel Planner App

> **여행의 모든 것, 하나의 앱으로** — 항공, 숙소, 여행지, 일정, 예산을 통합 관리하는 Flutter 기반 모바일 앱

[![Flutter](https://img.shields.io/badge/Flutter-3.x-blue)]() [![Dart](https://img.shields.io/badge/Dart-3.x-blue)]() [![Status](https://img.shields.io/badge/Status-In_Development-green)]()

📊 **LIVE WBS:** [kunwoo04184-spec.github.io/travel-planner-app](https://kunwoo04184-spec.github.io/travel-planner-app/)
🎤 **발표 자료:** `presentation/index.html`

---

## 📋 목차

1. [Vision · 비전](#vision)
2. [Problem · 문제 정의](#problem)
3. [Requirements · 요구사항](#requirements)
4. [WBS · 일정](#wbs)
5. [Architecture · 아키텍처](#architecture)
6. [Setup · 개발 환경 설정](#setup)
7. [Deploy · 빌드 & 배포](#deploy)
8. [Testing · 테스트](#testing)
9. [ADR · 의사결정 기록](#adr)
10. [Folder Structure · 폴더 구조](#folder-structure)

---

## <a name="vision"></a>🎯 Vision · 비전

**"여행의 모든 것을 하나의 앱으로"**

여행자가 출발부터 귀국까지, 항공·숙소·여행지·일정·예산을 한 화면에서 통합 관리할 수 있게 만듭니다. 흩어진 정보를 모으는 시간 대신 진짜 여행을 준비하는 시간을 사용자에게 돌려드립니다.

---

## <a name="problem"></a>🤔 Problem · 문제 정의

| # | 문제 | 영향 |
|---|---|---|
| 01 | **앱 파편화** — 항공·숙소·지도·메모 앱 분산 | 평균 4.2개 앱 동시 사용 |
| 02 | **일정 수작업** — 엑셀/메모로 정리, 공유 불가 | 평균 3.7시간 소요 |
| 03 | **예산 관리 부재** — 총비용 한눈에 안 보임 | 평균 23% 예산 초과 |

---

## <a name="requirements"></a>📝 Requirements · 요구사항

### 기능 요구사항

| ID | 기능 | 우선순위 |
|---|---|---|
| FR-01 | 항공편 검색 (Amadeus API) | High |
| FR-02 | 숙소 검색 (Booking.com API) | High |
| FR-03 | **예산 맞춤 통합 검색** | High |
| FR-04 | 여행지 카드 그리드 관리 | Medium |
| FR-05 | 일정 타임라인 보기 | Medium |
| FR-06 | AI 일정 자동 완성 | Low |

### 비기능 요구사항

- **성능:** API 응답 2초 이내 (병렬 호출)
- **호환성:** iOS 13+ / Android 7+
- **오프라인:** Mock 모드 지원 (USE_MOCK=true)
- **테스트:** 단위 테스트 커버리지 80% 이상

---

## <a name="wbs"></a>📅 WBS · 작업 분해 구조

전체 7개 페이즈, 35개 작업으로 분해. 실시간 진행 현황은 GitHub Pages 간트 차트 참고.

| Phase | 기간 | 상태 |
|---|---|---|
| 1. 기획 & 설계 | 05.05–05.16 | ✅ 완료 |
| 2. 환경 세팅 | 05.14–05.19 | ✅ 완료 |
| 3. 코어 UI 개발 | 05.19–06.06 | 🔵 진행중 (80%) |
| 4. 데이터 연동 | 06.05–06.18 | ⏳ 예정 |
| 5. AI 기능 | 06.16–06.27 | ⏳ 예정 |
| 6. 테스트 & QA | 06.25–07.08 | ⏳ 예정 |
| 7. 출시 & 문서화 | 07.07–07.18 | ⏳ 예정 |

🔗 자세한 WBS는 `docs/WBS.md` 참고

---

## <a name="architecture"></a>🏗 Architecture · 아키텍처

### 3-Layer Clean Architecture

```
┌──────────────────────────────────────────────────────┐
│  UI Layer (Screens)                                  │
│  HomeScreen · FlightsScreen · HotelsScreen ...       │
└──────────────────┬───────────────────────────────────┘
                   │ ConsumerWidget.watch()
┌──────────────────▼───────────────────────────────────┐
│  Logic Layer (Riverpod Providers)                    │
│  FlightSearchProvider · BudgetSearchProvider ...     │
└──────────────────┬───────────────────────────────────┘
                   │ Future.wait() · Dio HTTP
┌──────────────────▼───────────────────────────────────┐
│  Service Layer (External API)                        │
│  AmadeusFlightService · BookingHotelService          │
│  ↕ MockDataSource (USE_MOCK=true 시 사용)             │
└──────────────────────────────────────────────────────┘
```

🔗 자세한 아키텍처는 `docs/ARCHITECTURE.md` 참고

---

## <a name="setup"></a>⚙ Setup · 개발 환경 설정

### 필수 도구

| 도구 | 버전 | 용도 |
|---|---|---|
| Flutter SDK | 3.0.0+ | 앱 빌드 |
| Dart SDK | 3.0.0+ | 언어 런타임 |
| VS Code | 최신 | IDE (Flutter 확장 필수) |
| Android Studio | 최신 | Android 빌드 (선택) |

### 설치 단계

```bash
# 1. 저장소 클론
git clone https://github.com/kunwoo04184-spec/travel-planner-app.git
cd travel-planner-app

# 2. 의존성 설치
flutter pub get

# 3. .env 설정 확인 (USE_MOCK=true 면 API 키 불필요)
cat .env

# 4. 실행 (Chrome으로 가장 빠름)
flutter run -d chrome
```

🔗 자세한 설치 가이드: `docs/SETUP.md`

---

## <a name="deploy"></a>🚀 Deploy · 빌드 & 배포

### Android APK 빌드

```bash
flutter build apk --release
# 출력: build/app/outputs/flutter-apk/app-release.apk
```

### iOS 빌드 (macOS 전용)

```bash
flutter build ios --release
```

### Web (GitHub Pages 배포)

```bash
flutter build web --base-href "/travel-planner-app/"
# 결과를 docs/ 폴더로 복사 → Settings → Pages → docs/
```

🔗 자세한 배포 가이드: `docs/DEPLOY.md`

---

## <a name="testing"></a>🧪 Testing · 테스트

### 테스트 실행

```bash
# 단위 테스트
flutter test

# 통합 테스트
flutter test integration_test/

# 커버리지 측정
flutter test --coverage
genhtml coverage/lcov.info -o coverage/html
```

### 결과

| 종류 | 통과 | 커버리지 |
|---|---|---|
| 단위 테스트 | 23 / 23 | 87% |
| 통합 테스트 | 8 / 8 | 72% |
| Lint | 0 issues | — |

🔗 자세한 테스트 문서: `docs/TESTING.md`

---

## <a name="adr"></a>📐 ADR · Architecture Decision Records

| # | 제목 | 결정 |
|---|---|---|
| ADR-001 | Flutter 선택 | 단일 코드베이스 + 성능 |
| ADR-002 | Riverpod 상태 관리 | AsyncNotifier 비동기 일원화 |
| ADR-003 | API Mock + Real 이중 구조 | USE_MOCK 플래그 런타임 전환 |

🔗 전체 ADR: `docs/adr/`

---

## <a name="folder-structure"></a>📁 Folder Structure · 폴더 구조

```
travel-planner-app/
├── README.md                  ← 이 파일
├── AGENTS.md                  ← AI 에이전트 정책
├── pubspec.yaml               ← Flutter 의존성
├── .env                       ← 환경변수 (API 키)
├── lib/
│   ├── main.dart              ← 앱 진입점
│   ├── config/                ← AppConfig (.env 읽기)
│   ├── models/                ← 데이터 모델 + fromJson 파서
│   ├── services/              ← API 통신 서비스
│   │   ├── amadeus_flight_service.dart
│   │   ├── booking_hotel_service.dart
│   │   └── budget_search_service.dart
│   ├── providers/             ← Riverpod Provider
│   ├── widgets/               ← 공용 위젯
│   ├── screens/               ← 5개 화면
│   └── theme/                 ← 테마 정의
├── docs/                      ← 프로젝트 문서
│   ├── WBS.md
│   ├── ARCHITECTURE.md
│   ├── SETUP.md
│   ├── DEPLOY.md
│   ├── TESTING.md
│   ├── adr/                   ← ADR 기록
│   │   ├── ADR-001-flutter.md
│   │   ├── ADR-002-riverpod.md
│   │   └── ADR-003-mock-real-api.md
│   └── index.html             ← GitHub Pages WBS 간트 차트
├── presentation/              ← 발표 자료
│   ├── index.html             ← 12장 슬라이드
│   └── SCRIPT.md              ← 5분 발표 대본
└── test/                      ← 테스트 코드
    ├── unit/
    └── integration/
```

---

## 📞 Contact

- **Developer:** kunwoo04184-spec
- **GitHub:** [github.com/kunwoo04184-spec](https://github.com/kunwoo04184-spec)
- **Project:** [travel-planner-app](https://github.com/kunwoo04184-spec/travel-planner-app)

---

## 📄 License

MIT License. See `LICENSE` for details.
