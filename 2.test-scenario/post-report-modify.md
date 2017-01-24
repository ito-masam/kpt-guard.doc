# レポートを修正する

reportのidを指定すればwrote_userも書き変わるが本質的な問題ではないので考慮しない

1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が小さすぎる`と書き込む
1. slack api tokenを使って、@incident-botへ@replyでメッセージを送る
1. 送るメッセージは`post #1 暗号強度が大きすぎる`
1. DBのReportテーブルのid列が1且つcontent列に`暗号強度が大きすぎる`と書き込まれていること
