@startuml

    ' ----------- meta
    title レポートの改善状態を変更する

    skinparam {
      ControlFontColor<<error>> white
      ControlFontName<<error>> Verdana
      ControlBackgroundColor<<error>> gray
      ControlBorderColor<<error>> black
    }

    actor User
    boundary bot
    control status
    note bottom of status
        レポート一覧を返す
    end note
    control find
    note right of find
        <レポートID>に紐付く
        レポートを探す
    end note
    control update
    note left of update
        該当レポートの
        statusを
        更新する
    end note
    entity report


    ' ----------- main
    User -right-> bot
    bot -right-> status : <レポートID>と<改善状態>を\npostする
    status -right-> find
    find --> update
    update --- report
    update --> bot : 200 OKを返す

    ' ----------- alternative
    control error400 <<error>>
    note top of error400
        400 Bad Request を返す
    end note
    status -up-> error400 : post_statusの構文\nに適合しない
    error400 --> bot

    control error403 <<error>>
    note top of error403
        403 Forbiddenを返す
    end note
    status -up->  error403 : Userとbotが同じ\nchannelに属していない
    error403 --> bot

    control error404 <<error>>
    note top of error404
        404 Not Foundを返す
    end note
    find -up-> error404 : 有効なレポートが存在しない
    error404 --> bot

@enduml
