@startuml

    left to right direction

    mix_actor User

    class Report {
      - uuid
      - content
      - status
      - wrote_user_name
      - channel_id
    }

    class Channel {
      - id
    }
    note bottom of Channel {
      ChannelにUser/Reportが
      属することは
      Slackが保証する
    }

    User --o Channel

    Report "1..*" --o "1" Channel

@enduml
