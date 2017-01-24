@startuml

    ' ----------- meta
    title レポートを修正する

    actor User
    boundary bot
    participant slack_adapter
    participant post_modify_action
    participant post_modify_validator
    entity report

    ' ----------- main
    User -> bot : @reply post #id <string>
    bot -> post_modify_action : set_message(message)
    activate post_modify_action
        post_modify_action -> post_modify_validator : validate_syntax(message)
        activate post_modify_validator
            alt success
                post_modify_validator --> post_modify_action : Validated
                post_modify_action -> post_modify_action : parse_message(message)
                post_modify_action -> report : find(#id)
                activate report
                    alt success
                        report --> post_modify_action
                        post_modify_action -> post_modify_action : create_report(#id, user, content)
                        post_modify_action -> report : update(report)
                        post_modify_action -> slack_adapter : ok(200 OK)
                    else failure
                        report --> post_modify_action
                        post_modify_action -> slack_adapter : error(404 Not Found)
                    end
                deactivate report
            else failure
                ' ----------- alternative
                post_modify_validator --> post_modify_action : Invalidate
                post_modify_action -> slack_adapter : error(400 Bad Request)
            end
        deactivate post_modify_validator
    deactivate post_modify_action
    slack_adapter -> bot : post message
    bot --> User

@enduml
