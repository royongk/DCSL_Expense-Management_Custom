#### Document Status 조회 버튼 로직 변경
- 변경 대상 화면: `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - List Screen.fx.yaml`

- 데이터 소스 구성:
    1. 연결된 데이터 소스 변경: 
        - 현재: `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\Expense reports %28mserp%29.json`
        - 변경: `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\Expense reports %28mserp%29_1.json`
    2. 필드 구성:
        - 데이터 소스 변경으로 인해, 화면에서 표시되는 모든 연결된 필드 및 로직들에 변경한 데이터 소스에 맞춰서 변경
    (화면 소스 코드 내에 사용 되는 필드 명칭들을 기반으로 현재 데이터 소스와 변경 데이터 소스 필드 명칭들을 반드시 비교할 것.)
        - 변경: 
            - Document Status는 `"mserp_deexdocumentstatus": "Document Status"`로 변경

- 필터링 로직:
    1. Document Status는 총 4개(Draft, Submitted, Approved, Rejected) 단계 상태로 해당 버튼을 클릭할 경우 갤러리 목록에 조회 값이 변경되어야함.
        (상태 값 필터링 로직은 현재 소스 코드를 반드시 참고하고, 제거 필요한 항목이 있는지 확인할 것.)

- UI/UX
    - 모든 구성요소는 반응형(PC 및 모바일)에 동작 가능하도록 구성 되어야함.
    - Document Status 필터링 버튼: `scr16_btn_Draft`, `scr16_btn_Inreview`, `scr16_btn_Approve` 버튼을 그대로 사용하되, Rejected를 위한 버튼 신규 추가
    - 디자인은 통일성 유지를 위해 기존 그대로 활용.