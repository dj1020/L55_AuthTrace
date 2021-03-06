# Laradebut #12 新手必備！Laravel 登入機制解密 源碼追追追

## 事前準備

* Composer
* 全新安裝 Laravel 5.5.25 本日範例
* 至少你要想辦法看得到 Laravel Welcome 的首頁, ex: `php artisan serve`
* 把資料庫建好，權限設好，可以執行 `php artisan migrate` 不會出錯為準
* 執行 `php artisan make:auth`
* (optional) 建立一個 mailtrap.io 的帳號，方便測試忘記密碼寄信的功能

## 狀況一： 在註冊表單加欄位，加入 username 之後可以登入使用

* 改 migration 檔 `2014_10_12_000000_create_users_table.php` ，在 `users` table 中加入 usernmae 欄位，改完記得把 DB 整個砍掉，再跑一次 `php artisan migrate`
* 改 view 檔 `register.blade.php` ，加入 username 欄位的 input tag
* 改 `RegisterController@create` 把欄位加入
* (建議) 也要改 `RegisterController@validator` 把 `username` 視為 `required`
* 測試看看應該可以了



















## 狀況二： 用 username 或是 email 應該都要可以登入

* 改 view 欄位描述調整，並把 email 驗證拿掉 (表示要後端自己驗是不是 email)
* 調整 `LoginController`，重點在覆寫 `credentials` 這個方法
* 如果要改更大，還可以覆寫 `attemptLogin` 方法













## 狀況三： 密碼輸錯的訊息是英文的？幫我弄成中文

* (不建議，但快) 硬幹改 `lang/en/auth.php`
* 調整 `lang/` 裡的檔案，加入 `lang/zh-tw` 相關檔 (從 `lang/en` 複製過來改就行了)
* 調整 `config/app.php` 裡的 `locale` 成 `zh-tw`
* 建議放在 `.env` 中設定














## 狀況四： 已登入的人不要導回首頁行不行？

* 改 `LoginController` 的 `$redirectTo`
* (進階) 新增 `redirectPath` 方法在 `LoginController` 裡，建議使用 `return route('routeName');`

* 加碼追 Code ，未登入成功的人是怎麼被導回 login 頁面的
















## 狀況五： 忘記密碼信的內容怎麼改

* (簡單) 覆寫 `ForgotPasswordController` 的 `sendResetLinkEmail` 方法
* (高階) 參考 `PasswordBroker` 自己寫一個 borker，extends `PasswordBrokerContract` ，並覆寫 `broker()` 方法









