@startuml

    ' ----------- meta
    title レポートリストを出力する

    actor User
    boundary bot
    participant slack_adapter
    participant list_action
    participant list_validator
    entity report

    ' ----------- main
    User -> bot : @reply list
    bot -> list_action : set_message(message)
    activate list_action
        list_action -> list_validator : validate_syntax(message)
        activate list_validator
            alt success
                list_validator --> list_action : Valid
                list_action -> list_action : parse_message(message) : channel_id
                list_action -> report : list()
                activate report
                    alt success
                        report --> list_action : Found
                        list_action -> list_action : group_by_statuses(channel_id)
                        list_action -> slack_adapter : list(list, 200 OK)
                    else failure
                        report --> list_action : Not Found
                        list_action -> slack_adapter : error(404 Not Found)
                    end
                deactivate report
            else failure
                ' ----------- alternative
                list_validator --> list_action : Invalid
                list_action -> slack_adapter : error(400 Bad Request)
            end
        deactivate list_validator
    deactivate list_action
    slack_adapter -> bot : post message
    bot --> User

@enduml
