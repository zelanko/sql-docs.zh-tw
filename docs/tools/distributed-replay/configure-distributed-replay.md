---
title: "設定 Distributed 的 Replay |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: distributed-replay
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aee11dde-daad-439b-b594-9f4aeac94335
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0eb4502675fb2bd9e9978b5443882a44f867e39c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="configure-distributed-replay"></a>設定 Distributed Replay
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay controller、 client 上的 XML 檔案中指定 Distributed Replay 組態詳細資料以及安裝管理工具的位置。 這些檔案包括下列各項：  
  
-   [控制器組態檔](#DReplayController)  
  
-   [用戶端組態檔](#DReplayClient)  
  
-   [前置處理組態檔](#PreprocessConfig)  
  
-   [重新執行組態檔](#ReplayConfig)  
  
##  <a name="DReplayController"></a> 控制器組態檔：DReplayController.config  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 服務啟動時，會從控制器組態檔 `DReplayController.config`載入記錄層次。 這個檔案位於您安裝 Distributed Replay Controller 服務的資料夾中：  
  
 **\<控制器安裝路徑 > \DReplayController.config**  
  
 控制器組態檔所指定的記錄層次包括：  
  
|設定|XML 元素|說明|允許的值|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|記錄層級|`<LoggingLevel>`|指定控制器服務的記錄層次。|`INFORMATION` &#124; `WARNING` &#124; `CRITICAL`|否。 根據預設，此值為 `CRITICAL`。|  
  
### <a name="example"></a>範例  
 此範例會顯示已經修改為隱藏 `INFORMATION` 和 `WARNING` 記錄項目的控制器組態檔。  
  
```  
<?xml version='1.0'?>  
<Options>  
<LoggingLevel>CRITICAL</LoggingLevel>  
</Options>  
```  
  
##  <a name="DReplayClient"></a> 用戶端組態檔：DReplayClient.config  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 服務啟動時，會從用戶端組態檔 ( `DReplayClient.config`) 載入組態設定。 這個檔案位於每個用戶端上您安裝 Distributed Replay Client 服務的資料夾中：  
  
 **\<用戶端安裝路徑 > \DReplayClient.config**  
  
 用戶端組態檔所指定的設定包括：  
  
|設定|XML 元素|說明|允許的值|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|控制器|`<Controller>`|指定控制器的電腦名稱。 用戶端會嘗試連絡控制器，藉以向 Distributed Replay 環境註冊。|您可以使用 "`localhost`" 或 "`.`" 表示本機電腦。|否。 根據預設，用戶端會嘗試向本機執行的 Controller 執行個體 ("`.`") 註冊 (如果它存在的話)。|  
|用戶端工作目錄|`<WorkingDirectory>`|這是在用戶端上儲存分派檔案的本機路徑。<br /><br /> 下一次重新執行時，就會覆寫這個目錄中的檔案。|完整目錄名稱，以磁碟機代號為開頭。|否。 如果未指定值，則分派檔案與預設用戶端組態檔會儲存在相同的位置。 如果有指定值，而且該資料夾不存在用戶端上，用戶端服務就不會啟動。|  
|用戶端結果目錄|`<ResultDirectory>`|這是在用戶端上儲存重新執行活動之結果追蹤檔案 (針對用戶端) 的本機路徑。<br /><br /> 下一次重新執行時，就會覆寫這個目錄中的檔案。|完整目錄名稱，以磁碟機代號為開頭。|否。 如果未指定值，則結果追蹤檔案與預設用戶端組態檔會儲存在相同的位置。 如果有指定值，而且該資料夾不存在用戶端上，用戶端服務就不會啟動。|  
|記錄層級|`<LoggingLevel>`|這是用戶端服務的記錄層次。|`INFORMATION` &#124; `WARNING` &#124; `CRITICAL`|否。 根據預設，此值為 `CRITICAL`。|  
  
### <a name="example"></a>範例  
 此範例會顯示已經修改為指定控制器服務在不同電腦 (名為 `Controller1`的電腦) 上執行的用戶端組態檔。 `WorkingDirectory` 和 `ResultDirectory` 項目已經分別設定成使用 `c:\ClientWorkingDir` 和 `c:\ResultTraceDir`資料夾。 記錄層次已經從預設值變更為隱藏 `INFORMATION` 和 `WARNING` 記錄項目。  
  
```  
<?xml version='1.0'?>  
<Options>  
    <Controller>Controller1</Controller>  
    <WorkingDirectory>c:\ClientWorkingDir</WorkingDirectory>  
    <ResultDirectory>c:\ResultTraceDir</ResultDirectory>  
    <LoggingLevel>CRITICAL</LoggingLevel>  
</Options>  
```  
  
##  <a name="PreprocessConfig"></a> 前置處理組態檔：DReplay.exe.preprocess.config  
 當您使用管理工具來起始前置處理階段時，管理工具就會從前置處理組態檔 `DReplay.exe.preprocess.config`載入前置處理設定。  
  
 您可以使用預設組態檔，也可以使用管理工具的 **-c** 參數來指定已修改前置處理組態檔的位置。 如需使用管理工具之前置處理選項的詳細資訊，請參閱[前置處理選項 &#40;Distributed Replay 管理工具&#41;](../../tools/distributed-replay/preprocess-option-distributed-replay-administration-tool.md)。  
  
 預設前置處理組態檔位於您安裝管理工具的資料夾中：  
  
 **\<系統管理工具安裝路徑 > \DReplayAdmin\DReplay.exe.preprocess.config**  
  
 前置處理組態設定指定於前置處理組態檔中屬於 `<PreprocessModifiers>` 元素子系的 XML 元素中。 這些設定包括：  
  
|設定|XML 元素|說明|允許的值|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|包含系統工作階段活動|`<IncSystemSession>`|指出是否要在重新執行期間包含擷取期間進行的系統工作階段活動。|`Yes` &#124; `No`|否。 根據預設，此值為 `No`。|  
|最大閒置時間|`<MaxIdleTime>`|將閒置時間的上限設定為絕對數字 (以秒為單位)。|>= -1 的整數。<br /><br /> `-1` 表示沒有變更原始追蹤檔案的原始值。<br /><br /> `0` 表示在任何給定的時間點有某個活動進行中。|否。 根據預設，此值為 `-1`。|  
  
### <a name="example"></a>範例  
 預設前置處理組態檔：  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
##  <a name="ReplayConfig"></a> 重新執行組態檔：DReplay.exe.replay.config  
 當您使用管理工具來起始事件重新執行階段時，管理工具就會從重新執行組態檔 `DReplay.exe.replay.config`載入重新執行設定。  
  
 您可以使用預設組態檔，也可以使用管理工具的 **-c** 參數來指定已修改重新執行組態檔的位置。 如需使用管理工具之重新執行選項的詳細資訊，請參閱[重新執行選項 &#40;Distributed Replay 管理工具&#41;](../../tools/distributed-replay/replay-option-distributed-replay-administration-tool.md)。  
  
 預設重新執行組態檔位於您安裝管理工具的資料夾中：  
  
 **\<系統管理工具安裝路徑 > \DReplayAdmin\DReplay.exe.replay.config**  
  
 重新執行組態設定指定於重新執行組態檔中屬於 `<ReplayOptions>` 和 `<OutputOptions>` 元素子系的 XML 元素中。  
  
### <a name="replayoptions-element"></a>\<P > 項目  
 重新執行組態檔在 `<ReplayOptions>` 元素中指定的設定如下：  
  
|設定|XML 元素|說明|允許的值|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目標執行個體 (測試伺服器)|`<Server>`|指定伺服器名稱以及要連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|*server_name*[\\*instance_name*]<br /><br /> 您無法使用 "`localhost`" 或 "`.`" 來代表本機主機。|否，如果已經搭配使用 **-s***目標伺服器* 參數與管理工具的 [重新執行] 選項來指定伺服器名稱。|  
|順序模式|`<SequencingMode>`|指定用於事件排程的模式。|`synchronization` &#124; `stress`|否。 根據預設，此值為 `stress`。|  
|壓力規模粒度|`<StressScaleGranularity>`|指定服務設定檔識別碼 (SPID) 上的所有連接是應該在壓力模式下同時 (SPID) 還是個別 (連接) 調整。|SPID &#124; 連接|是的。 根據預設，此值為 `SPID`。|  
|連接時間間隔|`<ConnectTimeScale>`|這是用來在壓力模式中設定連接時間的間隔。|介於 `1` 與 `100`之間的整數。|否。 根據預設，此值為 `100`。|  
|考慮時間間隔|`<ThinkTimeScale>`|這是用來在壓力模式中設定考慮時間的間隔。|介於 `0` 與 `100`之間的整數。|否。 根據預設，此值為 `100`。|  
|使用連接共用|`<UseConnectionPooling>`|指定是否要在每個 Distributed Replay Client 上啟用連接共用。|是 &#124; 否|是的。 根據預設，此值為 `Yes`。|  
|健全狀況監視器間隔|`<HealthmonInterval>`|表示要執行健全狀況監視器的頻率 (以秒為單位)。<br /><br /> 此值只用於同步處理模式中。|>= 1 的整數<br /><br /> (`-1` 表示停用)|否。 根據預設，此值為 `60`。|  
|查詢逾時|`<QueryTimeout>`|指定查詢逾時值 (以秒為單位)。 此值只在傳回第一個資料列之前有效。|>= 1 的整數<br /><br /> (`-1` 表示停用)|否。 根據預設，此值為 `3600`。|  
|每個用戶端的執行緒|`<ThreadsPerClient>`|指定要用於每個重新執行用戶端的重新執行執行緒數目。|介於 `1` 與 `512`之間的整數。|否。 如果未指定，則 Distributed Replay 會使用值 `255`。|  
  
### <a name="outputoptions-element"></a>\<P > 項目  
 重新執行組態檔在 `<OutputOptions>` 元素中指定的設定如下：  
  
|設定|XML 元素|說明|允許的值|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|記錄資料列計數|`<RecordRowCount>`|指出是否應該針對每個結果集記錄資料列計數。|`Yes` &#124; `No`|否。 根據預設，此值為 `Yes`。|  
|記錄結果集|`<RecordResultSet>`|指出是否應該記錄所有結果集的內容。|`Yes` &#124; `No`|否。 根據預設，此值為 `No`。|  
  
### <a name="example"></a>範例  
 預設重新執行組態檔：  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server></Server>  
        <SequencingMode>stress</SequencingMode>  
        <ConnectTimeScale></ConnectTimeScale>  
        <ThinkTimeScale></ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
## <a name="see-also"></a>另請參閱  
 [管理工具命令列選項 &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [SQL Server Distributed Replay 論壇](http://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [使用 Distributed Replay 對您的 SQL Server – 第 2 部分進行負載測試](http://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [使用 Distributed Replay 對您的 SQL Server-第 1 部分進行負載測試](http://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
