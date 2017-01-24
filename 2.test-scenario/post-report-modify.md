# レポートを修正する

@incident-botは、#bot-sandboxに属していること

## 基本コース

reportのidを指定すればwrote_userも書き変わるが本質的な問題ではないので考慮しない

1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が小さすぎる`と書き込む
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
1. 送るメッセージは`post #1 暗号強度が大きすぎる`
1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が大きすぎる`と書き込まれていること
1. #bot-sandboxの最新コメント（or botのレスポンス）に`200 OK`が確認できること

## 代替コース 400 Bad Request

1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が小さすぎる`と書き込む
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
1. 送るメッセージは`post 1 暗号強度が大きすぎる`
1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が大きすぎる`と書き込まれていないこと
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記になること
  - `incident-bot \ 400 Bad Request`

## 代替コース 404 Not Found

1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が小さすぎる`と書き込む
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
1. 送るメッセージは`post 2 暗号強度が大きすぎる`
1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が大きすぎる`と書き込まれていないこと
1. DBのReportテーブルのid列が2且つcontent列に`暗号強度が大きすぎる`と書き込まれていないこと
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記になること
  - `incident-bot \ 404 Not Found`
