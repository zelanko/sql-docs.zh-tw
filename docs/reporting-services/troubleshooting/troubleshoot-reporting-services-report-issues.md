---
title: 針對 Reporting Services 報表問題進行疑難排解 | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: troubleshooting
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a705d103-85b1-49b5-b27f-332b1040d029
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: cb93c59cec663a99ebc0460d948f4c2bd0a78f94
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot--reporting-services-report-issues"></a>針對 Reporting Services 報表問題進行疑難排解
本主題可協助您對下列問題進行疑難排解： [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] 報表設計、預覽報表、以原生模式或 SharePoint 模式將報表發行至報表伺服器、在報表伺服器上檢視報表，或是將報表匯出為不同的檔案格式。  
## <a name="monitor-report-servers"></a>監視報表伺服器  
您可以使用系統和資料庫工具來監視報表伺服器活動。 您也可以檢視報表伺服器追蹤記錄檔，或是查詢報表伺服器執行記錄，以找出有關特定報表的詳細資訊。 如果您正在使用效能監視器，您可以針對報表伺服器 Web 服務和 Windows 服務加入效能計數器，以識別視需要或排程處理中的瓶頸。  
如需詳細資訊，請參閱 [監視報表伺服器效能](../../reporting-services/report-server/monitoring-report-server-performance.md)。  
  
  
## <a name="view-the-report-server-logs"></a>檢視報表伺服器記錄  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] 會將許多內部與外部事件記錄到記錄檔中，其中包含特定報表的資料、偵錯資訊、HTTP 要求與回應，以及報表伺服器事件。 您也可以建立效能記錄，然後選擇效能計數器來指定要收集的資料。 預設安裝記錄檔的預設目錄是 `<drive>\Program Files\Microsoft SQL Server\MSRS130.MSSQLSERVER\Reporting Services\LogFiles`。   
  
如需詳細資訊，請參閱 [Reporting Services 記錄檔和來源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
若要明確判斷報表等待時間是花在資料擷取、報表處理或報表轉譯，請使用執行記錄。 如需詳細資訊，請參閱 [報表伺服器 ExecutionLog 和 ExecutionLog3 檢視]。   
  
## <a name="view-the-call-stack-for-report-processing-error-messages-on-the-report-server"></a>在報表伺服器上檢視報表處理錯誤訊息的呼叫堆疊  
在報表管理員中檢視已發行的報表時，可能會出現代表一般處理或轉譯錯誤的錯誤訊息。 若要查看詳細資訊，您可以檢視呼叫堆疊。   
  
請使用本機管理員認證登入報表伺服器，然後以滑鼠右鍵按一下 [報表管理員] 頁面，再按一下 [檢視來源]，即可檢視呼叫堆疊。 呼叫堆疊會提供錯誤訊息的詳細內容。  
  
## <a name="use-includessmanstudiofullincludesssmanstudiofullmd-to-verify-queries-and-credentials"></a>使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull.md)] 驗證查詢和認證  
將複雜查詢加入報表之前，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull.md)] 驗證複雜查詢。   
  
如需詳細資訊，請參閱 [Database Engine 查詢編輯器](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md) 和 [使用物件總管管理物件](~/ssms/object/manage-objects-by-using-object-explorer.md)。  
  
## <a name="analyze-problem-reports-with-report-data-cached-on-the-client"></a>使用在用戶端上快取的報表資料分析問題報表  
當報表作者在 Business Intelligence Development Studio 中建立報表時，撰寫用戶端會將資料快取為 .rdl.data 檔案，供您預覽報表時使用。 每當查詢變更時，快取也會隨之更新。 若要對報表問題進行偵錯，設定不要重新整理報表資料可能會很有用，因為這樣可以避免資料在偵錯期間發生變更。   
  
若要控制 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)] 是否只能使用快取資料，請將下列區段加入 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio.md)]的 devenv.exe.config 中。 預設目錄的位置為： `<drive>:Program Files\Microsoft Visual Studio 10.0\Common7\IDE`。   
  
```  
<system.diagnostics>  
      <switches>  
         <add name="Microsoft.ReportDesigner.ReportPreviewStore.ForceCache" value="1" />  
      </switches>  
   </system.diagnostics>  
```  
只要將值設為 1，就只會使用快取報表資料。 當您完成報表偵錯時，請務必移除這段程式碼。  
  
## <a name="see-also"></a>另請參閱  
[錯誤和事件 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


