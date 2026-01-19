
#### Cost Center 필드 추가 요구 사항 상세 정의
- 수정 대상 화면:
  - `Expenses - Edit Screen.fx.yaml`
  - `Itemization - Itemized Expense Edit Screen.fx.yaml`
  - `Expenses - View Only Screen.fx.yaml` (Read-only 모드)

- 데이터 구성
    - 마스터 데이터 소스: `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\DCSL Financial Dimension CostCenter %28mserp%29.json`
    - 필드 구성:
        - 마스터 데이터 소스의 `"mserp_description": "Name"`의 목록을 표시해야함.
        - 필드 구성 위치: `"'Expense category_DataCard3_3'` 다음 위치로 표시

- 기능 로직:
    - 데이터 저장:
        1. 저장 대상 테이블:
            - `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\Expense lines %28mserp%29.json`에 저장
        2. 저장 대상 필드:
            - 저장 대상 테이블의 `"mserp_deexcostcenter": "CostCenter"`에 저장 해야함.


- UI/UX 구성:
    - 반응형 레이아웃 적용 (모바일/PC)
    - 다른 선택 박스 디자인과 동일하게 데이터 카드 형태로 디자인 구성 
    (예시: `C:\PJT\Dulwich\ExpenseApp_Src\Src\Expenses - Edit Screen.fx.yaml` 화면의 `Department_DataCard` 데이터 카드 구성 참고)