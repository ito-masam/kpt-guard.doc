# レポートを一覧する

- @incident-botは、#bot-sandboxに属していること

## 基本コース

1. DBのReportテーブルに下記を書き込む
    1. problem
        - id=`da2fd65e-0708-48a7-ac1e-ded06d289dfc`
        - content=`暗号強度が小さすぎる`
        - channel_id=`#bot-sandbox`
        - status=`problem`
    2. try
        - id=`e8c5f921-b941-4b55-83e6-be0b086ad3bb`
        - content=`暗号強度を大きくする`
        - channel_id=`#bot-sandbox`
        - status=`try`
    3. keep
        - id=`d780bf2e-da5a-409f-bbb8-d99181466318`
        - content=`暗号強度がちょうどいい`
        - channel_id=`#bot-sandbox`
        - status=`keep`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`list`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - 
    ```
    keep
        - 暗号強度がちょうどいい d780bf2e-da5a-409f-bbb8-d99181466318 @user_name
    problem
        - 暗号強度が小さすぎる da2fd65e-0708-48a7-ac1e-ded06d289dfc @user_name
    try
        - 暗号強度が大きすぎる e8c5f921-b941-4b55-83e6-be0b086ad3bb @user_name
    ```

## 代替コース 400 Bad Request

1. DBのReportテーブルに下記を書き込む
    1. problem
        - id=`da2fd65e-0708-48a7-ac1e-ded06d289dfc`
        - content=`暗号強度が小さすぎる`
        - channel_id=`#bot-sandbox`
        - status=`problem`
    2. try
        - id=`e8c5f921-b941-4b55-83e6-be0b086ad3bb`
        - content=`暗号強度が大きすぎる`
        - channel_id=`#bot-sandbox`
        - status=`try`
    3. keep
        - id=`d780bf2e-da5a-409f-bbb8-d99181466318`
        - content=`暗号強度がちょうどいい`
        - channel_id=`#bot-sandbox`
        - status=`keep`
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`list #da2fd65e-0708-48a7-ac1e-ded06d289dfc`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `400 Bad Request`

## 代替コース 404 Not Found

1. DBのReportテーブルに何も書き込まない
1. slack api tokenを使って、#bot-sandboxで@incident-botへメッセージを送る
    - 送るメッセージは`list`
1. #bot-sandboxの最新コメント（or botのレスポンス）が下記であること
    - `404 Not Found`
