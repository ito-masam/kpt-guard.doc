@startuml

    ' ----------- meta
    title レポートを削除する

    actor User
    boundary bot
    participant slack_adapter
    participant delete_action
    participant delete_validator
    entity report

    ' ----------- main
    User -> bot : @reply delete #uuid
    bot -> delete_action : set_message(message)
    activate delete_action
        delete_action -> delete_validator : validate_syntax(message)
        activate delete_validator
            alt success
                delete_validator --> delete_action : Valid
                delete_action -> delete_action : parse_message(message) : #uuid
                delete_action -> report : find(#uuid)
                activate report
                    alt success
                        report --> delete_action : Found
                        delete_action -> delete_action : create_report(#uuid)
                        delete_action -> report : delete(report)
                        delete_action -> slack_adapter : ok(200 OK)
                    else failure
                        report --> delete_action : Not Found
                        delete_action -> slack_adapter : error(404 Not Found)
                    end
                deactivate report
            else failure
                ' ----------- alternative
                delete_validator --> delete_action : Invalid
                delete_action -> slack_adapter : error(400 Bad Request)
            end
        deactivate delete_validator
    deactivate delete_action
    slack_adapter -> bot : post message
    bot --> User

@enduml
