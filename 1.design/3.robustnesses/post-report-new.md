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
    User --> bot
    bot --> deassembly : <レポート>をpostする
    deassembly --> status_problem : OK
    status_problem --> save
    save --- report
    save --- bot : 200 OKを返す

    ' ----------- alternative
    control error403 <<error>>
    deassembly -->  error403 : Userとbotが同じchannelに属していない
    error403 --> bot : 403 Forbiddenを返す

@enduml
