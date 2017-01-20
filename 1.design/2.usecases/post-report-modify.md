@startuml

    ' ----------- meta
    title レポートを修正する

    skinparam usecase {
      FontColor<<error>> white
      FontName<<error>> Verdana
      BackgroundColor<<error>> gray
      BorderColor<<error>> black
    }

    actor User

    ' ----------- main
    User -- ( <レポートID>と<レポート>を\npostする )
    ( <レポートID>と<レポート>を\npostする ) ..> ( userとcontentに\n分解する ) : << precedes >>
    ( <レポートID>と<レポート>を\npostする ) ..> ( <レポートID>に紐付く\nレポートを探す ) : << precedes >>
    ( <レポートID>に紐付く\nレポートを探す ) ..> ( 該当レポートの\nuserとcontent\nを更新する ) : << precedes >>
    ( userとcontentに\n分解する ) ..> ( 該当レポートの\nuserとcontent\nを更新する ) : << precedes >>

    note right of ( <レポートID>と<レポート>を\npostする )
      @reply #0104503 Bプロジェクトでパスワードの長さが英数４桁だった。
    end note

    ' ----------- alternative
    ( 404 Not Found を返す ) <<error>>
    ( <レポートID>と<レポート>を\npostする ) ..> ( 404 Not Found を返す ) : <レポートID>に紐付く\nレポートが存在しない

@enduml
