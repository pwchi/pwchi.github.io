<!--
.. title: .NET Runtime Optimization Service 持續佔用 CPU
.. slug: .NET Runtime Optimization Service 持續佔用 CPU
.. date: 2017-06-29 14:00:00 UTC+08:00
.. tags: 自然輸入法, .NET
.. category:
.. link:
.. description:
.. type: text
-->
# 症狀

電腦安裝自然輸入法後，當電腦 Idle 一陣子，會發現CPU風扇轉速變高噪音變大，於工作管理員會看到 .NET Runtime Optimization Service 程序持續佔用 CPU。

![](/2017-06-29-.NET-Runtime-Optimization-Service-持續佔用-CPU/taskmanager.png "Windows工作管理員")

正常情況下 .NET RuntimeOptimization Service 會利用電腦空閒時間，將新安裝的 .NET 應用程式進行預編譯，來加快應用程式的啟動速度。通常預編譯只需執行一次，預編譯過的應用程式就不會再執行。[1][]

但問題出在，自然輸入法的預編譯過程一直無法完成，使得 .NET RuntimeOptimization Service 卡在那邊吃 CPU。

年初就有人在官方FB提出類似問題，但遲遲沒有人出來回應。[2][]

官方網站的常見問題也沒有關於這方面的相關資訊。

特別把這問題 email 詢問官方後，才收到會在之後版本修正的回覆，但也沒有提供任何 workaround。

不得不說，對網際智慧這種趨近射後不理的產品支援方式感到擔憂。

所以整理以下方法給大家自力救濟

[1]: https://blogs.msdn.microsoft.com/dotnet/2013/08/06/got-a-need-for-speed-net-apps-start-faster/ "Got a need for speed? .NET apps start faster."
[2]: https://www.facebook.com/IQGoing/posts/1508997545800403?comment_id=1572744919425665&amp;amp;reply_comment_id=1617858151581008&amp;amp;notif_t=feed_comment_reply&amp;amp;notif_id=1498703585774745 "自然輸入法官方FB"

# 驗證方法

**檢查目前 .NET Runtime Optimization Service 的預編譯是卡在什麼地方。** 

1. 以系統管理員身份啟動 CMD

2. `cd C:\Windows\Microsoft.NET\Framework\v2.0.50727\`

3. C:\Windows\Microsoft.NET\Framework\v2.0.50727>`ngen executeQueuedItems`

```
   Microsoft (R) CLR Native Image Generator - Version 2.0.50727.8745
   Copyright (c) Microsoft Corporation.  All rights reserved.
       Compiling assembly C:\Program Files\IQ Technology\Going11\Go11Util.dll (CLR v2.0.50727) ... 
```
   發現卡在`C:\ProgramFiles\IQ Technology\Going11\Go11Util.dll`跑不完，只要把 Go11Util.dll 從編譯佇列移除，問題就解決。

# 解決方法

**把 Go11Util.dll 從預編譯佇列移除**

1.  以系統管理員身份啟動 CMD

2. `cd C:\Windows\Microsoft.NET\Framework\v2.0.50727\`

3. C:\Windows\Microsoft.NET\Framework\v2.0.50727>`ngen.exeuninstall "C:\Program Files\IQ Technology\Going11\Go11Util.dll"`

```
   Microsoft (R) CLR Native Image Generator - Version 2.0.50727.8745
   Copyright (c) Microsoft Corporation.  All rights reserved.
   Uninstalling assembly C:\Program Files\IQ Technology\Going11\Go11Util.dll
```

4. C:\Windows\Microsoft.NET\Framework\v2.0.50727>`ngenexecuteQueuedItems`

```
   Microsoft (R) CLR Native Image Generator - Version 2.0.50727.8745
   Copyright (c) Microsoft Corporation.  All rights reserved.
   All compilation targets are up to date.
```
   Go11Util.dll 已經從編譯佇列移除
