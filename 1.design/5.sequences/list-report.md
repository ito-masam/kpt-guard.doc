@startuml

    ' ----------- meta
    title レポートリストを出力する

    actor User
    boundary bot
    participant slack_adapter
    participant list_action
    participant authenticator
    participant list_validator
    entity report

    ' ----------- main
    User -> bot : @reply list
    bot -> list_action : set_message(message)
    activate list_action
      list_action -> authenticator : authenticate(user, channel)
      activate authenticator
        alt success
          authenticator --> list_action : Authentication Accepted
          list_action -> list_validator : validate_syntax(message)
          activate list_validator
            alt success
              list_validator --> list_action : Valid
              list_action -> list_action : parse_message(message)
              list_action -> report : list()
              activate report
                alt success
                  report --> list_action : Found
                  list_action -> list_action : list_report_group_by_statuses()
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
        else failure
          ' ----------- alternative
          authenticator --> list_action : Authentication Failure
          list_action -> slack_adapter : error(403 Forbidden)
        end
      deactivate authenticator
    deactivate list_action
    slack_adapter -> bot : post message
    bot --> User

@enduml
