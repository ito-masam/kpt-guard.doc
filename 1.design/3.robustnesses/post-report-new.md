@startuml

    ' ----------- meta
    title レポートを登録する

    skinparam {
      ControlFontColor<<error>> white
      ControlFontName<<error>> Verdana
      ControlBackgroundColor<<error>> gray
      ControlBorderColor<<error>> black
    }

    actor User
    boundary bot
    control deassembly as "userとcontentに\n分解する"
    control status_problem as "改善状態を\nproblemに設定する"
    control save as "userとcontentと\nstatusを保存する"
    entity report


    ' ----------- main
    User -right-> bot
    bot -right-> deassembly : <レポート>をpostする
    deassembly --> status_problem : OK
    status_problem --> save
    save --- report
    save --- bot : 200 OKを返す

    ' ----------- alternative
    control error400 <<error>>
    note top of error400
        400 Bad Request を返す
    end note
    deassembly -up-> error400 : post_newの構文\nに適合しない
    error400 --> bot

    control error403 <<error>>
    note top of error403
        403 Forbiddenを返す
    end note
    deassembly -up->  error403 : Userとbotが同じ\nchannelに属していない
    error403 --> bot

@enduml
