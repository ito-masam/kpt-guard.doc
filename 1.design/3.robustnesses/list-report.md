@startuml

    ' ----------- meta
    title レポートリストを出力する

    skinparam {
      ControlFontColor<<error>> white
      ControlFontName<<error>> Verdana
      ControlBackgroundColor<<error>> gray
      ControlBorderColor<<error>> black
    }

    actor User
    boundary bot
    control list
    note bottom of list
        レポート一覧を返す
    end note
    control collect
    note right of collect
        有効な
        レポートを集める
    end note
    entity report


    ' ----------- main
    User -right-> bot
    bot -right--> list : listする
    list --> collect
    collect --- report
    collect --> bot : レポート一覧を返す
    note on link
        全ての改善状態の
        レポートを出力する
    end note

    ' ----------- alternative
    control error400 <<error>>
    note top of error400
        400 Bad Request を返す
    end note
    list -up-> error400 : listの構文\nに適合しない
    error400 --> bot

    control error403 <<error>>
    note top of error403
        403 Forbiddenを返す
    end note
    list -up->  error403 : Userとbotが同じ\nchannelに属していない
    error403 --> bot

    control error404 <<error>>
    note top of error404
        404 Not Foundを返す
    end note
    list -up-> error404 : 有効なレポートが存在しない
    error404 --> bot

@enduml
