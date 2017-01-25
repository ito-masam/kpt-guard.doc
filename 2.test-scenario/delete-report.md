# レポートを削除する

- @incident-botは、#bot-sandboxに属していること

## 基本コース

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`delete #f8681be4-45f3-463f-aee4-00e3599da497`
1. DBのReportテーブルが下記であること
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - deleted_at=`NOT NULL`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `200 OK`

## 代替コース 400 Bad Request

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`delete f8681be4-45f3-463f-aee4-00e3599da497`
1. DBのReportテーブルが*下記でないこと*
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - deleted_at=`NOT NULL`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `incident-bot \ 400 Bad Request`

## 代替コース 404 Not Found

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`delete 7e967ab0-5153-4e83-b93e-bd5cd290e0a5`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `incident-bot \ 404 Not Found`
