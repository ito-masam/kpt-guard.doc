# レポートを削除する

@incident-botは、#bot-sandboxに属していること

## 基本コース

1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が小さすぎる`と書き込む
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
  - 送るメッセージは`delete #1`
1. DBのReportテーブルが下記であること
  - id=1
  - deleted_at=NOT NULL
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
  - `200 OK`

## 代替コース 400 Bad Request

1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が小さすぎる`と書き込む
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
  - 送るメッセージは`delete 1`
1. DBのReportテーブルが*下記でないこと*
  - id=1
  - deleted_at=NOT NULL
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
  - `incident-bot \ 400 Bad Request`

## 代替コース 404 Not Found

1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が小さすぎる`と書き込む
1. DBのReportテーブルのid列が2且つcontent列に`暗号強度が多きすぎる`と書き込む
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
  - 送るメッセージは`delete 2`
1. DBのReportテーブルが*下記でないこと*
  - id=1
  - deleted_at=NOT NULL
1. DBのReportテーブルが*下記でないこと*
  - id=2
  - deleted_at=NOT NULL
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
  - `incident-bot \ 404 Not Found`
