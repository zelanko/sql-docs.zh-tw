---
title: 報表伺服器服務追蹤記錄 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- logs [Reporting Services], trace
- traces [Reporting Services]
- system information [Reporting Services]
- versions [Reporting Services]
ms.assetid: 2fde08b2-137d-4f4b-88e5-216030216e0d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d69b2a3eeb28d5fe23eb6674c8a0ca0ee7628a75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103413"
---
# <a name="report-server-service-trace-log"></a>報表伺服器服務追蹤記錄
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表伺服器追蹤記錄為 ASCII 文字檔案，包含報表伺服器服務作業的詳細資訊，包括報表伺服器 Web 服務、報表管理員及背景處理所執行的作業。 追蹤記錄檔包括已記錄於其他記錄檔的重複資訊，加上別處所沒有的其他資訊。 如果您要偵錯包含報表伺服器的應用程式，或者調查寫入事件記錄或執行記錄的特定問題，追蹤記錄資訊可能會很有用。  
  
> [!NOTE]  
>  在先前的版本中，系統提供了多個追蹤記錄檔 (每個應用程式都有一個檔案)。 下列檔案已過時，在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和之後的版本中不會再建立：ReportServerWebApp_ *\<時間戳記 >* .log、 ReportServer_ *\<時間戳記 >* .log 和 ReportServerService_main_ *\<時間戳記 >* 。 記錄檔。  
  
 **本主題內容：**  
  
-   [所在的報表伺服器記錄檔？](#bkmk_view_log)  
  
-   [追蹤組態設定](#bkmk_trace_configuration_settings)  
  
-   [新增自訂組態設定來指定傾印檔位置](#bkmk_add_custom)  
  
-   [記錄檔欄位](#bkmk_log_file_fields)  
  
##  <a name="bkmk_view_log"></a> 報表伺服器記錄檔在何處？  
 追蹤記錄檔為 `ReportServerService_<timestamp>.log` ，位於下列資料夾：  
  
 `C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles`  
  
 系統每天都會建立追蹤記錄，從午夜過後 (當地時間) 發生的第一個項目，以及每次服務重新啟動時開始。 此時間戳記是以國際標準時間 (UTC) 為基礎。 此檔案採用 EN-US 格式。 追蹤記錄檔的預設大小上限為 32 MB，且預設會在 14 天後刪除。  
  
 觀看示範如何使用 Microsoft Power Query 檢視 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 記錄檔的短片。  
  
 ![檢視有關 Power Query 和 SSRS 記錄檔的影片](../media/generic-video-thumbnail.png "檢視有關 Power Query 和 SSRS 記錄檔的影片")  
  
##  <a name="bkmk_trace_configuration_settings"></a> 追蹤組態設定  
 追蹤記錄檔的行為在組態檔 **ReportingServicesrService.exe.config**中管理。下列資料夾路徑中可找到組態檔：  
  
 `\Program Files\Microsoft SQL Server\MSRS12.<instance name>\Reporting Services\ReportServer\bin`.  
  
 下列範例說明 `RStrace` 設定的 XML 結構。 `DefaultTraceSwitch` 的值會決定要將哪種資訊新增到記錄。 除了 `Components` 屬性外，`RStrace` 的值在所有組態檔中都相同。  
  
```  
<system.diagnostics>  
      <switches>  
          <add name="DefaultTraceSwitch" value="3" />  
      </switches>  
</system.diagnostics>  
<RStrace>  
      <add name="FileName" value="ReportServerService_" />  
      <add name="FileSizeLimitMb" value="32" />  
      <add name="KeepFilesForDays" value="14" />  
      <add name="Prefix" value="tid, time" />  
      <add name="TraceListeners" value="file" />  
      <add name="TraceFileMode" value="unique" />  
      <add name="Components" value="all" />  
</RStrace>  
```  
  
 下表提供有關各項設定的資訊。  
  
|設定|描述|  
|-------------|-----------------|  
|`RStrace`|指定用於錯誤和追蹤的命名空間。|  
|`DefaultTraceSwitch`|指定報告到 ReportServerService 追蹤記錄的資訊層級。 每一個層級包括所有較低層級所報告的資訊。 不建議停用追蹤。 有效值為：<br /><br /> 0= 停用追蹤。 ReportServerService 記錄檔是預設為啟用。 若要關閉，請將追蹤層級設定為 0。<br /><br /> 1= 例外狀況和重新啟動<br /><br /> 2= 例外、重新啟動和警告<br /><br /> 3= 例外、重新啟動、警告和狀態訊息 (預設值)<br /><br /> 4= 詳細資訊模式|  
|**FileName**|指定記錄檔名稱的第一部分。 `Prefix` 所指定的值會完成名稱的其餘部分。|  
|**FileSizeLimitMb**|指定追蹤記錄的大小上限。 檔案大小的單位為 MB。 有效值為 0 到最大整數。 預設值為 32。 如果指定 0 或負數，報表伺服器會將該值視為 1。<br /><br /> 藉由設定追蹤層級 (0 到 4) 來控制記錄的內容多寡，便可以控制檔案大小。 您也可以指定要追蹤的元件。 如果在 14 天的到期日之前就已經到達記錄檔上限，將會以較新的項目取代較舊的項目。|  
|**KeepFilesForDays**|指定一個天數，超過此天數後，追蹤記錄檔便會被刪除。 有效值為 0 到最大整數。 預設值為 14。 如果指定 0 或負數，報表伺服器會將該值視為 1。|  
|`Prefix`|指定可區別記錄檔執行個體的產生值。 依預設，會將時間戳記附加至追蹤記錄檔名稱。 此值設定為 "tid, time"。 請勿修改此設定。|  
|**TraceListeners**|指定輸出追蹤記錄內容的目標。 您可以指定多重目標，每個目標之間請以逗號隔開。 有效值為：<br /><br /> DebugWindow<br /><br /> File (預設值)<br /><br /> StdOut|  
|**TraceFileMode**|指定追蹤記錄中是否要包含 24 小時內的資料。 每個元件每一天只能有一份追蹤記錄。 此值設定為「Unique (預設值)」。 請勿修改此值。|  
|`Components`|使用下列格式來指定要產生追蹤記錄資訊的元件以及追蹤層級：<br /><br /> \<元件類別>:\<追蹤層級><br /><br /> 元件類別可設定為：<br />`All` 用於針對所有不屬於特定類別的程序，追蹤其一般報表伺服器活動。<br />`RunningJobs` 用於追蹤進行中報表或訂閱作業。<br />`SemanticQueryEngine` 用於追蹤語意查詢，語意查詢會在使用者對以模型為基礎的報表執行隨選資料瀏覽時處理。<br />`SemanticModelGenerator` 用於追蹤模型產生。<br />`http` 是用於啟用報表伺服器 HTTP 記錄檔。 如需詳細資訊，請參閱＜ [Report Server HTTP Log](report-server-http-log.md)＞。<br /><br /> <br /><br /> 追蹤層級的有效值包括：<br /><br /> 0= 停用追蹤<br /><br /> 1= 例外狀況和重新啟動<br /><br /> 2= 例外、重新啟動和警告<br /><br /> 3= 例外、重新啟動、警告和狀態訊息 (預設值)<br /><br /> 4= 詳細資訊模式<br /><br /> 報表伺服器的預設值是："all:3"。<br /><br /> 您可以指定全部或部分元件 (`all`、`RunningJobs`、`SemanticQueryEngine`、`SemanticModelGenerator`)。 如果不要產生特定元件的資訊，可以停用該元件的追蹤 (例如 "SemanticModelGenerator:0")。 請不要停用 `all` 的追蹤。<br /><br /> 如果您沒有將追蹤層級附加至元件，就會使用針對 `DefaultTraceSwitch` 所指定的值。 例如，如果指定 "all,RunningJobs,SemanticQueryEngine,SemanticModelGenerator"，所有元件都會使用預設追蹤層級。<br /><br /> 如果要檢視為每個語意查詢產生的 Transact-SQL 陳述式，您可以設定 "SemanticQueryEngine:4"。 Transact-SQL 陳述式就會記錄在追蹤記錄中。 下列範例說明將 Transact-SQL 陳述式加入記錄的組態設定：<br /><br /> \<add name="元件" value="all,SemanticQueryEngine:4" />|  
  
##  <a name="bkmk_add_custom"></a> 新增自訂組態設定來指定傾印檔位置  
 您可以新增自訂設定，來設定 Windows 的 Dr. Watson for Windows 工具用於儲存傾印檔案。 自訂設定為 `Directory`。 下列範例說明如何在 `RStrace` 區段中指定這個組態設定：  
  
```  
<add name="Directory" value="U:\logs\" />  
```  
  
 如需詳細資訊，請參閱 [網站上的](https://support.microsoft.com/?kbid=913046) 知識庫文件 913046 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
##  <a name="bkmk_log_file_fields"></a> 記錄檔欄位  
 您可以在追蹤記錄中找到下列欄位：  
  
-   系統資訊，包括作業系統、版本、處理器數量及記憶體。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 元件和版本資訊。  
  
-   應用程式記錄檔的事件記錄。  
  
-   報表伺服器所產生的例外狀況。  
  
-   報表伺服器所記錄的低資源警示。  
  
-   輸入 SOAP Envelope 和摘要輸出 SOAP Envelope。  
  
-   HTTP 標頭、堆疊追蹤和偵錯追蹤資訊。  
  
 您可以檢閱追蹤記錄資訊，以便判斷是否發生報表傳遞、誰接收到報表以及嘗試傳遞了幾次。 追蹤記錄也會記錄報表執行活動，以及報表處理期間有作用的環境變數。 錯誤和例外狀況也會輸入到追蹤記錄中。 例如，您可能會發現報表逾時錯誤 (指定為 `ThreadAbortExceptions` 項目)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 記錄檔和來源](../report-server/reporting-services-log-files-and-sources.md)   
 [錯誤和事件參考 &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
