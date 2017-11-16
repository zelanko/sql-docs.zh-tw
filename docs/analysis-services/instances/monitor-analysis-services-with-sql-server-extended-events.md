---
title: "監視 Analysis Services with SQL Server 擴充事件 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- XEvents
- Sql13.ssms.XeASNewEventSession.General.f1
- Sql13.ssms.XeASNewEventSession.Events.f1
- Sql13.ssms.XeASNewEventSession.Targets.f1
- Sql13.ssms.XeASNewEventSession.Advanced.f1
ms.assetid: b57cc2fe-52dc-4fa9-8554-5a866e25c6d7
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cec6da660c202dfde5a1169dd34397fca5c51207
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="monitor-analysis-services-with-sql-server-extended-events"></a>使用 SQL Server 擴充事件監視 Analysis Services
  擴充事件 (*xEvent*) 是輕量型追蹤和效能監視系統，其使用的系統資源非常少，因此可成為在生產與測試伺服器上用來診斷問題的理想工具。 它也具備高擴充性且可設定，而且在 SQL Server 2016 中，可以更輕鬆地透過新的內建工具支援來使用。 在 SQL Server Management Studio 中與 Analysis Services 執行個體的連接上，您可以設定、執行和監視即時追蹤，類似於使用 SQL Server Profiler。 增加更好的工具應該能夠讓 xEvents 更合理地成為 SQL Server Profiler 的取代項目，並且在診斷資料庫引擎和 Analysis Services 工作負載的問題方式中建立更多的對稱。  
  
 除了 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，您也可以透過 XMLA 指令碼，使用舊方法來設定  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 擴充事件工作階段 (如同舊版本中所支援)。  
  
 您可以擷取所有的 Analysis Services 事件，並將特定取用者設為目標，如 [擴充事件](../../relational-databases/extended-events/extended-events.md)中所定義。  
  
> [!NOTE]  
>  觀賞這段 [快速的影片介紹](https://www.youtube.com/watch?v=ja2mOHWRVC0&index=1&list=PLv2BtOtLblH1YvzQ5YnjfQFr_oKEvMk19) 或讀取 [支援的部落格文章](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx) ，以深入了解 SQL Server 2016 中 Analysis Services 的 xEvent。  
  
##  <a name="bkmk_top"></a> 本主題內容  
  
-   [使用 Management Studio 設定 Analysis Services](#bkmk_ssas_extended_events_ssms)  
  
-   [用以啟動 Analysis Services 中擴充事件的 XMLA 指令碼](#bkmk_script_start)  
  
##  <a name="bkmk_ssas_extended_events_ssms"></a> 使用 Management Studio 設定 Analysis Services  
 針對表格式和多維度執行個體，Management Studio 提供新的管理資料夾，其中包含使用者初始的 xEvent 工作階段。 您可以一次執行多個工作階段。 不過，在目前的實作中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 擴充事件使用者介面不支援更新或重新執行現有的工作階段。  
  
 ![ssas_extended_events_ssms_start](../../analysis-services/instances/media/ssas-extended-events-ssms-start.png "ssas_extended_events_ssms_start")  
  
 **選擇事件**  
  
 如果您已經知道想要擷取的事件，則搜尋它們是將它們加入追蹤的最簡單方式。 否則，通常會使用下列事件進行監視作業：  
  
-   **CommandBegin** 和 **CommandEnd**。  
  
-   **QueryBegin**、 **QueryEnd**和 **QuerySubcubeVerbose** (顯示整個 MDX 或傳送到伺服器的 DAX 查詢)，加上 **ResourceUsage** (適用於查詢所取用資源的統計資料，以及要傳回多少個資料列)。  
  
-   **ProgressReportBegin** 和 **ProgressReportEnd** (適用於處理作業)。  
  
-   **AuditLogin** 和 **AuditLogout** (會擷取用戶端應用程式連接至 Analysis Services 的使用者識別)。  
  
 **選擇資料存放區**  
  
 工作階段可以即時串流處理到 Management Studio 中的視窗，或保存至檔案以使用 Power Query 或 Excel 進行後續分析。  
  
-   **event_file** 會將工作階段資料儲存於 .xel 檔案中。  
  
-   **event_stream** 可在 Management Studio 中啟用 [監看即時資料] 選項。  
  
-   只要伺服器正在執行中，**ring_buffer** 就會將工作階段資料儲存在記憶體中。 在伺服器重新啟動時，即會擲出工作階段資料  
  
 **新增事件欄位**  
  
 請務必設定包括事件欄位的工作階段，讓您能夠輕鬆地查看感興趣的資訊。  
  
 [設定] 是對話方塊中最右側的選項。  
  
 ![ssas xevents 設定](../../analysis-services/instances/media/ssas-xevents-configure.PNG "ssas xevents 設定")  
  
 在組態中，於 [事件欄位] 索引標籤上選取 [TextData]，如此一來，此欄位會出現在事件相鄰位置並顯示傳回值，其中包括在伺服器上執行的查詢。  
  
 在針對所需的事件和資料存放區設定工作階段之後，您可以按一下指令碼按鈕，將您的組態傳送到其中一個支援的目的地，包括檔案、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的新查詢，以及剪貼簿。  
  
 **重新整理工作階段**  
  
 一旦建立工作階段之後，請務必重新整理 Management Studio 中的 [工作階段] 資料夾，以查看您剛建立的工作階段。 如果設定了 event_stream，您就能以滑鼠右鍵按一下工作階段名稱，並選擇 [監看即時資料] 來監視即時伺服器活動。  
  
##  <a name="bkmk_script_start"></a> 用以啟動 Analysis Services 中擴充事件的 XMLA 指令碼  
 您可以使用類似的 XMLA 建立物件指令碼命令來啟用擴充事件追蹤，如下所示：  
  
```  
<Execute …>  
   <Command>  
      <Batch …>  
         <Create …>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session …>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" …/>  
                        </event>  
                        <target package="PACKAGE0" name="asynchronous_file_target">  
                           <parameter name="filename" value="data_filename.xel"/>  
                           <parameter name="metadatafile" value="metadata_filename.xem"/>  
                        </target>  
                     </event_session>  
                  </ddl300_300:XEvent>  
               </Trace>  
            </ObjectDefinition>  
         </Create>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 其中，下列元素會由使用者根據追蹤需要而定義：  
  
 *trace_id*  
 定義此追蹤的唯一識別碼。  
  
 *trace_name*  
 提供給此追蹤的名稱；通常是人們可讀取的追蹤定義。 使用 *trace_id* 值作為名稱是常見的做法。  
  
 *AS_event*  
 要公開的 Analysis Services 事件。 如需事件的名稱，請參閱 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md) 。  
  
 *data_filename*  
 包含事件資料之檔案的名稱。 此名稱的後置字元為時間戳記，以防重複傳送追蹤時，資料遭到覆寫。  
  
 *metadata_filename*  
 包含事件中繼資料之檔案的名稱。 此名稱的後置字元為時間戳記，以防重複傳送追蹤時，資料遭到覆寫。  
  
||  
|-|  
|![搭配回到頁首連結使用的箭號圖示](../../analysis-services/instances/media/uparrow16x16.gif "搭配回到頁首連結使用的箭號圖示")[本主題內容](#bkmk_top)|  
  
##  <a name="bkmk_script_stop"></a> 用以停止 Analysis Services 中擴充事件的 XMLA 指令碼  
 若要停止擴充事件追蹤物件，您需要使用類似的 XMLA 刪除物件指令碼命令來刪除該物件，如下所示：  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch …>  
         <Delete …>  
            <Object>  
               <TraceID>trace_id</TraceID>  
            </Object>  
         </Delete>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 其中，下列元素會由使用者根據追蹤需要而定義：  
  
 *trace_id*  
 定義要刪除之追蹤的唯一識別碼。  
  
||  
|-|  
|![搭配回到頁首連結使用的箭號圖示](../../analysis-services/instances/media/uparrow16x16.gif "搭配回到頁首連結使用的箭號圖示")[本主題內容](#bkmk_top)|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  

