@startuml

    ' ----------- meta
    title レポートを削除する

    skinparam {
      ControlFontColor<<error>> white
      ControlFontName<<error>> Verdana
      ControlBackgroundColor<<error>> gray
      ControlBorderColor<<error>> black
    }

    actor User
    boundary bot
    control find
    note bottom of find
        <レポートID>に紐付く
        レポートを探す
    end note
    control delete
    note right of delete
        該当レポート
        を論理削除する
    end note
    entity report


    ' ----------- main
    User -right-> bot
    bot -right--> find : <レポートID>をdeleteする
    find --> delete
    delete --- report
    delete --> bot : 200 OKを返す

    ' ----------- alternative
    control error400 <<error>>
    note top of error400
        400 Bad Request を返す
    end note
    find -up-> error400 : deleteの構文\nに適合しない
    error400 --> bot

    control error404 <<error>>
    note top of error404
        404 Not Foundを返す
    end note
    find -up-> error404 : <レポートID>に紐付く\nレポートが存在しない
    error404 --> bot

@enduml
