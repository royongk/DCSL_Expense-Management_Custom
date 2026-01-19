
#### Main Screen 신규 추가 요구 사항 정의
- 개요:
    - 화면 구현 목적: 신규 메인 화면을 추가하여 일반 경비(expenses reports)와 여행 경비(Travel Requisition) 등록 화면을 사용자에게 구분하여 이동 되도록 보이게 하는 목적
    - `C:\PJT\Dulwich\ExpenseApp_Src\Src\App.fx.yaml` App이 시작하면 최초로 실행 되어야할 화면
        > 현재는 `C:\PJT\Dulwich\ExpenseApp_Src\Src\Expenses - List Screen.fx.yaml` 화면이기 때문에 시작 시 연동되는 로직을 판단해서 기존 로직 및 구조에 영향이 발생하지 않도록 수정해야하는데 중요.
    - 화면 디자인 예시: `C:\PJT\Dulwich\AIDoc\EXAPP-001_Main Screen Sample Mockup.png`

- 화면 구성 및 기능 상세:
    - 화면 중앙 상단: `C:\PJT\Dulwich\ExpenseApp_Src\Assets\Images\DCSL_Logo.png` 로고 이미지를 표시
        > 다른 화면 fx 수식들에서 이미지 표현 방법을 참고하여 Power Apps 웹 편집기에서 오류 발생하지 않도록 구현
    - 화면 중앙: `Expense Management`라는 텍스트와 `Welcome,`[User.Name] 텍스트를 표시
        > User.Name은 접속 하는 사용자의 이름을 표시하도록 Power Fx 함수 활용
    - 화면 중앙 하단: 버튼 2개 추가하여 각 버튼 별 화면 이동 시 모든 목록 화면 아래 Footer 구성을 다르게 표시
        1. 버튼 1:
            - 텍스트: `Expense Report`
            - 버튼 클릭 시 이동 화면: `C:\PJT\Dulwich\ExpenseApp_Src\Src\Expenses - List Screen.fx.yaml` 화면으로 이동
            - 버튼 클릭 시 기능: 모든 목록 화면의 하단 Footer를 기존과 동일한 Footer(`cmp_Footer_3`)에 동일한 텍스트와 기능 유지
                > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Components\cmp_Footer_3.fx.yaml`의 동작 방식 확인 필요
        2. 버튼 2:
            - 텍스트: `Airfare Allowance`
            - 버튼 클릭 시 이동 화면: `C:\PJT\Dulwich\ExpenseApp_Src\Src\Expenses - List Screen.fx.yaml` 화면으로 이동
            - 버튼 클릭 시 기능: 모든 목록 화면의 하단 Footer의 Approval을 `Travel` 목록을 표시하는 화면으로 연결되도록 구성
                > `C:\PJT\Dulwich\ExpenseApp_Src\Src\Components\cmp_Footer_3.fx.yaml`의 동작 방식 확인 필요
                > Footer 상세 구성
                    > 텍스트: Travel
                    > 아이콘 이미지:
                        > 미선택: `C:\PJT\Dulwich\ExpenseApp_Src\Assets\Images\travelDeselectedIcon.png`
                        > 선택: `C:\PJT\Dulwich\ExpenseApp_Src\Assets\Images\travelSelected.png`
                    > 연결 화면: Travel - List Screen (아직 미구현. 화면 구현 되면 연결할 예정)

- UI 디자인:
    - 반응형 레이아웃 적용 (모바일/PC)
    - 다른 화면들에서 사용된 구성 요소들을 참고해서 최대한 일관성 있게 구현