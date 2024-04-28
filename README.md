# Telegram聊天機器人超詳細懶人包，商管人都看得懂【附Python程式碼】

> 相關文章：
> [LINE機器人，商管人也看得懂的最詳細步驟【2020年最新更新版本】](https://marketingliveincode.com/2021/03/20/%E6%89%93%E9%80%A0%E8%81%8A%E5%A4%A9%E6%A9%9F%E5%99%A8%E4%BA%BA%EF%BC%8C%E5%95%86%E7%AE%A1%E4%BA%BA%E4%B9%9F%E7%9C%8B%E5%BE%97%E6%87%82%E7%9A%84%E6%9C%80%E8%A9%B3%E7%B4%B0%E6%AD%A5%E9%A9%9F%E3%80%9020/)
> [一個觀念，開啟Python 網路爬蟲成長之路！(含解說影片與程式碼)](https://medium.com/%E8%AA%A4%E9%97%96%E6%95%B8%E6%93%9A%E5%8F%A2%E6%9E%97%E7%9A%84%E5%95%86%E7%AE%A1%E4%BA%BAzino/%E5%88%9D%E5%AD%B8%E8%80%85%E5%BF%85%E7%9C%8B-%E4%B8%80%E5%80%8B%E8%A7%80%E5%BF%B5-%E9%96%8B%E5%95%9Fpython-%E7%B6%B2%E8%B7%AF%E7%88%AC%E8%9F%B2%E6%88%90%E9%95%B7%E4%B9%8B%E8%B7%AF-%E5%90%AB%E8%A7%A3%E8%AA%AA%E5%BD%B1%E7%89%87-fac0a17cd261)

您肯定有發現許多名人、政治人物的官方Line帳號，最近都不再發訊息了呢？其實有在經營Line@的朋友都知道，自從Line@的收費機制改變後，每發一次訊息所需的費用高答數十萬（不同粉絲數量金額不同），少有人能付的起。
![Telegram佈署的完整架構](https://i.imgur.com/eyHIpej.png)
> Line@所費變高，但Line bot價格沒變
> 為何還要換Telegram？

會讓我想要退出Line bot機器人的最大原因，是因為Line bot開始限制每月推播數量。免費版每月只有500則，常常測試到一半就爆表，更別說要用來發送訊息給客戶的您；就算是付費版，也還是有上限，超過以量計價，品牌端真的吃不消。
![資料來自Line Developer](https://i.imgur.com/GJ1mwhZ.png)

相對的我測試了Telegram，在15分鐘內，用迴圈無限循環，一直發送訊息，發送了1618封訊息，仍然還在進行。由於一直跳訊息有礙工作，所以沒有更深入的測試。
![使用for迴圈一直對機器發送訊息](https://i.imgur.com/t7Wvzbt.png)

Telegram成了品牌與使用者溝通的下一個平台，除了主打免費外，群組人數最多可達20萬人，大大超越Line的500人。其中令我著迷的是，Telegram在機器人上，有許多令我欣喜若狂的資源，但在本篇文章不會介紹，我們先以做出一個「會重複說話」的機器人，為可交付成果。
![可交付成果](https://i.imgur.com/Ic5TVoY.png)

## 平台創建
本文的建造方式與前篇文章[「打造聊天機器人，商管人也看得懂的最詳細步驟【2020年最新更新版本】」]()類似，都有申請Heroku與Github，但基於清楚的流程表達，這裡還是重複帶領您申請一次。若您已經熟悉了，可以自行跳過。

本次專案會使用到Heroku、Telegram、Github三個平台，以下為您詳細說明建立流程。
### Telegram API
[點這裡到BotFather](https://telegram.me/BotFather)
#### 呼叫BotFather
telegram並沒有如[Line Developer](https://developers.line.biz/zh-hant/)建立一個那麼龐大的平台，而是全部內嵌在telegram中。Telegram API的申請，首先要到[BotFather](https://telegram.me/BotFather)，按下send message，就會在您的Telegram打開這個官方的「機器人老爸」了。
![會多一個機器人好友BotFather](https://i.imgur.com/E4Wd41o.png)
#### 開始申請機器人
在您的Telegram中，BotFather有給我們幾個超連結，是Telegram API的詳細文件，而對話框輸入的位置，會有一個「Start」的按鈕，按下就會下達指令「/start」。
![申請機器人](https://i.imgur.com/Cn57mWc.png)

#### 創立新的機器人
每個「/」都代表一個指令，Telegram這邊介紹許多指令。而我們要使用到的是「/newbot」，顧名思義，就是創立一個新的機器人。這裡可以選擇用點擊的或者直接輸入「/newbot」。
![創立新的機器人](https://i.imgur.com/XS79zYO.png)

#### 為機器人命名
命名必須符合規則，Telegram要求機器人名稱的結尾一定要是「_bot」或者「Bot」，並且這個名稱必須要是獨一無二的。因此舉例來說，當初我想要命名「Ivan_bot(被用過)」或者「Ivanbot(不符合規定)」都不行，最後我使用「IvanYang_bot」作為機器人的名稱。
![為機器人命名](https://i.imgur.com/cUCylQW.png)

到這裡機器人的申請告一段落，最後留下一串非常重要的token，因為作者必須保護自己的隱私，因此在本文將token假設為「8302849587:egrRdav568Qf9kEGfYJU」。

> 請注意！若有心人士拿到這個token，他就可以操控您的機器人，因此請妥善保管。

#### 啟動機器人
完成後就會跳出聊天視窗，輸入的位置點選「Start」，就會看到屬於您自己的機器人了。
![啟動機器人](https://i.imgur.com/bbPYUkp.png)

### Heroku平台
[點這裡到Heroku](https://www.heroku.com/)
平台在文章[「打造聊天機器人，商管人也看得懂的最詳細步驟【2020年最新更新版本】」]()中有詳細介紹。

#### 創辦heroku帳號
密碼要求必須要英文大小寫、數字混合。接下來的範例，需要將程式碼部屬（傳送）到上面。
![創辦heroku帳號](https://i.imgur.com/2Pdua2P.png)

#### 創立一個新的APP專案
按下右上角「Creat new app」。
![新的APP專案](https://i.imgur.com/o477uWm.png)

#### 創立專案：
專案的名稱必須是世界上獨一無二，類似線上遊戲角色ID的概念。到這裡heroku平台就告一段落了。等等進行串接的時候會再回來。
![創立專案](https://i.imgur.com/aJg1Ehe.png)

### Github：
平台在文章[「打造聊天機器人，商管人也看得懂的最詳細步驟【2020年最新更新版本】」]()中有詳細介紹。

#### 創立Github帳號：
[點這裡到Github](https://github.com/)
因為資安意識的抬頭，帳號申請加入了很多機器人驗證的過程。
![創立Github帳號](https://i.imgur.com/mQFyX2q.png)

## 三大平台串聯
Telegram的串接，流程是與line一樣的，但並沒有像line那樣的繁瑣，相信您會更快上手。

### 下載Telegram bot程式碼
裡面有三個檔案，簡單與您介紹。
> Procfile：
> Heroku所需要的文件，讓Heroku的主機知道要開啟機器人的主程式是哪一個。因此檔案app.py的名稱若有做修改，這裡面也必須一起修改。

> app.py：
> 機器人的主程式，本文章會修改的程式碼都在這個檔案中。檔案內的方法reply_handler(bot, update)是主要編輯區塊，但與Line不同的是，Telegram API支援呼叫function，因此reply_handler並不是唯一可以被使用者呼叫的方法。

> requirements.txt：
> 告訴Heroku要安裝哪一些套件。requirement的意思就是先決條件，要搭建這個機器人，需要用到的套件，就是他的先決條件。
![](https://i.imgur.com/4sWykZo.png)

### 貼上token
將我們一開始申請機器人所得到的token貼在app.py程式碼第10行。
![貼上token](https://i.imgur.com/yp9BOUC.png)

### 貼上你自己的ID
找到自己ID的方式很有趣。首先先跟自己的機器人聊天兩句（當然他還不會理你）。而後在瀏覽器中輸入以下網址：
```
https://api.telegram.org/bot【你的token】/getUpdates
```
例如範例：
```
https://api.telegram.org/bot8302849587:egrRdav568Qf9kEGfYJU/getUpdates
```
您就會在網頁中得到類似下列的訊息。其中第二行可以看到「”id”: 1975876568」就是我的ID，這裡也是因為資安疑慮，所以修圖替換過。
![貼上你自己的ID](https://i.imgur.com/HQFJFrM.png)

最後將你的ID貼到app.py程式碼中的第11行。
![貼上你自己的ID](https://i.imgur.com/8jFRorH.png)

### 串接Webhook
Webhook的設定方式與ID類似。首先到我們剛辦好的Heroku專案中，按下「Open app」，複製打開的網站網址。接下來將以下網址在瀏覽器中貼上：

> 請確認最後面要加/hook
```
https://api.telegram.org/bot【你的token】/setWebhook?url=【你的Heroku專案網址】/hook
```
如我的範例：
```
https://api.telegram.org/bot8302849587:egrRdav568Qf9kEGfYJU/setWebhook?url=https://ivan20200505.herokuapp.com/hook
```
![串接Webhook](https://i.imgur.com/J5ZYmnd.png)

### 上傳程式碼到平台
到了驗收的時刻，流程與之前[Line bot機器人]()的教學一模一樣，但又更為簡單。

#### 上傳程式碼到Github
請切換到各位剛辦好的Github專案，點選「Upload files」，並將四個檔案都拉進去。
![上傳程式碼到Github](https://i.imgur.com/533oCuc.png)

#### Heroku與Github連接
請選擇Deployment method中的Github，以前機器人都是使用第一個heroku Git，他是使用終端機的方式。當初會這樣選擇是因為，當時github設置私有專案是要付費的，但現在變成免費的，那也會建議商管人用圖形化介面的Github就好，不要一直與終端機打交道。
https://miro.medium.com/max/4006/1*2bPvhsjcloQ7S3PTUFB0qA.png

#### 佈署機器人
拉到最下方，按下Deploy Branch即可佈署了。
![](https://i.imgur.com/lVFh3ts.png)

## 測試機器人
如果您的機器人有主動密你說：「你可以開始了」，那心就可以放一半了，如果你對機器人說話，他會重複你說的話，那就是成功了喔。\
![測試機器人](https://i.imgur.com/5AOUENq.png)
