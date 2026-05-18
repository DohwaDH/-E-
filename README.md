```mermaid
graph TB
    %% Actor Definition
    Actor((플레이어 / Actor))

    %% System Boundary
    subgraph 게임 시스템 (System)
        %% 메인 유스케이스
        U_Name["이름 입력"]
        U_Start["게임 시작"]
        U_Skin["스킨 관리"]
        U_Title["칭호 관리"]
        U_Backup["클라우드 백업"]
        U_Load["클라우드 불러오기"]
        U_Score["최고점수 보기"]
        U_Dev["개발자 / 도움말"]
        U_Exit["게임 종료"]

        %% 인게임 관련 하위 유스케이스
        U_Battle["전투"]
        U_Explore["탐색"]
        U_Skill["스킬"]
        U_Potion["포션"]
        U_Success["성공"]
        U_Fail["실패"]

        %% 스킨 관련 상세 유스케이스
        U_SkinApply["스킨 적용"]
        U_SkinExpand["스킨 상점 확장"]
        U_SkinAdd["스킨 추가"]
        U_SkinInput["스킨 이름/이미지 URL 입력"]
        U_SkinSave["스킨 저장"]

        %% 칭호 관련 상세 유스케이스
        U_TitleEquip["칭호 장착"]
        U_TitleUnequip["칭호 해제"]

        %% 점수 및 정보 관련 상세 유스케이스
        U_Leaderboard["순위표"]
        U_AppInfo["앱 정보 / 버전 정보"]
    end

    %% External Systems
    subgraph 구글 서비스 (External System)
        Sys_Google["구글 로그인"]
        Sys_Data["데이터 저장"]
    end

    %% Actor -> Main Use Cases 관계
    Actor --> U_Name
    Actor --> U_Start
    Actor --> U_Skin
    Actor --> U_Title
    Actor --> U_Backup
    Actor --> U_Load
    Actor --> U_Score
    Actor --> U_Dev
    Actor --> U_Exit

    %% 게임 시작 및 인게임 흐름
    U_Start --> U_Battle
    U_Start --> U_Explore
    U_Battle --> U_Skill
    U_Battle --> U_Potion
    U_Explore --> U_Success
    U_Explore --> U_Fail

    %% 스킨 상세 관계
    U_Skin --> U_SkinExpand
    U_Skin --> U_SkinApply
    U_Skin --> U_SkinAdd
    U_SkinAdd --> U_SkinInput
    U_SkinInput --> U_SkinSave
    U_SkinApply -.->|"<<include>>"| U_SkinAdd

    %% 칭호 상세 관계
    U_Skin --> U_TitleEquip
    U_Title --> U_TitleUnequip
    U_TitleUnequip -.->|"<<include>>"| U_TitleEquip

    %% 시스템 정보 및 스코어 상세 관계
    U_Score --> U_Leaderboard
    U_Dev --> U_AppInfo

    %% 클라우드 시스템 연동 관계
    U_Backup --> Sys_Google
    Sys_Google --> Sys_Data
    Sys_Data --> U_Load
    ```
