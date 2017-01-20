@startuml

    ' ----------- meta
    title レポートを削除する

    skinparam usecase {
      FontColor<<error>> white
      FontName<<error>> Verdana
      BackgroundColor<<error>> gray
      BorderColor<<error>> black
    }

    actor User

    ' ----------- main
    User -- ( <レポートID>をdeleteする )

    note right of ( <レポートID>をdeleteする )
      @reply delete #0104503
    end note

' 1. slackのbotとして動作する
' 1. botは@replyでコマンドとレポートIDを受け付ける
' 1. 受け付けるコマンドは`delete #<レポートID>`
' 1. botは受け付けたレポートIDに紐つくレポートを論理削除する
' 	- 代替コース：受け付けたレポートIDに紐つくレポートが存在しない場合は、`404 Not Found`を返して終わる。
' 1. 履歴は保存しない
' 1. 改善状態を変更しない

@enduml
