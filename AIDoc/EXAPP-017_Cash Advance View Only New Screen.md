
#### Cash Advance View Only 화면 신규 추가 요구 사항 정의
- 개요:
    - 화면 구현 목적: Cash Advance View Only 화면을 추가하고, Cash Advance - List Screen에서 사용자가 Draft 상태가 아닌 그 외 상태 값의 문서를 클릭하면 데이터를 볼 수 있도록 하는 목적

- 데이터 구성:
    - 데이터 소스: `Cash advances (mserp)` (C:\PJT\Dulwich\ExpenseApp_Src\DataSources\Cash advances %28mserp%29.json)
    - 표시 및 저장 대상 필드: `Cash Adavance - List Screen` 화면에서 선택한 Record의 데이터
        1. "Requested date"
        2. "Location"
        3. "Purpose"
        4. "Requested amount"
        6. "Currency"
        7. "Note"

- 화면 구성:
    - 각 필드 표시 모드: View Only
    - 하단 버튼 구성:
        - `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - View Only Screen.fx.yaml`의 `"'Buttons - In Review' As groupContainer.manualLayoutContainer"` 참고
        - "Done" 버튼 추가
            1. `Cash Advance - List Screen`으로 이동합니다.

        - "Withdraw" 버튼 추가
            1. `Cash advances (mserp)` 데이터 소스의 `DEEXWorkflowAction`필드를 "Recall"로 업데이트
            2. 동작에 오류가 없으면, `Cash Advance - List Screen`으로 이동합니다.

    - 화면 이동 로직:
        1. `Cash Advance - List Screen` 화면에서 `scrCashAdvance_Gallery` 갤러리 데이터 목록 중 `Cash advance status`가 "Draft" 상태가 아닌 다른 상태이면 이 화면으로 이동

- UI 디자인:
    - *중요!* 모든 구성 요소들은 반응형 레이아웃 적용 (모바일/PC)
    - 다른 화면들에서 사용된 구성 요소들을 참고해서 최대한 일관성 있게 구현
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - View Only Screen.fx.yaml`