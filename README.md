# Laravel-Echo-Authorizer-Example

### 中文說明
使用 Laravel Reverb + Echo 時，若採用自訂驗證（例如需攜帶 Cookies 或其他進行驗證），必須自行撰寫 Echo 的 authorizer 方法。

否則你會看到「WebSocket 已連線」（connected），但頻道實際上沒有被訂閱成功（subscribe 未觸發），導致 whisper()、listenForWhisper() 等功能無法運作。

請務必以 x-www-form-urlencoded 格式送出 socket_id 與 channel_name，驗證成功時呼叫 callback(null, data)，驗證失敗時呼叫 callback(true, null)，否則 Laravel Echo 將無法完成訂閱，Reverb 也不會將訊息轉發給該使用者。

### English Explanation
When using Laravel Reverb with Laravel Echo and custom authentication (such as sending cookies or Bearer tokens), you must define a custom authorizer method in your Echo configuration.

Otherwise:
You will see that the WebSocket connection is established (connected), But the channel will not be subscribed successfully (no subscribed event), As a result, features like whisper() and listenForWhisper() will not work.

You must:
Send socket_id and channel_name using x-www-form-urlencoded format, Call callback(null, data) on successful authorization, Call callback(true, null) on failure, If you skip these steps, Laravel Echo will fail to subscribe to the channel, and Reverb will not forward any messages to that user.
