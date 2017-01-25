# レポートを新規登録する

- @incident-botは、#bot-sandboxに属していること
- channel_idは変換後名を表記している

## 基本コース

1. slack api tokenを使って、@incident-botへ@replyでメッセージを送る
    - 送るメッセージは`post 暗号強度が小さすぎる`
1. DBのReportテーブルが下記であること
    - id=`＜なんらかのUUID＞`
    - content=`暗号強度が小さすぎる`
    - channel_id=`#bot-sandbox`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `200 OK`

## 代替コース 400 Bad Request

1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記になること
    - `incident-bot \ 400 Bad Request`
