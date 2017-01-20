@startuml

    ' ----------- meta
    title レポートを登録する

    skinparam usecase {
      FontColor<<error>> white
      FontName<<error>> Verdana
      BackgroundColor<<error>> gray
      BorderColor<<error>> black
    }

    actor User

    ' ----------- main
    User --- ( <レポート>をpostする )
    ( <レポート>をpostする ) ..> ( userとcontentに\n分解する ) : << precedes >>
    ( userとcontentに\n分解する ) ..> ( 改善状態を\nproblem固定とする ) : << precedes >>
    ( 改善状態を\nproblem固定とする ) ..> ( 保存する ) : << precedes >>

    note right of ( <レポート>をpostする )
      @reply post Aプロジェクトでパスワードの長さが英数４桁だった。
    end note

    ' ----------- alternative
    ( 400 Bad Request を返す ) <<error>>
    ( <レポート>をpostする ) ..> ( 400 Bad Request を返す ) : post_newの構文\nに適合しない

    ( 403 Forbidden を返す ) <<error>>
    ( <レポート>をpostする ) ..> ( 403 Forbidden を返す ) : Userとbotが\n同じchannelに\n属していない

@enduml
