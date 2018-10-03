---
title: 報表伺服器 HTTP 記錄 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- HTTP [Reporting Services]
ms.assetid: 6cc433b7-165c-4b16-9034-79256dd6735f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6b990f4a2dbf321b20d9d8e45ecf13b3ede47987
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147868"
---
# <a name="report-server-http-log"></a>報表伺服器 HTTP 記錄
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器 HTTP 記錄檔會保留報表伺服器所處理之每個 HTTP 要求與回應的記錄。 由於要求溢位和逾時錯誤不會送達報表伺服器，因此它們不會記錄在記錄檔中。  
  
 HTTP 記錄預設是不啟用的。 若要啟用 HTTP 記錄，請修改 **ReportingServicesService.exe.config** 組態檔，以在安裝中使用這項功能。  
  
## <a name="viewing-log-information"></a>檢視記錄資訊  
 此記錄是 ASCII 文字檔。 您可以使用任何文字編輯器來檢視此檔案。 報表伺服器 HTTP 記錄檔相當於 IIS 中的 W3C 記錄擴充檔而且使用類似的欄位，因此您可以使用現有的 IIS 記錄檔檢視器來讀取報表伺服器 HTTP 記錄檔。 下表提供有關 HTTP 記錄檔的其他資訊：  
  
|||  
|-|-|  
|**檔案名稱**|根據預設，記錄檔名稱為<br /><br /> `ReportServerService_HTTP_<timestamp>.log.`<br /><br /> 您可以透過在 ReportingServicesService.exe.config 檔中修改 HttpTraceFileName 屬性，自訂檔案名稱的前置詞。 此時間戳記是以國際標準時間 (UTC) 為基礎。|  
|**檔案位置**|檔案會寫入下列位置：<br /><br /> `\Microsoft SQL Server\<SQL Server Instance>\Reporting Services\LogFiles`|  
|**檔案格式**|此檔案採用 EN-US 格式。 它是 ASCII 文字檔。|  
|**檔案建立和保留**|當您在組態檔中啟用 HTTP 記錄、重新啟動此服務，然後報表伺服器處理 HTTP 要求之後，系統就會建立 HTTP 記錄。 如果您設定了這些設定，但卻沒有看見記錄檔，請開啟報表或啟動報表伺服器應用程式 (例如「報表管理員」) 來產生 HTTP 要求，以便建立此檔案。<br /><br /> 記錄檔的新執行個體會在報表伺服器的每個服務重新啟動和後續 HTTP 要求之後建立。<br /><br /> 根據預設，追蹤記錄的上限為 32 MB，並且會在 14 天之後遭到刪除。|  
  
## <a name="configuration-settings-for-report-server-http-log"></a>設定報表伺服器 HTTP 記錄的設定  
 若要設定報表伺服器 HTTP 記錄，請使用 [記事本] 來修改 **ReportingServicesService.exe.config** 檔。 此組態檔位於 \Program Files\Microsoft SQL Server\MSSQL.n\Reporting Services\ReportServer\Bin 資料夾中。  
  
 若要啟用 HTTP 伺服器，請將 `http:4` 加入 ReportingServicesService.exe.config 檔的 RStrace 區段。 所有其他 HTTP 記錄檔項目是選擇性的。 下列範例包含所有設定，因此您可以將整個區段貼入 RStrace 區段，然後刪除不需要的設定。  
  
```  
   <RStrace>  
         <add name="FileName" value="ReportServerService_" />  
         <add name="FileSizeLimitMb" value="32" />  
         <add name="KeepFilesForDays" value="14" />  
         <add name="Prefix" value="tid, time" />  
         <add name="TraceListeners" value="debugwindow, file" />  
         <add name="TraceFileMode" value="unique" />  
         <add name="HttpTraceFileName" value="ReportServerService_HTTP_" />  
         <add name="HttpTraceSwitches" value="date,time, clientip,username,serverip,serverport,host,method,uristem,uriquery,protocolstatus,bytesreceived,timetaken,protocolversion,useragent,cookiereceived,cookiesent,referrer" />  
         <add name="Components" value="all:3,http:4" />  
   </RStrace>  
```  
  
## <a name="log-file-fields"></a>記錄檔欄位  
 下表將描述記錄中提供的欄位。 此欄位清單是可設定;您可以指定要透過包含的欄位`HTTPTraceSwitches`組態設定。 **預設**資料行可讓您指定是否欄位會包含在記錄檔自動是否您未指定`HTTPTraceSwitches`。  
  
|欄位|描述|預設|  
|-----------|-----------------|-------------|  
|HttpTraceFileName|此為選擇性的值。 預設值為 ReportServerServiceHTTP_。 如果您想要使用不同的檔案命名慣例 (例如，當您要將記錄檔儲存至集中位置時，若要包含伺服器名稱)，可以指定不同的值。|是|  
|HTTPTraceSwitches|此為選擇性的值。 如果您指定了此欄位，就可以使用逗號分隔的格式來設定記錄檔中使用的欄位。|否|  
|date|活動發生的日期。|否|  
|Time|活動發生的時間。|否|  
|ClientIp|存取報表伺服器之用戶端的 IP 位址。|是|  
|UserName|存取報表伺服器之使用者的名稱。|否|  
|ServerPort|用於連接的通訊埠編號。|否|  
|Host|主機標頭的內容。|否|  
|方法|從用戶端呼叫的動作或 SOAP 方法。|是|  
|UriStem|存取的資源。|是|  
|UriQuery|用來存取資源的查詢。|否|  
|ProtocolStatus|HTTP 狀態碼。|是|  
|BytesReceived|伺服器所接收的位元組數目。|否|  
|TimeTaken|從 HTTP.SYS 傳回要求資料的那一刻，直到伺服器完成最後一個傳送作業為止的時間 (以毫秒為單位)，但不包括網路傳輸時間。|否|  
|ProtocolVersion|用戶端所使用的通訊協定版本。|否|  
|UserAgent|用戶端所使用的瀏覽器類型。|否|  
|CookieReceived|伺服器所接收的 Cookie 內容。|否|  
|CookieSent|伺服器所傳送的 Cookie 內容。|否|  
|Referrer|用戶端造訪的上一個網站。|否|  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器服務追蹤記錄](report-server-service-trace-log.md)   
 [Reporting Services 記錄檔和來源](../report-server/reporting-services-log-files-and-sources.md)   
 [錯誤和事件參考&#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
