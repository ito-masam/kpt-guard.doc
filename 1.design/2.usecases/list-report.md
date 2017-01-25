@startuml

    ' ----------- meta
    title レポートリストを出力する

    skinparam usecase {
      FontColor<<error>> white
      FontName<<error>> Verdana
      BackgroundColor<<error>> gray
      BorderColor<<error>> black
    }

    actor User

    ' ----------- main
    User --- ( listする )
    ( listする ) ..> ( チャンネルを指定した\nレポート一覧を返す ) : << precedes >>
    ( チャンネルを指定した\nレポート一覧を返す ) ..> ( 有効な\nレポートを集める ) : << invokes >>

    note right of ( listする )
      @reply list
    end note

    ' ----------- alternative
    ( 400 Bad Request を返す ) <<error>>
    ( listする ) ..> ( 400 Bad Request を返す ) : listの構文\nに適合しない

    ( 404 Not Found を返す ) <<error>>
    ( 有効な\nレポートを集める ) ..> ( 404 Not Found を返す ) : 有効なレポートが存在しない

@enduml
