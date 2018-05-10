---
title: ReportingServicesService 設定檔 | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [Reporting Services]
- Report Server Windows service, ReportingServicesService configuration file
- ReportingServicesService configuration file
ms.assetid: 40f4a401-cb61-4c42-b1ec-01acdacdacd1
caps.latest.revision: 41
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 071650750724cf8a58c4ac6377f9e2b1f635fe12
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="reportingservicesservice-configuration-file"></a>ReportingServicesService 組態檔
 ||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SQL Server 2016|
  
ReportingServicesService.exe.config 檔包括設定追蹤的設定。  
  
## <a name="file-location"></a>檔案位置  
 此檔案位於 \Reporting Services\Report Server\Bin 資料夾中。  
  
## <a name="editing-guidelines"></a>編輯指導方針  
 您可以修改此檔案以重新命名記錄檔，或者增加或減少追蹤層級。 請勿修改其他任何設定。 如需指示，請參閱[修改 Reporting Services 設定檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。 如需追蹤紀錄的詳細資訊，請參閱 [報表伺服器服務追蹤記錄](../../reporting-services/report-server/report-server-service-trace-log.md)。  
  
## <a name="example-configuration"></a>範例組態  
 下列範例顯示 ReportingServicesService.exe.config 檔中的設定和預設值。  
  
```  
<configSections>  
      <section name="RStrace" type="Microsoft.ReportingServices.Diagnostics.RSTraceSectionHandler,Microsoft.ReportingServices.Diagnostics" />  
</configSections>  
\<system.diagnostics>  
      <switches>  
          <add name="DefaultTraceSwitch" value="3" />  
      </switches>  
\</system.diagnostics>  
<RStrace>  
      <add name="FileName" value="ReportServerService_" />  
      <add name="FileSizeLimitMb" value="32" />  
      <add name="KeepFilesForDays" value="14" />  
      <add name="Prefix" value="tid, time" />  
      <add name="TraceListeners" value="debugwindow, file" />  
      <add name="TraceFileMode" value="unique" />  
      <add name="Components" value="all" />  
</RStrace>  
<runtime>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
             <dependentAssembly>  
                    <assemblyIdentity name="Microsoft.ReportingServices.Interfaces"  
                        publicKeyToken="89845dcd8080cc91"  
                        culture="neutral" />  
                    <bindingRedirect oldVersion="8.0.242.0"  
                                     newVersion="10.0.0.0"/>  
                    <bindingRedirect oldVersion="9.0.242.0"  
                                     newVersion="10.0.0.0"/>  
             </dependentAssembly>  
      </assemblyBinding>  
      <gcServer enabled="true" />  
</runtime>  
```  
  
## <a name="configuration-settings"></a>組態設定  
 下表提供有關特定設定的資訊。 設定會依其出現在組態檔的順序顯示。  
  
|設定|描述|  
|-------------|-----------------|  
|**RStrace**|指定用於錯誤和追蹤的命名空間。|  
|**DefaultTraceSwitch**|指定報告到 ReportServerService 追蹤記錄的資訊層級。 每一個層級包括所有較低層級所報告的資訊。 不建議停用追蹤。 有效值包括：<br /><br /> 0= 停用追蹤<br /><br /> 1= 例外狀況和重新啟動<br /><br /> 2= 例外、重新啟動和警告<br /><br /> 3= 例外、重新啟動、警告和狀態訊息 (預設值)<br /><br /> 4= 詳細資訊模式|  
|**FileName**|指定記錄檔名稱的第一部分。 **Prefix** 所指定的值會完成名稱的其餘部分。 依預設，名稱是 ReportServerService_。|  
|**FileSizeLimitMb**|指定追蹤記錄的大小上限。 檔案大小的單位為 MB。 有效值為 0 到最大整數。 預設值為 32。|  
|**KeepFilesForDays**|指定一個天數，超過此天數後，追蹤記錄檔便會被刪除。 有效值為 0 到最大整數。 預設值為 14。|  
|**Prefix**|指定可區別記錄檔執行個體的產生值。 依預設，會將時間戳記附加至追蹤記錄檔名稱。 此值設定為 "tid, time"。 請勿修改此設定。|  
|**TraceListeners**|指定輸出追蹤記錄內容的目標。 您可以指定多重目標，每個目標之間請以逗號隔開。 有效值包括：<br /><br /> DebugWindow (預設值)<br /><br /> File (預設值)<br /><br /> StdOut|  
|**TraceFileMode**|指定追蹤記錄中是否要包含 24 小時內的資料。 每個元件每一天只能有一份追蹤記錄。 此值設定為「Unique (預設值)」。 請勿修改此值。|  
|**Components**|指定建立追蹤記錄的元件。 預設值是 **all**秒。 此設定的其他有效值包括內部元件的名稱。 請勿修改此值。|  
|**執行階段**|指定支援與前版回溯相容的組態設定。 執行階段設定是用來重新導向以新版為前版 Microsoft.ReportingServices.Interfaces 之目標的要求。<br /><br /> 本節中的所有組態設定會在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 產品文件集中加以描述。 如需詳細資訊，請在 MSDN 網站上或 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 文件集中搜尋「執行階段結構描述設定」。|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態檔](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [報表伺服器服務追蹤記錄](../../reporting-services/report-server/report-server-service-trace-log.md)  
  
  
