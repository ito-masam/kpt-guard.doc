@startuml

    class Report {
      - uuid
      - content
      - status
      - wrote_user_name
      - channel_id
      - created_at
      - deleted_at
      + save(self)
      + find(uuid)
      + list(channel_id)
      + update(self)
      + delete(uuid)
    }

@enduml
