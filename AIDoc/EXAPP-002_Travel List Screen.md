
#### Travel List Screen 신규 추가 요구 사항 정의
- 개요:
    - 화면 구현 목적: Main Screen에서 Airfare Allowance 버튼을 사용자 클릭해서 들어왔을때, Footer에 표시되는 Approvals을 Travel로 표시하여 사용자에게 Travel requisition 데이터 목록을 표시하도록 하는 목적

- 데이터 구성:
    - 데이터 소스: `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\Travel requisition %28mserp%29.json`
    - 표시 필드: 
        1. "Travel requisition number"
        2. "Amount"
        3. "Amount to reconcile"
        4. "Business purpose"
    - 필터링:
        - "Approval status" 필드 데이터가 "Approved"인 데이터 목록

- 화면 구성:
    - 목록 데이터 갤러리 형식으로 화면 구성
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - List Screen.fx.yaml` 화면 구성 참고
        > `Reports - List Screen`의 필터 버튼, 다중 선택 버튼, 삭제 버튼은 Travel List 화면에서는 사용하지 않음.
    - 화면 표시 및 이동: `C:\PJT\Dulwich\ExpenseApp_Src\Src\Main Screen.fx.yaml`에서 `Airfare Allowance` 버튼을 클릭할 경우 모든 Footer의 `Approvals`를 `Travel`으로 변경되고 클릭하면 이 화면으로 이동되도록 모든 Footer에 연결
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Components\cmp_Footer_3.fx.yaml`의 동작 방식 확인 필요

- 기능 로직:
    - 조회된 데이터 목록에서 1개 씩 데이터를 사용자가 클릭할 경우: 
        - 해당 데이터의 `Amount to reconcile` 데이터가 0이면: "This Travel requirement number cannot register an Expense Report because the Remaining Amount is 0 KRW." 라는 오류 메세지 표시
        - 해당 데이터의 `Amount to reconcile` 데이터가 0이 아니면: 선택한 Record를 변수로 저장하고, `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - Edit Screen.fx.yaml` 화면으로 이동

- UI 디자인:
    - 반응형 레이아웃 적용 (모바일/PC)
    - 다른 화면들에서 사용된 구성 요소들을 참고해서 최대한 일관성 있게 구현
    - 참고 화면 구성: 
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - List Screen.fx.yaml` 화면 구성 참고
        > `Reports - List Screen`의 필터 버튼, 다중 선택 버튼, 삭제 버튼은 Travel List 화면에서는 사용하지 않음.