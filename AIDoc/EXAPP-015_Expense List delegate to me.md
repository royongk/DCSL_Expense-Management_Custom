
#### Expense List 화면 대리인 문서 조회 버튼 기능 추가
- 개요:
    - 화면 구현 목적: Expense List 화면의 상단에 대리인 문서 조회 버튼을 추가해서, 기본 갤러리 목록은 자신에게 할당된 데이터 목록만 조회하고 버튼 클릭 시 대리인 문서를 불러오도록 하는 기능

- 변경 대상 화면: `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - List Screen.fx.yaml`

- 버튼 추가:
    - 버튼 텍스트: `Delegate`
    - 버튼 위치: `scr16_btn_FakeButton` 버튼 왼쪽
    - 버튼 활성화: `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\%40DEEX%3aDEEX_20316 %28mserp%29.json` 데이터 소스 목록들 중 `DelegatedUserInfoRecId`필드 데이터가 `userRecord.CreatingWorker`와 동일한 데이터가 1개라도 있을 경우 버튼 활성화
    - 버튼 기능:   
        - 버튼 클릭 해제 하거나, 기본 조회 로직:
            - `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\Expense reports %28mserp%29_1.json` 데이터 소스 테이블의 ""Employee (mserp_creatingworker)" 필드 데이터가 `userRecord.CreatingWorker`와 동일한 데이터만 조회(본인 문서만 조회)
        - 버튼 클릭 시 조회 로직:
            -  `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\%40DEEX%3aDEEX_20316 %28mserp%29.json` 데이터 소스 목록들 중 `DelegatedUserInfoRecId`필드 데이터가 `userRecord.CreatingWorker`와 동일하면서, 오늘 날짜가 `Start date`필드 데이터와 `End date`사이일 경우 `C:\PJT\Dulwich\ExpenseApp_Src\DataSources\Expense reports %28mserp%29_1.json` 데이터 소스 테이블의 ""Employee (mserp_creatingworker)" 필드 데이터가 `Employee`와 동일한 데이터만 조회(대리인 문서만 조회)

- UI 디자인:
    - 반응형 레이아웃 적용 (모바일/PC)
    - 다른 화면들에서 사용된 구성 요소들을 참고해서 최대한 일관성 있게 구현
    - 갤러리 표시 필드는 이미 구현된 그대로 사용