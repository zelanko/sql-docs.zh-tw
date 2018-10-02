---
title: 針對 Reporting Services 訂用帳戶和傳遞進行疑難排解 | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: ae1775f7-9919-48ca-8bd7-cc16df274e2c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a8384ad803f70b6ec4bcca2bca49390f969a661
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604306"
---
# <a name="troubleshoot-reporting-services-subscriptions-and-delivery"></a>為 Reporting Services 訂閱與傳遞疑難排解
  
    
使用本主題，即可針對您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] 報表訂閱、排程與傳遞時遇到的問題進行疑難排解。  
## <a name="log-information"></a>記錄資訊
 
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 中的 [訂閱] 頁面包含訂閱的狀態，但如果訂閱發生問題， [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 記錄中會有詳細資訊。 
![ssrs_tutorial_datadriven_subscription_status_ReportManager](../../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png)

**追蹤記錄** ︰追蹤記錄是寫入下列位置的文字檔： `\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`

以下是範例記錄項目：

```
   subscription WindowsService_10   4c7c    05/24/2016-01:05:06  e ERROR     Failure writing file \\ServerName\SalesReports\so71949.xls : Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider+NetworkErrorException: An impersonation error occurred using the security context of the current user. ---> System.ArgumentException: Value does not fall within the expected range.  05/24/2016
```
如需 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 追蹤記錄的詳細資訊，請參閱： 
+ [報表伺服器追蹤記錄](../../reporting-services/report-server/report-server-service-trace-log.md)。
+ [Reporting Services 記錄檔](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。

**執行記錄檢視：**

執行記錄是 ReportServer SQL 資料庫中的檢視，如需 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 的詳細資訊，請參閱 [Reporting Services ExecutionLog 和 ExecutionLog3 檢視](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)。  

----------
## <a name="unable-to-send-reports-using-e-mail-with-windows-server-2003-and-pop3"></a>無法使用 Windows Server 2003 和 POP3，以電子郵件傳送報表  
如果您是在 Microsoft Windows Server 2003 上執行使用郵局通訊協定第 3 版 (POP3) 的電子郵件應用程式，可能會無法使用本機 POP3 伺服器來傳送報表。 如果您設定報表伺服器以本機 POP3 伺服器傳送電子郵件，並建立傳送報表的訂閱，則可能會收到下列錯誤訊息：  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Failure sending mail: <error message>`  
  
其中 \<錯誤訊息> 會取代為協同作業資料物件 (CDO) 所傳回的其他錯誤訊息資訊。  
  
### <a name="to-resolve-this-problem"></a>若要解決這個問題：  
* 將 `SendUsing` Rsreportserver.config **檔案中的** 元素的值設為 1。  
* 清除 `SMTPServer` 屬性的值，使其空白。 您也需要提供 `SMTPServerPickupDirectory` 屬性的值。   
  
如需有關將本機 SMTP 服務用於報表之電子郵件傳遞的詳細資訊，請參閱＜設定報表伺服器的電子郵件傳遞＞。  
  
## <a name="failure-sending-mail-the-server-rejected-the-sender-address-the-server-response-was-454-573-client-does-not-have-permission-to-submit-mail-to-this-server"></a>傳送郵件失敗：伺服器拒絕寄件者地址。 伺服器回應為：454 5.7.3 用戶端沒有提交郵件到此伺服器的權限  
當 SMTP 伺服器上的安全性原則設定只允許已驗證的使用者提交郵件以進行後續的傳遞時，會發生此錯誤。 如果 SMTP 伺服器不接受匿名使用者的電子郵件提交，請向系統管理員洽詢有關取得伺服器使用權限的事宜。  
> 當您指定 Exchange 伺服器名稱做為 SMTPServer 時，會發生此錯誤。 若要使用 Exchange 伺服器傳遞電子郵件，必須指定為 Exchange 伺服器設定的 SMTP 閘道名稱。 請向您的 Exchange 管理員洽詢此資訊。  
  
## <a name="subscriptions-are-not-processing"></a>無法處理訂閱  
在這些狀況下，訂閱可能失敗。   
* 用來觸發報表的排程已經過期。 針對會觸發報表快照集更新的訂閱，用來重新整理快照集的排程可能已經過期。  
  
* 報表伺服器、SQL Server Agent 或電子郵件伺服器應用程式未在執行中。  
* 無法傳遞報表 (例如報表過大)。 若要判斷傳遞失敗是否因為報表太大，請將報表儲存為檔案，然後以電子郵件傳送它。 請務必選擇您在訂閱中指定的相同轉譯格式。 如果您看到傳遞錯誤，請使用「檔案共用」傳遞延伸模組，而不要使用報表伺服器電子郵件。  
* 用於檔案共用傳遞的電腦並未執行，或者檔案共用設定為唯讀存取。  
* 已經解除安裝或停用訂閱中指定的傳遞延伸模組。  
* 將認證設定從預存變更為整合或提示的值。  
* 報表定義中的參數名稱或資料類型已變更，並且已經重新發行報表。 如果訂閱包括已不再有效的參數，則訂閱會變成非使用中。  
  
如需詳細資訊，請參閱 TechNet Wiki [Troubleshoot issues and errors with Reporting Services](http://social.technet.microsoft.com/wiki/contents/articles/1633.ssrs-troubleshoot-issues-and-errors-with-reporting-services.aspx)(針對 Reporting Services 的問題和錯誤進行疑難排解)。  
  
  
    
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

