@startuml

    class Report {
      - id
      - string
      - status
      - wrote_user
      - created_at
      - deleted_at
      + save()
      + find()
      + list()
      + update()
      + delete()
    }

@enduml
