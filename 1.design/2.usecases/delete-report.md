@startuml

    ' ----------- meta
    title レポートを削除する

    skinparam usecase {
      FontColor<<error>> white
      FontName<<error>> Verdana
      BackgroundColor<<error>> gray
      BorderColor<<error>> black
    }

    actor User

    ' ----------- main
    User -- ( <レポートID>をdeleteする )
    ( <レポートID>をdeleteする ) ..> ( <レポートID>に紐付く\nレポートを探す ) : << precedes >>
    ( <レポートID>に紐付く\nレポートを探す ) ..> ( 該当レポートを\n論理削除する ) : << precedes >>

    note right of ( <レポートID>をdeleteする )
      @reply delete #0104503
    end note

    ' ----------- alternative
    ( 400 Bad Request を返す ) <<error>>
    ( <レポートID>をdeleteする ) ..> ( 400 Bad Request を返す ) : deleteの構文\nに適合しない

    ( 404 Not Found を返す ) <<error>>
    ( <レポートID>に紐付く\nレポートを探す ) ..> ( 404 Not Found を返す ) : <レポートID>に紐付く\nレポートが存在しない

@enduml
