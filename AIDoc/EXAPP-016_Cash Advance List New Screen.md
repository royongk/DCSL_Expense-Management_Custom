
#### Cash Advance List 화면 신규 추가 요구 사항 정의
- 개요:
    - 화면 구현 목적: Cash Advance List 화면을 추가하고, Main Screen에서 Cash Advance 버튼을 사용자 클릭해서 들어왔을때, Footer에 표시되는 Approvals을 Travel로 표시하여 사용자에게 Travel requisition 데이터 목록을 표시하도록 하는 목적

- 데이터 구성:
    - 데이터 소스: `Cash advances (mserp)` (C:\PJT\Dulwich\ExpenseApp_Src\DataSources\Cash advances %28mserp%29.json)
    - 표시 필드: 
        1. "Cash advance number"
        2. "Requested amount"
        3. "Requested date"
    - 필터링:
        1. 상태 별 필터링:
            - 화면 상단에 상태 별 필터링 드롭 다운 추가 (데이터 소스 상태 값이 많으니, 사용자가 필터링 드롭 다운으로 선택할 수 있도록 구성)
            - 필터링 데이터 소스 필드: "Cash advance status"
                > 유형: Draft, Submitted, In review, Approved, Returned, Ordered, Ready to pay, Paid
        2. 날짜 별 필터링:
            - 화면 상단에 날짜 별 필터링 추가
                > 참고 화면: `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - List Screen.fx.yaml` 화면의 `scr16_txt_SearchBox` 구성 요소 참고
            - 필터링 데이터 소스 필드: "Requested date"

- 화면 구성:
    - 목록 데이터 갤러리 형식으로 화면 구성
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - List Screen.fx.yaml` 화면 구성 참고
        > `Reports - List Screen`의 다중 선택 버튼, 삭제 버튼 모두 동일하게 구성. (삭제는 Draft 상태일때만 가능)
    - 화면 표시 및 이동: `C:\PJT\Dulwich\ExpenseApp_Src\Src\Main Screen.fx.yaml`에서 `Cash Advance` 버튼을 클릭할 경우 모든 Footer의 `Approvals`를 `Cash`로 변경되고 클릭하면 이 화면으로 이동되도록 모든 Footer에 연결
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Components\cmp_Footer_3.fx.yaml`의 동작 방식 확인 필요

- 기능 로직:
    1. 조회된 데이터 목록에서 1개 씩 데이터를 사용자가 클릭할 경우: 
        - 해당 데이터의 "Cash advance status" 데이터가 "Draft"이면: `Cash Advance Edit Screen`으로 이동(아직 미구현 상태)
        - 해당 데이터의 "Cash advance status" 데이터가 "Draft"가 아니면: `Cash Advance View Only Screen`으로 이동(아직 미구현 상태)
        - 이 동작 방식은 `Reports - List Screen`과 동일한 형태로 구현 필요
    2. 플러스(+) 아이콘 추가 및 클릭 시:
        - 해당 아이콘을 사용자가 클릭하면: `Cash Advance Edit Screen`으로 이동(아직 미구현 상태)
        - 이 동작 방식은 `Reports - List Screen`과 동일한 형태로 구현 필요
            > 참고 구성요소: `Reports - List Screen`화면의 `scr16_img_CreateReport` 구성 요소

- UI 디자인:
    - 반응형 레이아웃 적용 (모바일/PC)
    - 다른 화면들에서 사용된 구성 요소들을 참고해서 최대한 일관성 있게 구현
    - 참고 화면 구성: 
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - List Screen.fx.yaml` 화면 구성 참고
        > `Reports - List Screen`의 다중 선택 버튼, 삭제 버튼 모두 동일하게 구성. (삭제는 Draft 상태일때만 가능)