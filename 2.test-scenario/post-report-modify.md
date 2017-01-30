# レポートを修正する

- @incident-botは、#bot-sandboxに属していること

## 基本コース

reportのidを指定すればwrote_userも書き変わるが本質的な問題ではないので考慮しない

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #f8681be4-45f3-463f-aee4-00e3599da497 暗号強度が大きすぎる`
1. DBのReportテーブルが下記であること
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が大きすぎる`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `200 OK`

## 代替コース 400 Bad Request (syntax error)

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post f8681be4-45f3-463f-aee4-00e3599da497 暗号強度が大きすぎる`
1. DBのReportテーブルが*下記でないこと*
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が大きすぎる`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `400 Bad Request`

## 代替コース 400 Bad Request (syntax error args over)

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #f8681be4-45f3-463f-aee4-00e3599da497 暗号強度が大きすぎる third_hoge_fuga`
1. DBのReportテーブルが*下記でないこと*
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が大きすぎる`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `400 Bad Request`

## 代替コース 400 Bad Request (not UUID)

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #f8681be4-45f3-463f 暗号強度が大きすぎる`
1. DBのReportテーブルが*下記でないこと*
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が大きすぎる`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `400 Bad Request`

## 代替コース 404 Not Found

1. DBのReportテーブルに下記を書き込む
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が小さすぎる`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`post #7e967ab0-5153-4e83-b93e-bd5cd290e0a5 暗号強度が大きすぎる`
1. DBのReportテーブルが*下記でないこと*
    - id=`f8681be4-45f3-463f-aee4-00e3599da497`
    - content=`暗号強度が大きすぎる`
1. DBのReportテーブルが*下記でないこと*
    - id=`7e967ab0-5153-4e83-b93e-bd5cd290e0a5`
    - content=`暗号強度が大きすぎる`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `404 Not Found`
