# Weave ERP 시스템 아키텍처

## 🏗️ 시스템 개요

Weave는 독립적으로 비즈니스를 운영하는 프리랜서, 소상공인, 전문직, 크리에이터를 위한 통합 관리 플랫폼으로, 견적-계약-인보이스-세무 변환까지의 전체 워크플로우를 지원합니다.

## 📦 핵심 모듈

### 1. Dashboard Module (대시보드)
- **DashboardContainer**: 메인 대시보드 컨테이너
- **InsightCard**: 룰 기반 인사이트 카드 컴포넌트
- **MetricChart**: 차트 및 그래프 컴포넌트
- **QuickActions**: 빠른 실행 버튼 그룹

### 2. Invoice Module (인보이스 관리)
- **InvoiceList**: 인보이스 목록 및 필터
- **InvoiceForm**: 인보이스 생성/편집 폼
- **InvoiceDetail**: 인보이스 상세 뷰
- **PaymentTracker**: 입금 추적 컴포넌트
- **ReminderSettings**: 리마인드 규칙 설정

### 3. Tax Export Module (세무 변환)
- **TaxExporter**: 국세청 양식 변환 엔진
- **ExportPreview**: 내보내기 미리보기
- **TaxPackageGenerator**: 세무 패킷 생성기
- **NTSFormatter**: 국세청 포맷 변환기

### 4. Document Template Module (문서 템플릿)
- **TemplateEngine**: 템플릿 변수 처리 엔진
- **TemplateEditor**: 템플릿 편집기
- **TemplatePreview**: 미리보기 컴포넌트
- **VariableManager**: 변수 관리자

### 5. CRM Module (고객 관리)
- **ClientList**: 고객 목록
- **ClientForm**: 고객 정보 입력
- **ClientDetail**: 고객 상세 정보
- **ProjectManager**: 프로젝트 관리

## 🎨 UI 컴포넌트 구조

```
src/
├── components/
│   ├── ui/                    # 기본 UI 컴포넌트
│   │   ├── Button.tsx         # ✅ 구현됨
│   │   ├── Card.tsx           # ✅ 구현됨
│   │   ├── Input.tsx          # ✅ 구현됨
│   │   ├── Table.tsx          # 🆕 추가 필요
│   │   ├── Modal.tsx          # 🆕 추가 필요
│   │   ├── Select.tsx         # 🆕 추가 필요
│   │   ├── DatePicker.tsx     # 🆕 추가 필요
│   │   └── Tabs.tsx           # 🆕 추가 필요
│   │
│   ├── dashboard/             # 대시보드 컴포넌트
│   │   ├── DashboardLayout.tsx
│   │   ├── InsightCard.tsx
│   │   ├── MetricChart.tsx
│   │   └── QuickActions.tsx
│   │
│   ├── invoice/              # 인보이스 컴포넌트
│   │   ├── InvoiceList.tsx
│   │   ├── InvoiceForm.tsx
│   │   ├── InvoiceDetail.tsx
│   │   └── PaymentTracker.tsx
│   │
│   ├── tax/                  # 세무 변환 컴포넌트
│   │   ├── TaxExporter.tsx
│   │   ├── ExportPreview.tsx
│   │   └── NTSFormatter.tsx
│   │
│   ├── template/             # 템플릿 컴포넌트
│   │   ├── TemplateEditor.tsx
│   │   ├── TemplatePreview.tsx
│   │   └── VariableManager.tsx
│   │
│   └── crm/                  # CRM 컴포넌트
│       ├── ClientList.tsx
│       ├── ClientForm.tsx
│       └── ProjectManager.tsx
│
├── lib/
│   ├── types/               # TypeScript 타입 정의
│   │   ├── invoice.ts
│   │   ├── client.ts
│   │   ├── project.ts
│   │   └── tax.ts
│   │
│   ├── utils/              # 유틸리티 함수
│   │   ├── formatter.ts
│   │   ├── validator.ts
│   │   └── calculator.ts
│   │
│   └── services/           # 비즈니스 로직
│       ├── invoiceService.ts
│       ├── taxService.ts
│       └── templateService.ts
│
└── app/
    ├── dashboard/          # 대시보드 페이지
    ├── invoices/          # 인보이스 페이지
    ├── tax/               # 세무 변환 페이지
    ├── templates/         # 템플릿 관리 페이지
    └── clients/           # 고객 관리 페이지
```

## 🔄 데이터 플로우

```
사용자 입력
    ↓
컴포넌트 (UI Layer)
    ↓
서비스 (Business Logic)
    ↓
API/데이터베이스
    ↓
상태 관리 (Zustand/Context)
    ↓
UI 업데이트
```

## 🎯 구현 우선순위

### Phase 1: Core Foundation (Week 1)
1. ✅ 기본 UI 컴포넌트 확장
2. ✅ 대시보드 레이아웃 구현
3. ✅ 데이터 타입 정의

### Phase 2: Invoice System (Week 2)
1. 인보이스 CRUD 구현
2. 상태 관리 시스템
3. 리마인드 기능

### Phase 3: Tax Export (Week 3)
1. 국세청 양식 변환기
2. 데이터 매핑 로직
3. 내보내기 기능

### Phase 4: Template Engine (Week 4)
1. 템플릿 변수 시스템
2. 미리보기 기능
3. 템플릿 관리

## 🔧 기술 스택

- **Frontend**: Next.js 14, TypeScript, Tailwind CSS
- **State**: Zustand (간단한 상태 관리)
- **UI**: Weave Design System (Teal 브랜드 컬러)
- **Charts**: Recharts (대시보드 차트)
- **Forms**: React Hook Form (폼 관리)
- **Date**: date-fns (날짜 처리)
- **Export**: xlsx, jsPDF (파일 내보내기)

## 📊 대시보드 룰 명세

### R1: 결제 지연 청구서
- 조건: `due_date < today AND status != 'Paid'`
- 표시: 연체 금액, 일수, 고객명
- CTA: 리마인드 보내기

### R2: 마감 임박 프로젝트
- 조건: `due_date BETWEEN today AND today+7`
- 표시: 프로젝트명, D-day, 진행률
- CTA: 프로젝트 상세 보기

### R3: 월간 발행/입금 현황
- 조건: 이번 달 데이터
- 표시: 발행 총액, 입금 총액, 차액
- CTA: 상세 리포트 보기

### R4: 상위 고객 기여도
- 조건: 최근 3개월 데이터
- 표시: Top 3 고객, 매출 비중
- CTA: 고객 상세 보기

## 🚀 다음 단계

1. 기본 UI 컴포넌트 확장 구현
2. 대시보드 컨테이너 및 레이아웃 구축
3. 인보이스 데이터 모델 및 서비스 구현
4. 국세청 양식 변환 로직 개발