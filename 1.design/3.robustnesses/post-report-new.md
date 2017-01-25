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
    control deassembly
    note top of deassembly
        user, content,
        channel_idに分解する
    end note
    control status_problem
    note bottom of status_problem
        改善状態を
        problemに設定する
    end note
    control save
    note left of save
        user, content,
        status, channel_id,
        を保存する
    end note
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

@enduml
