@startuml

    ' ----------- meta
    title レポートを登録する

    actor User
    boundary bot
    participant post_new_action
    participant authenticator
    participant post_new_validator
    entity report

    ' ----------- main
    User -> bot : @reply post <message>
    bot -> post_new_action : set_message(message)
    activate post_new_action
      post_new_action -> authenticator : authenticate(user, channel)
      activate authenticator
        alt success
          authenticator --> post_new_action : Authentication Accepted
          post_new_action -> post_new_validator : validate_syntax(message)
          activate post_new_validator
            alt success
              post_new_validator --> post_new_action : Validated
              post_new_action -> post_new_action : parse_message(message)
              post_new_action -> post_new_action : create_report(user, content, status=:problem)
              post_new_action -> report : save(report)
              post_new_action --> bot : 200 OK
            else failure
              ' ----------- alternative
              post_new_validator --> post_new_action : Invalidate
              post_new_action --> bot : 400 Bad Request
            end
          deactivate post_new_validator
        else failure
          ' ----------- alternative
          authenticator --> post_new_action : Authentication Failure
          post_new_action --> bot : 403 Forbidden
        end
      deactivate authenticator
    deactivate post_new_action

@enduml
