
#### Cash Advance Edit 화면 신규 추가 요구 사항 정의
- 개요:
    - 화면 구현 목적: Cash Advance Edit 화면을 추가하고, Cash Advance - List Screen에서 사용자가 플러스 아이콘(+) 버튼을 클릭하면 데이터 새로 생성하고, Draft 상태의 문서를 클릭하면 데이터를 수정할 수 있도록 하는 목적

- 데이터 구성:
    - 데이터 소스: `Cash advances (mserp)` (C:\PJT\Dulwich\ExpenseApp_Src\DataSources\Cash advances %28mserp%29.json)
    - 표시 및 저장 대상 필드: 
        1. "Requested date" : 필수
        2. "Location" : 필수
            - Items: Filter('Travel locations (mserp)','Company Code' = varSelectedLegalEntity)
                > 데이터 구성은 `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - Edit Screen.fx.yaml`의 `LocationContainer_1` 참고
        3. "Purpose"
            - Items: Filter('DimAttributeTrvTravelTxtEntity (mserp)', 'Company Code' = varSelectedLegalEntity)
                > 데이터 구성은 `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - Edit Screen.fx.yaml`의 `PurposeContainer_1` 참고 
        4. "Requested amount" : 필수
        6. "Currency" : 필수
            - Items: ShowColumns(
                            'Currencies (mserp)',
                            'Currency code',Name
                        )
                > 데이터 구성은 `C:\PJT\Dulwich\ExpenseApp_Src\Src\Expenses - Edit Screen.fx.yaml`의 `Currency_DataCard1_3` 참고
        7. "Note" : 선택
            - 여러줄 입력 가능하도록 설정

- 화면 구성:
    - 메인 입력 화면: Editform 형식의 입력/수정 화면
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Expenses - Edit Screen.fx.yaml` 화면 구성 참고
    - 하단 버튼 구성:
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Expenses - Edit Screen.fx.yaml`의 `"'Buttons - Draft' As groupContainer.manualLayoutContainer"` 참고
        - "Save Draft" 버튼 추가
            1. SubmitForm 함수로 저장
            2. 신규로 입력한 데이터면 신규 생성
            3. 이미 입력된 데이터면 수정
            4. 오류 없이 데이터 저장 완료되면 `Cash Advance - List Screen`으로 이동
        - "Submit" 버튼 추가
            1. SubmitForm 함수로 저장
            2. 신규로 입력한 데이터면 신규 생성
            3. 이미 입력된 데이터면 수정
            4. 오류 없이 데이터 저장 완료되면 `Cash Advance - List Screen`으로 이동
            5. `Cash advances (mserp)` 데이터소스에 "WorkFlowAction"이라는 필드 추가 예정, 아직 로직 미구현 (D365의 Workflow 기능을 사용할 수 있는 필드)          

    - 화면 이동 로직:
        1. 신규 생성: `Cash Advance - List Screen` 화면에서 `scrCashAdvance_img_Create` 버튼을 클릭하면 `Cash Advance - Edit Screen` 신규 생성 모드로 이동
        2. 수정: `Cash Advance - List Screen` 화면에서 `scrCashAdvance_Gallery` 갤러리 데이터 목록 중 `Cash advance status`가 "Draft" 상태이면 수정 모드로 이동 (그 외 상태는 `Cash Advance - View Only Screen`으로 이동하게 하려고함. 아직 생성 안함.)


- UI 디자인:
    - 반응형 레이아웃 적용 (모바일/PC)
    - 다른 화면들에서 사용된 구성 요소들을 참고해서 최대한 일관성 있게 구현
    - 참고 화면들: 
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Expenses - Edit Screen.fx.yaml`
        > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Reports - Edit Screen.fx.yaml`