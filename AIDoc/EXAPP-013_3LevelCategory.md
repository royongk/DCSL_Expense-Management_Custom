#### 3단계 카테고리 선택 구현
- 마스터 데이터 소스: `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\DCSL Expense Category Mapping Setup Entity %28mserp%29.json`
- 필드 상세 구성:
    - Level 1: Department Type 드롭다운 구현
        - 필드: "mserp_department"
        - 필드명: Department
    - Level 2: Benefit Type 드롭다운 구현
        - 필드: "mserp_benefittype"
        - 필드명: Benefit Type
    - Level 3: Expense Category 드롭다운 구현
        - 필드: "mserp_expensecategory"
        - 필드명: Expense Category

- 기능 구현:
    - 필터링: 
        1. Level 2는 Level 1에서 필터링한 데이터만 조회
        2. Level 3는 Level 1, 2에서 필터링한 데이터만 조회
    - 데이터 저장:
        1. 저장 시 `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\Expense lines %28mserp%29.json`에 저장
        2. 저장 되는 데이터는 **Expense Category** 필드만 "mserp_costtype"에 저장

- UI/UX 구성:
    - 반응형 레이아웃 적용 (모바일/PC)
    - 빈 상태(Empty State) 처리
    - 로딩 스피너 적용
    - 다른 선택 박스 디자인과 동일하게 디자인 구성

- 적용 화면:
  - `Expenses - Edit Screen.fx.yaml`
  - `Itemization - Itemized Expense Edit Screen.fx.yaml`
  - `Expenses - View Only Screen.fx.yaml` (Read-only 모드)