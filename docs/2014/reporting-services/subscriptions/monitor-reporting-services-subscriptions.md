---
title: 監視 Reporting Services 訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], inactive
- subscriptions [Reporting Services], status
- monitoring [Reporting Services], subscriptions
- status information [Reporting Services]
- inactive subscriptions [Reporting Services]
ms.assetid: 054c4a87-60bf-4556-9a8c-8b2d77a534e6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 998a7823721b8c978e2b8bfd21b6308507a8963c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100755"
---
# <a name="monitor-reporting-services-subscriptions"></a>監視 Reporting Services 訂閱
  您可以透過使用者介面、Windows PowerShell 或記錄檔來監視 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱。 您可以使用的監視選項取決於正在執行的報表伺服器模式。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; SharePoint 模式|  
  
 **本主題內容：**  
  
-   [原生模式使用者介面](#bkmk_native_mode)  
  
-   [SharePoint 模式](#bkmk_sharepoint_mode)  
  
-   [使用 PowerShell 監視訂閱](#bkmk_use_powershell)  
  
-   [管理非使用中訂閱](#bkmk_manage_inactive)  
  
##  <a name="bkmk_native_mode"></a>原生模式使用者介面  
 個別 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用者可以使用 [我的訂閱] **** 頁面或報表管理員中的 [訂閱] **** 索引標籤，來監視訂閱的狀態。 [訂閱] 頁面會包括資料行，指出上次訂閱是在何時執行以及報表的狀態。 當訂閱已設定處理排程時，就會更新狀態訊息。 如果觸發程序從未發生 (例如，報表執行快照集從未重新整理或排程從未執行)，則狀態訊息不會更新。  
  
 下表描述 [狀態] **** 欄的可能值。  
  
|狀態|描述|  
|------------|-----------------|  
|新的訂用帳戶|出現在第一次建立訂閱時。|  
|非使用中|出現在無法處理訂閱時。 如需詳細資訊，請參閱此主題稍後的＜管理非使用中訂閱＞。|  
|完成：已處理 \<數目**> 個 (總共 \<數目**> 個)；\<數目**> 個錯誤。|顯示資料驅動訂閱執行的狀態；此訊息來自排程與傳遞處理器。|  
|\<已處理>*數目*|排程與傳遞處理器已成功傳遞或已不再嘗試傳遞的通知數目。 當資料驅動傳遞完成時，已處理的通知數目應該和產生的通知總數相等。|  
|\<> 總計*數*|訂閱最後一次傳遞所產生的通知總數。|  
|\<> 錯誤*數目*|排程與傳遞處理器無法傳遞或已不再嘗試傳遞的通知數目。|  
|傳送郵件失敗：傳輸無法連接到伺服器。|指出報表伺服器未連接到郵件伺服器；此訊息來自電子郵件傳遞延伸模組。|  
|檔案 \<檔案名稱**> 已寫入 \<路徑>。|指出已成功傳遞到檔案共用位置；此訊息來自檔案共用傳遞延伸模組。|  
|寫入檔案時發生未知的錯誤。|指出未成功傳遞到檔案共用位置；此訊息來自檔案共用傳遞延伸模組。|  
|無法連線到目的資料夾，\<路徑>。 請確認目的資料夾或檔案共用存在。|指出找不到所指定的資料夾；此訊息來自檔案共用傳遞延伸模組。|  
|檔案 \<檔案名稱> 無法寫入 \<路徑>。 正在嘗試重試。|指出無法以較新版本進行檔案更新；此訊息來自檔案共用傳遞延伸模組。|  
|無法寫入檔案 \<檔案名稱>：\<訊息>|指出未成功傳遞到檔案共用位置；此訊息來自檔案共用傳遞延伸模組。|  
|
  \<自訂狀態訊息>|關於傳遞成功與傳遞失敗的狀態訊息，是由傳遞延伸模組所提供。 如果您使用協力廠商或自訂傳遞延伸模組，就可能會提供其他的狀態訊息。|  
  
 報表伺服器管理員也可以監視目前正在處理的標準訂閱。 無法監視資料驅動訂閱。 如需詳細資訊，請參閱[管理執行中的進程](manage-a-running-process.md)。  
  
 如果無法傳遞訂閱 (例如，若郵件伺服器無法使用)，傳遞延伸模組就會重試傳遞。 組態設定會指定嘗試傳遞的次數。 預設值為不重試。 在某些情況下，報表可能會在無資料狀況下處理 (例如，若資料來源為離線)，此時，訊息內文將會說明此一狀況。  
  
### <a name="native-mode-log-files"></a>原生模式記錄檔  
 如果在傳遞期間發生錯誤，就會在報表伺服器追蹤記錄中產生項目。  
  
 報表伺服器管理員可以查看**reportserverservice_\*.log**檔，以判斷訂閱傳遞狀態。 針對電子郵件傳遞，報表伺服器記錄檔會包括處理以及傳遞到特定電子郵件帳戶的記錄。 下列是記錄檔的預設位置：  
  
 `C:\Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\LogFiles`  
  
 下列是範例記錄檔檔名：  
  
 `ReportServerService__05_21_2014_00_05_07.log`  
  
 下列是與訂閱相關的追蹤記錄檔範例錯誤訊息：  
  
-   library!WindowsService_7!b60!05/20/2014-22:34:36:: i INFO: 將 EnableExecutionLogging 初始化至 'True'  如同 Server 系統所示 properties.emailextension!WindowsService_7!b60!05/20/2014-22:34:41:: e ERROR: **傳送電子郵件時發生錯誤**。 例外狀況：System.Net.Mail.SmtpException: SMTP 伺服器需要安全的連線或是用戶端未經認證。 伺服器回應為：5.7.1 用戶端未經認證   於 System.Net.Mail.MailCommand.CheckResponse(SmtpStatusCode statusCode, String response)  
  
 記錄檔不包括有關報表是否開啟或實際上是否成功傳遞的資訊。 成功傳遞是指排程與傳遞處理器未產生錯誤，且報表伺服器已連接到郵件伺服器。 如果電子郵件在使用者信箱產生無法傳遞訊息錯誤，該資訊將不會包含在記錄檔中。 如需記錄檔的詳細資訊，請參閱 [Reporting Services 記錄檔和來源](../report-server/reporting-services-log-files-and-sources.md)。  
  
##  <a name="bkmk_sharepoint_mode"></a>SharePoint 模式  
 在 SharePoint 模式中監視訂閱：可從 [管理訂閱] **** 頁面監視訂閱狀態。  
  
1.  瀏覽至包含報表的文件庫  
  
2.  開啟報表的內容功能表 (**…**)。  
  
3.  選取展開的功能表選項 (**…**)。  
  
4.  選取 [管理訂閱] ****  
  
### <a name="sharepoint-uls-log-files"></a>SharePoint ULS 記錄檔  
 寫入 SharePoint ULS 記錄檔的訂閱相關資訊。 如需設定 ULS 記錄檔之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 事件的詳細資訊，請參閱[開啟 SharePoint 追蹤記錄的 Reporting Services 事件 &#40;ULS&#41;](../report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)。  下列是與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱相關的範例 ULS 記錄檔項目。  
  
||||||||  
|-|-|-|-|-|-|-|  
|Date|處理程序|區域|類別|層級|Correlation|訊息|  
|5/21/2014 14:34:06:15|應用程式集區：a0ba039332294f40bc4a81544afde01d|SQL Server Reporting Services|報表伺服器電子郵件延伸模組|未預期|(空白)|**傳送電子郵件時發生錯誤。** 例外狀況：System.net.mail.smtpexception: 信箱無法使用。 伺服器回應為：5.7.1 用戶端不具權限，無法以此寄件者傳送  於 System.Net.Mail.DataStopCommand.CheckResponse(SmtpStatusCode statusCode, String serverResponse)  於 System.Net.Mail.DataStopCommand.Send(SmtpConnection conn)  於 System.Net.Mail.SmtpClient.Send(MailMessage message)  於 Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider.Deliver(Notification notification)|  
  
##  <a name="bkmk_use_powershell"></a>使用 PowerShell 監視訂閱  
 例如，您可以使用 PowerShell 指令碼查看原生模式或 SharePoint 模式訂閱的狀態，請參閱 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](manage-subscription-owners-and-run-subscription-powershell.md)。  
  
##  <a name="bkmk_manage_inactive"></a>管理非使用中訂閱  
 如果訂閱變成非使用中，您應該將其刪除，或藉由解決導致無法處理的問題將其重新啟動。 如果發生問題而導致無法處理，訂閱就可能會變成非使用中。 這些條件包括：  
  
-   移除或解除安裝訂閱中所指定的傳遞延伸模組。  
  
-   將認證設定從儲存變更為整合或提示值。  
  
-   變更報表定義中的參數名稱或資料類型，然後重新發行報表。 如果訂閱包括已不再有效的參數，則訂閱會變成非使用中。  
  
-   變更報表的執行模式 (例如，修改視需要產生的報表，使其以報表執行快照集執行)。 如需詳細資訊，請參閱 [設定報表處理屬性](../report-server/set-report-processing-properties.md)。  
  
 非使用中訂閱是由訂閱本身的訊息指出。 訊息包括有關原因和重新啟動訂閱所應採取之步驟的資訊。  
  
 當條件導致訂閱變成非使用中，而報表伺服器執行訂閱時，該訂閱會反映出此事實。 如果訂閱已排程在每星期五的上午 2:00 傳遞報表，而其使用的傳遞延伸模組在星期一的上午 9:00 解除安裝，則直到星期五的上午 2:00，訂閱才會反映出其非使用中的狀態。  
  
## <a name="see-also"></a>另請參閱  
 [建立和管理原生模式報表伺服器的訂閱](../create-manage-subscriptions-native-mode-report-servers.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)  
  
  
