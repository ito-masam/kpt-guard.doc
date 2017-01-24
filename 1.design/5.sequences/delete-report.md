@startuml

    ' ----------- meta
    title レポートを削除する

    actor User
    boundary bot
    participant slack_adapter
    participant delete_action
    participant authenticator
    participant delete_validator
    entity report

    ' ----------- main
    User -> bot : @reply delete #id
    bot -> delete_action : set_message(message)
    activate delete_action
      delete_action -> authenticator : authenticate(user, channel)
      activate authenticator
        alt success
          authenticator --> delete_action : Authentication Accepted
          delete_action -> delete_validator : validate_syntax(message)
          activate delete_validator
            alt success
              delete_validator --> delete_action : Valid
              delete_action -> delete_action : parse_message(message)
              delete_action -> report : find(#id)
              activate report
                alt success
                  report --> delete_action : Found
                  delete_action -> delete_action : create_report(#id)
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
        else failure
          ' ----------- alternative
          authenticator --> delete_action : Authentication Failure
          delete_action -> slack_adapter : error(403 Forbidden)
        end
      deactivate authenticator
    deactivate delete_action
    slack_adapter -> bot : post message
    bot --> User

@enduml
