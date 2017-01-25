@startuml

    ' ----------- meta
    title レポートの改善状態を変更する

    actor User
    boundary bot
    participant slack_adapter
    participant post_status_action
    participant post_status_validator
    entity report

    ' ----------- main
    User -> bot : @reply post #uuid :status
    bot -> post_status_action : set_message(message)
    activate post_status_action
        post_status_action -> post_status_validator : validate_syntax(message)
        activate post_status_validator
            alt success
                post_status_validator --> post_status_action : Valid
                post_status_action -> post_status_action : parse_message(message) : #uuid, :status
                post_status_action -> report : find(#uuid)
                activate report
                    alt success
                        report --> post_status_action : Found
                        post_status_action -> post_status_action : create_report(#uuid, :status)
                        post_status_action -> report : update(report)
                        post_status_action -> slack_adapter : ok(200 OK)
                    else failure
                        report --> post_status_action : Not Found
                        post_status_action -> slack_adapter : error(404 Not Found)
                    end
                deactivate report
            else failure
                ' ----------- alternative
                post_status_validator --> post_status_action : Invalid
                post_status_action -> slack_adapter : error(400 Bad Request)
            end
        deactivate post_status_validator
    deactivate post_status_action
    slack_adapter -> bot : post message
    bot --> User

@enduml
