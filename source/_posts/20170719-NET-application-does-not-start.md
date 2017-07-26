---
title: '.NET 應用程式開不起來'
date: 2017-07-19 12:08:21
tags: [Windows,.NET,C#,Programming]
categories: .NET
---
# 症狀
*執行.NET應用程式後沒反應，檢查工作管理員有該處理程序，卻遲遲看不到主畫面。*

一開始使用.NET平台開發應用程式時，總覺得建置不會遇到什麼問題，畢竟都是使用Windows作業系統，並且透過.NET Framework。

<!-- more -->

於是當遇到提供給對方的應用程式開不來的情況時，當下的直覺反應：
* .NET Framework問題：
 * 重新安裝.NET Framwork
* 使用者權限問題：
 * 用系統管理員開啟，或是直接關閉UAC
 * 關閉防毒軟體，或是加入例外清單

當這兩個方向都無效時，實在是忍不住喊出了程式設計師經典的台詞：
{% img [class names] https://blog.codinghorror.com/content/images/uploads/2007/03/6a0120a85dcdae970b0128776ff992970c-pi.png [在我的電腦上是正常的啊] %}


# 解方
喊歸喊，問題還是得解決，於是試著透過事件檢視器找出問題

`開始` → `執行` → `eventvwr`

{% asset_img eventvwr.png [事件檢視器] %}

此例為應用程式引發了UnauthorizedAccessException，可能試圖存取某個檔案，卻沒有權限。最後居然是該檔案被設成了唯讀屬性，取消唯讀屬性後，應用程式即可順利執行，搞定收工！

# 參考
[Windows programming: The "it works on my machine" syndroma](http://codebetter.com/patricksmacchia/2010/04/06/windows-programming-the-quot-it-works-on-my-machine-quot-syndroma/)

