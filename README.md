# Auto-Store (쿠팡 및 스마트 스토어 관리 시스템)

## 프로젝트 개요

Auto-Store는 다양한 이커머스 채널(네이버, 쿠팡 등)과 온채널(Onch) 시스템을 연동하여 상품, 주문, 배송, 재고 등을 자동으로 관리하는 마이크로서비스 아키텍처(MSA) 기반 시스템입니다.

## Service Repository
- [Mail Service](https://github.com/daechan-jo/auto-store-services-mail.git)
- [Onch Service](https://github.com/daechan-jo/auto-store-services-onch.git)
- [Coupang Service](https://github.com/daechan-jo/auto-store-services-coupang.git)
- [Soldout Service](https://github.com/daechan-jo/auto-store-services-soldout.git)
- [Order Service](https://github.com/daechan-jo/auto-store-services-order.git)
- [Delivery Service](https://github.com/daechan-jo/auto-store-services-delivery.git)
- [Price Service](https://github.com/daechan-jo/auto-store-services-price.git)


## 주요 기능

- **다중 플랫폼 연동**: 네이버, 쿠팡, 온채널 등 여러 이커머스 플랫폼 통합 관리
- **재고 관리**: 품절 상태 자동 모니터링 및 관리
- **주문 처리**: 여러 채널의 주문 정보 수집 및 관리
- **가격 관리**: 상품 가격 비교 및 자동 조정
- **배송 관리**: 송장 처리 및 배송 상태 추적
- **알림 서비스**: 이메일 알림 기능

## 기술 스택

- **언어**: TypeScript
- **프레임워크**: NestJS
- **데이터베이스**: PostgreSQL
- **ORM**: TypeORM
- **메시지 큐**: RabbitMQ
- **웹 스크래핑**: Playwright
- **CI/CD**: Semantic Release
- **기타 도구**: 
  - GitHub Actions
  - Moment.js (시간 처리)
  - UUID (고유 ID 생성)

## 프로젝트 구조

```
auto-store/
├── .github/               # GitHub Action 설정
├── lib/                   # 공통 라이브러리
│   ├── models/            # 데이터 모델 및 인터페이스
│   ├── rabbitmq/          # RabbitMQ 통합 모듈
│   ├── util/              # 유틸리티 기능
│   ├── playwright/        # 웹 스크래핑 도구
│   └── log/               # 로깅 시스템
└── services/              # 마이크로서비스 
    ├── main/              # 메인 서비스
    ├── coupang/           # 쿠팡 연동 서비스
    ├── naver/             # 네이버 연동 서비스 
    ├── onch/              # 온채널 연동 서비스
    ├── order/             # 주문 관리 서비스
    ├── price/             # 가격 관리 서비스
    ├── soldout/           # 품절 관리 서비스
    ├── delivery/          # 배송 관리 서비스
    └── mail/              # 이메일 알림 서비스
```

## 공통 라이브러리

### Models (@daechanjo/models)

데이터 모델과 인터페이스를 정의하는 커스텀 라이브러리로, 서비스 간 일관된 데이터 구조를 제공합니다.

주요 인터페이스:
- 쿠팡 관련 (CoupangProduct, CoupangOrder, CoupangInvoice 등)
- 네이버 관련 (NaverProduct, NaverProductOption 등)
- 온채널 관련 (OnchItem, OnchProduct, OnchSoldout 등)
- 데이터 처리 (ProcessProductData, AdjustData 등)
- RabbitMQ 메시지 (RabbitmqMessage)

### Util (@daechanjo/util)

다양한 유틸리티 기능을 제공하는 커스텀 라이브러리입니다.

주요 기능:
- 로깅 (log, error, warn)
- 스피너 표시 (startSpinner, updateSpinner, stopSpinner)
- 타임아웃 처리 (withTimeout)
- 고유 ID 생성 (generateCronId)
- 한국 시간 관련 유틸리티 (createTodayKoreaTime, convertKoreaTime)
- 제품명 및 옵션 추출 (extractLastPart, extractProductInfo)
- 진행 상황 처리 (processWithProgress)

### RabbitMQ (@daechanjo/rabbitmq)

마이크로서비스 간 통신을 위한 RabbitMQ 커스텀 라이브러리입니다.

## 마이크로서비스

프로젝트는 여러 독립적인 마이크로서비스로 구성되어 있으며, 각 서비스는 특정 비즈니스 도메인을 담당합니다:

- **메인 서비스**: 다른 서비스 관리 및 조정
- **쿠팡 서비스**: 쿠팡 스토어 연동 및 관리
- **네이버 서비스**: 네이버 스토어 연동 및 관리
- **온채널 서비스**: 온채널 시스템 연동
- **주문 서비스**: 주문 정보 수집 및 처리
- **가격 서비스**: 가격 정보 비교 및 조정
- **품절 서비스**: 재고 상태 모니터링
- **배송 서비스**: 배송 정보 관리 및 추적
- **메일 서비스**: 알림 이메일 발송

## 개발 및 배포

```
# 데이터베이스 설정
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=username
DB_PASSWORD=password
DB_DATABASE=database

# RabbitMQ 설정
RABBITMQ_URL=amqp://localhost:5672
RABBITMQ_QUEUE_PREFIX=auto-store

# 플랫폼 API 키 설정
COUPANG_ACCESS_KEY=your_coupang_access_key
COUPANG_SECRET_KEY=your_coupang_secret_key
NAVER_CLIENT_ID=your_naver_client_id
NAVER_CLIENT_SECRET=your_naver_client_secret
ONCH_API_KEY=your_onch_api_key

# 메일 설정
MAIL_HOST=smtp.example.com
MAIL_PORT=587
MAIL_USER=user@example.com
MAIL_PASSWORD=password
```

