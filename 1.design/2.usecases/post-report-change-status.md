@startuml

    ' ----------- meta
    title レポートの改善状態を変更する

    skinparam usecase {
      FontColor<<error>> white
      FontName<<error>> Verdana
      BackgroundColor<<error>> gray
      BorderColor<<error>> black
    }

    actor User

    ' ----------- main
    User -- ( <レポートID>と<改善状態>を\npostする )
    ( <レポートID>と<改善状態>を\npostする ) ..> ( <レポートID>に紐付く\nレポートを探す ) : << precedes >>
    ( <レポートID>に紐付く\nレポートを探す ) ..> ( 該当レポートの\nstatusを\n更新する ) : << precedes >>

    note left of ( <レポートID>と<改善状態>を\npostする )
      @reply post #f8681be4-45f3-463f-aee4-00e3599da497 :try
      @reply post #f8681be4-45f3-463f-aee4-00e3599da497 :keep
    end note

    ' ----------- alternative
    ( 400 Bad Request を返す ) <<error>>
    ( <レポートID>と<改善状態>を\npostする ) ..> ( 400 Bad Request を返す ) : post_statusの構文\nに適合しない

    ( 404 Not Found を返す ) <<error>>
    ( <レポートID>に紐付く\nレポートを探す ) ..> ( 404 Not Found を返す ) : <レポートID>に紐付く\nレポートが存在しない

    ( 400 Bad Request を返す ) <<error>>
    ( <レポートID>と<改善状態>を\npostする ) ..> ( 400 Bad Request を返す ) : 改善状態が\n:keepか:try以外\nの場合
    ( <レポートID>に紐付く\nレポートを探す ) ..> ( 400 Bad Request を返す ) : 改善状態が\n遷移順に\n違反する場合
    note on link
      :problem -> :try <--> :keep
    end note

@enduml
