@startuml

    ' ----------- meta
    title レポートリストを出力する

    skinparam usecase {
      BackgroundColor<<error>> gray
      BorderColor<<error>> black
    }

    actor User

    ' ----------- main
    User --- ( listする )
    ( listする ) ..> ( レポート一覧を返す ) : << precedes >>
    ( レポート一覧を返す ) ..> ( 有効な\nレポートを集める ) : << invokes >>

    note right of ( listする )
      @reply list
    end note

    ' ----------- alternative
    ( 404 Not Found を返す ) <<error>>
    ( listする ) ..> ( 404 Not Found を返す ) : 有効なレポートが存在しない

@enduml
