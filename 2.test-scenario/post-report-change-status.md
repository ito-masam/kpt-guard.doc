# レポートの改善状態を変更する

- @incident-botは、#bot-sandboxに属していること

## 基本コース problem to try

reportのidを指定すればwrote_userも書き変わるが本質的な問題ではないので考慮しない

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`problem`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #f8681be4-45f3-463f-aee4-00e3599da497 :try`
1. DBのReportテーブルが下記であること
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`try`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `200 OK`

## 基本コース try to keep

reportのidを指定すればwrote_userも書き変わるが本質的な問題ではないので考慮しない

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`try`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #f8681be4-45f3-463f-aee4-00e3599da497 :keep`
1. DBのReportテーブルが下記であること
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`keep`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `200 OK`

## 基本コース keep to try

reportのidを指定すればwrote_userも書き変わるが本質的な問題ではないので考慮しない

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`keep`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #f8681be4-45f3-463f-aee4-00e3599da497 :try`
1. DBのReportテーブルが下記であること
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`try`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `200 OK`

## 代替コース 400 Bad Request

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`problem`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post :keep`
1. DBのReportテーブルが*下記でないこと*
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`keep`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `incident-bot \ 400 Bad Request`

## 代替コース 400 Bad Request : problem to keep

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`problem`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #f8681be4-45f3-463f-aee4-00e3599da497 :keep`
1. DBのReportテーブルが*下記でないこと*
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`keep`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `incident-bot \ 400 Bad Request`

## 代替コース 400 Bad Request : keep to problemp

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`keep`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #f8681be4-45f3-463f-aee4-00e3599da497 :problem`
1. DBのReportテーブルが*下記でないこと*
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`problem`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `incident-bot \ 400 Bad Request`

## 代替コース 400 Bad Request : try to problem

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`try`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #f8681be4-45f3-463f-aee4-00e3599da497 :problem`
1. DBのReportテーブルが*下記でないこと*
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`problem`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `incident-bot \ 400 Bad Request`

## 代替コース 404 Not Found

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
    - status=`problem`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #7e967ab0-5153-4e83-b93e-bd5cd290e0a5 :try`
1. DBのReportテーブルが*下記でないこと*
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - status=`try`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `incident-bot \ 404 Not Found`
