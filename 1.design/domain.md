@startuml

left to right direction

class User {
	- enrolled_channel_id
}
class Report {
	- id
	- who
	- content
	- status
	- created_at
	- deleted
}
class EnrolledChannels {
	- id
}

User "1"--o "1..*" Report
note on link
	@reply post new
	@reply post status
	@reply list
	@reply delete
end note
Report "1..*" --- "1" EnrolledChannels
note on link: isAvailable()

@enduml
