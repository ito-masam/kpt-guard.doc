@startuml

    title レポートを登録する

    skinparam usecase {
      BackgroundColor<<error>> gray
      BorderColor<<error>> black
    }

    actor User
    User --- ( <レポート>をpostする )
    ( <レポート>をpostする ) ..> ( userとcontentに\n分解する ) : << precedes >>
    ( userとcontentに\n分解する ) ..> ( 改善状態を\nproblem固定とする ) : << precedes >>
    ( 改善状態を\nproblem固定とする ) ..> ( 保存する ) : << precedes >>

    ' alternative

    ( 403 Forbidden を返す ) <<error>>
    ( <レポート>をpostする ) ..> ( 403 Forbidden を返す ) : Userとbotが同じchannelに属していない

    note right of ( <レポート>をpostする )
      @reply post Aプロジェクトでパスワードの長さが英数４桁だった。
    end note

@enduml
