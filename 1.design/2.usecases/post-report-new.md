@startuml

  title レポートを登録する

  actor User
  User --- ( <レポート>をpostする )
  ( <レポート>をpostする ) ..> ( userとcontentに\n分解する ) : << precedes >>
  ( userとcontentに\n分解する ) ..> ( 改善状態を\nproblem固定とする ) : << precedes >>
  ( 改善状態を\nproblem固定とする ) ..> ( 保存する ) : << precedes >>

  note right of ( <レポート>をpostする )
    @reply post Aプロジェクトでパスワードの長さが英数４桁だった。
  end note

@enduml
