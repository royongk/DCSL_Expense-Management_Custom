# 덜위치 Expense Management Power Apps 프로젝트 진행 체크리스트

**프로젝트명:** 덜위치 Expense Management Power Apps 확장 및 고도화  
**작성일:** 2025-01-XX  
**최종 수정일:** 2025-01-XX

---

## 📋 프로젝트 개요

- **목표:** Microsoft Dynamics 365 Expense Management를 Power Apps 인터페이스로 확장하여, 엄격한 재무 통제를 유지하면서도 직원이 모바일과 PC를 통해 손쉽게 비용을 청구할 수 있도록 함
- **기술 스택:**
  - Front-End: Power Apps (반응형 - 모바일/PC 지원)
  - Back-End: Dynamics 365 Finance & Operations (F&O)
  - 데이터 브리지: Dataverse Virtual Tables (실시간 동기화)

---

## 🎯 주요 화면별 작업 항목

### EXAPP-012: 출장 신청서 (Travel Requisition)

**목표:** 사용자에게 할당된 Travel Requisition 목록 조회 화면 구현

#### 데이터 소스 연동
- [ ] D365 `TrvRequisitionTableView` Virtual Table Dataverse 연결 확인
- [ ] Travel Requisition 데이터 소스 추가 (`DataSources/` 폴더)
- [ ] 데이터 필터링 로직 구현 (사용자별 할당된 Requisition만 조회)

#### 화면 구현
- [ ] Travel Requisition 목록 화면 생성 (`Reports - List Screen` 또는 신규 화면)
- [ ] Gallery 컨트롤 구성 (목록 표시)
- [ ] 표시 필드 구현:
  - [ ] Date (날짜)
  - [ ] Total estimate (총 예상 금액)
  - [ ] Remaining amount (잔여 금액)
  - [ ] Business purpose (출장 목적)
- [ ] 목록 선택 시 Expense Report 생성 화면으로 이동 로직

#### UI/UX
- [ ] 반응형 레이아웃 적용 (모바일/PC)
- [ ] 빈 상태(Empty State) 처리
- [ ] 로딩 스피너 적용

---

### EXAPP-013: 경비 등록 (Expense Report Line)

**목표:** 영수증 첨부 및 구체적인 비용 내역 입력 화면 확장

#### 3단계 카테고리 선택 구현
- [x] Level 1: Department Type 드롭다운 구현
  - [x] Admin / Academic 선택 옵션
  - [x] 데이터 소스 확인 (`DCSL Expense Category Mapping Setup Entity (mserp)`)
- [x] Level 2: Benefit Type 드롭다운 구현
  - [x] Level 1 선택값에 따른 필터링 로직
  - [x] Benefit claim, Billing trip 등 옵션
  - [x] 데이터 소스 확인 (`DCSL Expense Category Mapping Setup Entity (mserp)`)
- [x] Level 3: Expense Category 드롭다운 구현
  - [x] Level 1, 2 선택값에 따른 필터링 로직
  - [x] 기존 `Expense category (mserp)` 데이터 소스 활용
- [x] 적용 화면:
  - [x] `Expenses - Edit Screen.fx.yaml` ✅ 완료
  - [x] `Itemization - Itemized Expense Edit Screen.fx.yaml` ✅ 완료
  - [x] `Expenses - View Only Screen.fx.yaml` ✅ 완료 (Read-only 모드, Department/Benefit Type 표시)

#### Cost Center 필드 추가
- [ ] Cost Center 데이터 소스 확인 (`DCSL Financial Dimension CostCenter (mserp)`)
- [ ] Expense Line에 Cost Center 필드 추가
  - [ ] Cost Center 코드 표시
  - [ ] Cost Center 이름(Display Name) 표시
  - [ ] 두 필드 함께 표기 (예: "CC001 - Marketing Department")
- [ ] Read-only 모드 설정 (D365 동기화, 사용자 수정 불가)
- [ ] 적용 화면:
  - [ ] `Expenses - Edit Screen.fx.yaml`
  - [ ] `Itemization - Itemized Expense Edit Screen.fx.yaml`

#### 기존 필드 유지
- [ ] 경비 범주 (CostType) - 3단계 선택으로 대체되지만 하위 호환성 유지
- [ ] 거래 금액 (AmountCurr)
- [ ] 거래 날짜 (TransDate)
- [ ] 통화 (ExchangeCode)
- [ ] 결제 방법 (PayMethod)
- [ ] Merchant (MerchantId)

---

### EXAPP-014: 출장 보고서 등록 (Expense Report Header)

**목표:** 지출 목적, 장소 등 리포트 기본 정보 입력 화면 확장

#### Travel Requisition 연동 필드
- [ ] Map to travel requisition 필드 추가
  - [ ] Lookup 드롭다운 (Travel Requisition 목록에서 선택)
  - [ ] EXAPP-012 화면과 연동
- [ ] Travel requisition amount 필드 추가
  - [ ] Read-only 모드
  - [ ] 선택한 Travel Requisition의 총 예상 금액 표시
- [ ] Remaining amount 필드 추가
  - [ ] Read-only 모드
  - [ ] 선택한 Travel Requisition의 잔여 금액 표시

#### 기존 필드 유지
- [ ] 리포트 번호 (ExpNumber) - 자동 생성
- [ ] 목적 (Purpose) - Lookup 선택 박스
- [ ] 위치 (Location) - Lookup 선택 박스
- [ ] Destination (Home Country) - Read-only

#### 상태 관리 로직
- [ ] 저장 로직:
  - [ ] Document Status = 초안(Draft)
  - [ ] Approval Status = 초안(Draft)
- [ ] 제출 로직:
  - [ ] Document Status = 제출(Submit)
  - [ ] Approval Status = 초안(Draft)
  - [ ] 수정 잠금(Lock) 처리

#### 적용 화면
- [ ] `Reports - Edit Screen.fx.yaml` 수정

---

### EXAPP-015: 보고서 목록 (Expense Report Header)

**목표:** 사용자가 작성한 지출 결의서 목록 조회 화면 개선

#### 상태 값 표시 (Badge)
- [ ] Document Status 배지 구현
  - [ ] Draft (초안) - 배지 스타일 정의
  - [ ] Submitted (제출됨) - 배지 스타일 정의
  - [ ] Approved (승인됨) - 배지 스타일 정의
  - [ ] Rejected (거부됨) - 배지 스타일 정의
- [ ] Gallery 아이템에 배지 표시
- [ ] 색상 및 아이콘 적용

#### 수정 권한 제어
- [ ] Submitted 상태 감지 로직
- [ ] Read-only 모드 제어:
  - [ ] `Reports - View Only Screen`에서 Submitted 상태 확인
  - [ ] 모든 편집 필드 Read-only 적용
  - [ ] 저장/제출 버튼 비활성화

#### 대리 문서 조회
- [ ] 대리인(Delegate) 기능 확인
- [ ] F&O "Expenses delegated to me" 화면 데이터 연동
- [ ] 위임자(Delegator)의 지출 결의서 목록 조회 로직

#### 기존 기능 유지
- [ ] 각 리포트의 결재 상태(Status) 확인
- [ ] (+) 버튼을 통한 신규 지출 결의서 생성
- [ ] 상태별 필터링 (Draft, Submitted, Approved, Rejected)

#### 적용 화면
- [ ] `Reports - List Screen.fx.yaml` 수정
- [ ] `Reports - View Only Screen.fx.yaml` 수정

---

## 🔧 기능별 구현 사항

### 데이터 매핑 및 연동

#### Expense Report Header ↔ D365 TrvExpTable
- [ ] 리포트 번호 (ExpNumber) 매핑 확인
- [ ] 목적 (Purpose) 매핑 확인
- [ ] 위치 (Location) 매핑 확인
- [ ] Destination (Home Country) 매핑 확인
- [ ] Map to travel requisition 매핑 구현
- [ ] Travel requisition amount 매핑 구현
- [ ] Remaining amount 매핑 구현
- [ ] Document Status 매핑 확인
- [ ] Approval Status 매핑 확인

#### Expense Report Line ↔ D365 TrvExpTrans
- [ ] 경비 범주 (CostType) 매핑 확인
- [ ] 거래 금액 (AmountCurr) 매핑 확인
- [ ] 거래 날짜 (TransDate) 매핑 확인
- [ ] 통화 (ExchangeCode) 매핑 확인
- [ ] 결제 방법 (PayMethod) 매핑 확인
- [ ] Merchant (MerchantId) 매핑 확인
- [ ] Department (Level 1) 매핑 구현
- [ ] Benefit Type (Level 2) 매핑 구현
- [ ] Expense Category (Level 3) 매핑 확인
- [ ] Cost Center 매핑 구현
- [ ] Cost Center Name 매핑 구현

#### Travel Requisition ↔ D365 TrvRequisitionTableView
- [ ] Date 매핑 확인
- [ ] Total estimate 매핑 확인
- [ ] Remaining amount 매핑 확인
- [ ] Business purpose 매핑 확인

### 프로세스 흐름 구현

#### 1. 작성 (Draft) - Power Apps
- [ ] 리포트 생성 로직
- [ ] 영수증 첨부 기능
- [ ] 임시 저장 기능
- [ ] Document Status = Draft 설정
- [ ] Approval Status = Draft 설정

#### 2. 제출 (Submit) - Power Apps
- [ ] 승인 요청 로직
- [ ] 수정 잠금(Lock) 처리
- [ ] Document Status = Submit 설정
- [ ] Approval Status = Draft 유지

#### 3. 검토 (Review) - D365 F&O
- [ ] 데이터 검증 (F&O 표준 기능)
- [ ] 수정/분할(Split) 기능 (F&O 표준 기능)
- [ ] 1차 승인 (F&O 표준 기능)

#### 4. 전기 (Post) - D365 F&O
- [ ] 표준 워크플로우 (F&O 표준 기능)
- [ ] GL 전기 (F&O 표준 기능)

---

## 🧪 테스트 및 검증

### 단위 테스트
- [ ] 3단계 카테고리 선택 필터링 로직 테스트
- [ ] Cost Center 필드 표시 테스트
- [ ] Travel Requisition 연동 테스트
- [ ] Document Status 변경 로직 테스트
- [ ] Read-only 모드 제어 테스트

### 통합 테스트
- [ ] Power Apps ↔ Dataverse Virtual Tables 연동 테스트
- [ ] Dataverse ↔ D365 F&O 데이터 동기화 테스트
- [ ] Travel Requisition 선택 시 금액 자동 계산 테스트
- [ ] 제출 후 수정 잠금 테스트

### 사용자 시나리오 테스트
- [ ] 일반 직원 경비 입력 시나리오
- [ ] Travel Requisition 연동 시나리오
- [ ] 리포트 제출 시나리오
- [ ] Submitted 상태 Read-only 모드 시나리오
- [ ] 대리 문서 조회 시나리오

### 성능 테스트
- [ ] 대량 데이터 로딩 성능
- [ ] 필터링 성능
- [ ] 데이터 동기화 속도

---

## 📝 개발 워크플로우

### 소스 코드 관리
- [ ] `ExpenseApp_Src/Src/*.fx.yaml` 파일 수정 (Power Fx 공식 형식)
- [ ] `ExpenseApp_Src/Other/Src/*.pa.yaml` 파일 동기화 (Power Apps Studio 호환)
- [ ] `ExpenseApp_Src/DataSources/*.json` 파일 업데이트

### Pack 및 배포
- [ ] Power Apps CLI (pac)를 사용한 Pack 작업
- [ ] `.msapp` 파일 생성
- [ ] Power Apps Studio에서 업로드 및 테스트
- [ ] 최종 검증

### 버전 관리
- [ ] Git 커밋 (변경 사항별)
- [ ] 변경 사항 문서화

---

## ⚠️ 확인 필요 사항

### 데이터 구조 확인
- [ ] D365에 Department Type 테이블 존재 여부 확인
- [ ] D365에 Benefit Type 테이블 존재 여부 확인
- [ ] Expense Category와의 관계 매핑 확인
- [ ] Cost Center 필드가 Expense Line에 존재하는지 확인
- [ ] Travel Requisition Virtual Table 연결 상태 확인

### 권한 및 보안
- [ ] Team Member 라이선스 권한 확인
- [ ] Full User 라이선스 권한 확인
- [ ] Dataverse Virtual Tables 접근 권한 확인

### 요구사항 문서 확인
- [ ] `Doc/DCSL_Expense Mnagement Mobile App_Power Apps Requirement_KOR_251223.pdf` 재검토
- [ ] 데이터 매핑 정의 최종 확인
- [ ] 화면별 상세 요구사항 확인

---

## 📊 진행 상태 요약

### 전체 진행률
- **계획 단계:** ✅ 완료
- **설계 단계:** 🔄 진행 중
- **개발 단계:** ⏳ 대기 중
- **테스트 단계:** ⏳ 대기 중
- **배포 단계:** ⏳ 대기 중

### 우선순위별 진행 상황

#### 우선순위 1: 핵심 기능 구현
- [ ] 3단계 카테고리 선택 로직
- [ ] Cost Center 필드 추가

#### 우선순위 2: Travel Requisition 연동
- [ ] Travel Requisition 목록 화면
- [ ] Expense Report Header에 Travel Requisition 필드 추가

#### 우선순위 3: UI/UX 개선
- [ ] Document Status 배지 표시
- [ ] Submitted 상태 Read-only 제어

---

## 📌 참고 사항

### 핵심 설계 문서
- **요구사항 문서:** `Doc/DCSL_Expense Mnagement Mobile App_Power Apps Requirement_KOR_251223.pdf`
- **프로젝트 규칙:** `.cursor/rules/dcsl-expensemanagement.mdc`

### 개발 원칙
- Power Apps는 F&O의 승인 프로세스에 영향을 주지 않으며, 초안(Draft) 데이터 생성만 담당
- D365 F&O는 마스터 데이터 소스 및 최종 전기 목적지
- Dataverse는 중복 없는 실시간 데이터 흐름을 위한 브리지 테이블 역할

### 코딩 스타일
- 코드 내의 주석, 변수명, 함수명은 가급적 **영어**로 작성
- `Src/*.fx.yaml` 파일을 우선적으로 편집 (Power Fx 공식 형식)
- YAML 파일 편집 시 들여쓰기 및 문법 주의 (스페이스 2칸 또는 4칸 일관성 유지)

---

## 📝 변경 이력

| 날짜 | 변경 내용 | 작성자 |
|------|----------|--------|
| 2025-01-XX | 초기 체크리스트 작성 | - |

---

**마지막 업데이트:** 2025-01-XX

