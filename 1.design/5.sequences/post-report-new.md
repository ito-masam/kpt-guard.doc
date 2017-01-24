@startuml

    ' ----------- meta
    title レポートを登録する

    actor User
    boundary bot
    participant slack_adapter
    participant post_new_action
    participant post_new_validator
    entity report

    ' ----------- main
    User -> bot : @reply post <string>
    bot -> post_new_action : set_message(message)
    activate post_new_action
        post_new_action -> post_new_validator : validate_syntax(message)
        activate post_new_validator
            alt success
                post_new_validator --> post_new_action : Validated
                post_new_action -> post_new_action : parse_message(message)
                post_new_action -> post_new_action : create_report(user, content, status=:problem)
                post_new_action -> report : save(report)
                post_new_action -> slack_adapter : ok(200 OK)
            else failure
                ' ----------- alternative
                post_new_validator --> post_new_action : Invalidate
                post_new_action -> slack_adapter : error(400 Bad Request)
            end
        deactivate post_new_validator
    deactivate post_new_action
    slack_adapter -> bot : post message
    bot --> User

@enduml
