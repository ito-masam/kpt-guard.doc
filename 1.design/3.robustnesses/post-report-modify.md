@startuml

    ' ----------- meta
    title レポートを修正する

    skinparam {
      ControlFontColor<<error>> white
      ControlFontName<<error>> Verdana
      ControlBackgroundColor<<error>> gray
      ControlBorderColor<<error>> black
    }

    actor User
    boundary bot
    control deassembly
    note bottom of deassembly
        userとcontentに
        分解する
    end note
    control find
    note bottom of find
        <レポートID>に紐付く
        レポートを探す
    end note
    control save
    note right of save
        該当レポートの
        userとcontent
        を更新する
    end note
    entity report


    ' ----------- main
    User -right-> bot
    bot -right--> deassembly : <レポートID>と<レポート>を\npostする
    bot -left--> find
    deassembly --> save
    find --> save
    save --- report
    save --> bot : 200 OKを返す

    ' ----------- alternative
    control error400 <<error>>
    note top of error400
        400 Bad Request を返す
    end note
    deassembly -up-> error400 : post_modifyの構文\nに適合しない
    error400 --> bot

    control error403 <<error>>
    note top of error403
        403 Forbiddenを返す
    end note
    deassembly -up->  error403 : Userとbotが同じ\nchannelに属していない
    error403 --> bot

    control error404 <<error>>
    note top of error404
        404 Not Foundを返す
    end note
    find -up-> error404 : <レポートID>に紐付く\nレポートが存在しない
    error404 --> bot


@enduml
