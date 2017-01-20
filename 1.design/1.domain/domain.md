@startuml

    left to right direction

    mix_actor User

    class Report {
      - id
      - content
      - status
      + post()
      + delete()
      + post-status()
    }

    class Channel {
      - id
      + isMember(user_id)
    }

    User --o Channel
    note on link
      UserはChannelに属している
    end note

    Report "1..*" --o "1" Channel
    note on link
      ReportはChannelに属している
    end note

@enduml
