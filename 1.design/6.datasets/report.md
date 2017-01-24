@startuml

    class Report {
      - id
      - string
      - status
      - wrote_user
      - created_at
      - deleted_at
      + save(self)
      + find(id)
      + list()
      + update(self)
      + delete(id)
    }

@enduml
