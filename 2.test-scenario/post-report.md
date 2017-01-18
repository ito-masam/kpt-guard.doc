# test scenario


## レポートを登録する(light)

インタフェースの確認

1. slack api tokenを使って、@incident-botへ@replyでメッセージを送る
1. 送るメッセージは`post 暗号強度が小さすぎる`
1. http://localhost:3000/に`暗号強度が小さすぎる`と表示されること

## レポートを登録する

インタフェースの確認

1. slack api tokenを使って、@incident-botへ@replyでメッセージを送る
1. 送るメッセージは`post 暗号強度が小さすぎる`
1. DBのReportテーブルのcontent列に`暗号強度が小さすぎる`と書き込まれていること

