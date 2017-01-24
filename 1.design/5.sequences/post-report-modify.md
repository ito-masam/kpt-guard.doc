@startuml

    ' ----------- meta
    title レポートを修正する

    actor User
    boundary bot
    participant post_modify_action
    participant authenticator
    participant post_modify_validator
    entity report

    ' ----------- main
    User -> bot : @reply post #id <string>
    bot -> post_modify_action : set_message(message)
    activate post_modify_action
      post_modify_action -> authenticator : authenticate(user, channel)
      activate authenticator
        alt success
          authenticator --> post_modify_action : Authentication Accepted
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
                  post_modify_action --> bot : 200 OK
                else failure
                  report --> post_modify_action
                  post_modify_action --> bot : 404 Not Found
                end
              deactivate report
            else failure
              ' ----------- alternative
              post_modify_validator --> post_modify_action : Invalidate
              post_modify_action --> bot : 400 Bad Request
            end
          deactivate post_modify_validator
        else failure
          ' ----------- alternative
          authenticator --> post_modify_action : Authentication Failure
          post_modify_action --> bot : 403 Forbidden
        end
      deactivate authenticator
    deactivate post_modify_action

@enduml
