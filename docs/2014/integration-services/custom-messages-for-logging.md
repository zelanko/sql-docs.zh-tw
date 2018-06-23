---
title: Custom Messages for Logging |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logs [Integration Services], custom
- writing log entries
- SSIS packages, logs
- custom messages for logging [Integration Services]
ms.assetid: 3c74bba9-02b7-4bf5-bad5-19278b680730
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 80086e7a946ad9d5457e95646bcd9c8bce3e3df3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030830"
---
# <a name="custom-messages-for-logging"></a>自訂訊息以進行記錄
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供一組豐富的自訂事件寫入記錄項目，為封裝和許多工作。 您可以使用這些項目，透過記錄預先定義事件或使用者自訂訊息，來儲存關於執行進度、結果和問題的詳細資訊，以供稍後分析。 比方說，您可以記錄大量插入開始和結束的時間，以便識別封裝執行時的效能問題。  
  
 自訂記錄項目是一組與可用於封裝以及所有容器和工作的標準記錄事件不同的項目。 自訂記錄項目可以用來擷取與封裝中特定工作相關的有用資訊。 例如，「執行 SQL」工作記錄的其中一個自訂記錄項目會在記錄檔中記錄該工作所執行的 SQL 陳述式。  
  
 所有的記錄項目都包含日期和時間資訊，包括封裝開始和完成時自動寫入的記錄項目。 許多記錄事件都會將多個項目寫入記錄檔。 當事件具有不同的階段時，通常就會發生這種情況。 例如，`ExecuteSQLExecutingQuery`記錄檔事件會寫入三個項目： 一個項目，在工作取得資料庫，另一個工作之後的連接之後開始準備 SQL 陳述式，以及一個更多的 SQL 陳述式執行完成之後。  
  
 下列 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件具有自訂記錄項目：  
  
 [封裝](#Package)  
  
 [大量插入工作](#BulkInsert)  
  
 [資料流程工作](#DataFlow)  
  
 [執行 DTS 2000 工作](#ExecuteDTS200)  
  
 [執行處理工作](#ExecuteProcess)  
  
 [執行 SQL 工作](#ExecuteSQL)  
  
 [檔案系統工作](#FileSystem)  
  
 [FTP 工作](#FTP)  
  
 [訊息佇列工作](#MessageQueue)  
  
 [指令碼工作](#Script)  
  
 [傳送郵件工作](#SendMail)  
  
 [傳送資料庫工作](#TransferDatabase)  
  
 [傳送錯誤訊息工作](#TransferErrorMessages)  
  
 [傳送作業工作](#TransferJobs)  
  
 [傳送登入工作](#TransferLogins)  
  
 [傳輸主要預存程序工作](#TransferMasterStoredProcedures)  
  
 [傳送 SQL Server 物件工作](#TransferSQLServerObjects)  
  
 [Web 服務工作](#WebServices)  
  
 [WMI 資料讀取器工作](#WMIDataReader)  
  
 [WMI 事件監看員工作](#WMIEventWatcher)  
  
 [XML 工作](#XML)  
  
## <a name="log-entries"></a>記錄項目  
  
###  <a name="Package"></a> 封裝  
 下表列出封裝的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`PackageStart`|指出封裝已經開始執行。<br /><br /> 注意：此記錄項目會自動寫入記錄檔中。 您無法排除它。|  
|`PackageEnd`|指出封裝已經完成。<br /><br /> 注意：此記錄項目會自動寫入記錄檔中。 您無法排除它。|  
|`Diagnostic`|提供影響封裝執行之系統組態的相關資訊，例如可以同時執行的可執行檔數目。<br /><br /> `Diagnostic`記錄項目也包括之前和之後的項目，呼叫外部資料提供者。 如需詳細資訊，請參閱 [疑難排解工具封裝連接](troubleshooting/troubleshooting-tools-for-package-connectivity.md)。|  
  
###  <a name="BulkInsert"></a> 大量插入工作  
 下表列出「大量插入」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`DTSBulkInsertTaskBegin`|指出大量插入已經開始。|  
|`DTSBulkInsertTaskEnd`|指出大量插入已經完成。|  
|`DTSBulkInsertTaskInfos`|提供有關工作的描述性資訊。|  
  
###  <a name="DataFlow"></a> 資料流程工作  
 下表列出「資料流程」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`BufferSizeTuning`|指出資料流程工作已經變更緩衝區的大小。 記錄項目會描述大小變更的原因，並列出暫存的新緩衝區大小。|  
|`OnPipelinePostEndOfRowset`|表示該元件具有其結尾的資料列集的信號，這是由最後一個呼叫的`ProcessInput`方法。 處理輸入之資料流程中的每個元件都會寫入一個項目。 項目中包含元件的名稱。|  
|`OnPipelinePostPrimeOutput`|指出元件已經完成其上次呼叫`PrimeOutput`方法。 根據資料流程而定，可能會寫入多個記錄項目。 如果元件是來源，這表示該元件已經完成處理資料列。|  
|`OnPipelinePreEndOfRowset`|指出元件即將接收其結尾的資料列集的信號，這是由最後一個呼叫的`ProcessInput`方法。 處理輸入之資料流程中的每個元件都會寫入一個項目。 項目中包含元件的名稱。|  
|`OnPipelinePrePrimeOutput`|指出元件即將從 `PrimeOutput` 方法接收其呼叫。 根據資料流程而定，可能會寫入多個記錄項目。|  
|`OnPipelineRowsSent`|報告由 `ProcessInput` 方法之呼叫提供給元件輸入的資料列數目。 記錄項目會包含元件名稱。|  
|`PipelineBufferLeak`|提供在緩衝區管理員停止之後使緩衝區保持運作之任何元件的相關資訊。 這表示緩衝區資源並未釋放，而可能導致記憶體遺漏。 記錄項目會提供元件的名稱和緩衝區的識別碼。|  
|`PipelineExecutionPlan`|報告資料流程的執行計畫。 此項目提供如何將緩衝區傳送至元件的相關資訊。 這項資訊結合 PipelineExecutionTrees 項目，描述工作內部所發生的情況。|  
|`PipelineExecutionTrees`|報告資料流程中的配置執行樹狀目錄。 資料流程引擎的排程器使用這些樹狀目錄來建立資料流程的執行計畫。|  
|`PipelineInitialization`|提供有關工作的初始化資訊。 這項資訊包括作為 BLOB 資料暫存儲存位置使用的目錄、預設緩衝區大小，以及緩衝區中的資料列數目。 根據資料流程工作的組態而定，可能會寫入多個記錄項目。|  
  
###  <a name="ExecuteDTS200"></a> 執行 DTS 2000 工作  
 下表列出「執行 DTS 2000」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`ExecuteDTS80PackageTaskBegin`|指出工作已經開始執行 DTS 2000 封裝。|  
|`ExecuteDTS80PackageTaskEnd`|指出工作已經完成。<br /><br /> 注意：DTS 2000 封裝可能會在工作結束之後繼續執行。|  
|`ExecuteDTS80PackageTaskTaskInfo`|提供有關工作的描述性資訊。|  
|`ExecuteDTS80PackageTaskTaskResult`|報告工作執行之 DTS 2000 封裝的執行結果。|  
  
###  <a name="ExecuteProcess"></a> 執行處理工作  
 下表列出「執行處理」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|提供工作設定執行之可執行檔的執行處理相關資訊。<br /><br /> 將會寫入兩個記錄項目。 其中一個包含工作執行之可執行檔的名稱和位置相關資訊，另一個項目則記錄可執行檔的結束。|  
|`ExecuteProcessVariableRouting`|提供有關哪些變數會傳到可執行檔之輸入和輸出的相關資訊。 將會寫入 stdin (輸入)、stdout (輸出) 和 stderr (錯誤輸出) 的記錄項目。|  
  
###  <a name="ExecuteSQL"></a> 執行 SQL 工作  
 下表描述「執行 SQL」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|提供 SQL 陳述式執行階段的相關資訊。 寫入記錄項目的時機包括在工作取得資料庫連接時、在工作開始準備 SQL 陳述式時，以及在 SQL 陳述式執行完成之後。 準備階段的記錄項目包含工作所使用的 SQL 陳述式。|  
  
###  <a name="FileSystem"></a> 檔案系統工作  
 下表描述「檔案系統」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`FileSystemOperation`|報告工作執行的作業。 記錄項目會在檔案系統作業開始時寫入，項目中包含有關來源和目的地的資訊。|  
  
###  <a name="FTP"></a> FTP 工作  
 下表列出 FTP 工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`FTPConnectingToServer`|指出工作已經起始與 FTP 伺服器的連接。|  
|`FTPOperation`|報告工作執行之 FTP 作業的開始及其類型。|  
  
###  <a name="MessageQueue"></a> 訊息佇列工作  
 下表列出「訊息佇列」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`MSMQAfterOpen`|指出工作已經完成開啟訊息佇列。|  
|`MSMQBeforeOpen`|指出工作已經開始開啟訊息佇列。|  
|`MSMQBeginReceive`|指出工作已經開始接收訊息。|  
|`MSMQBeginSend`|指出工作已經開始傳送訊息。|  
|`MSMQEndReceive`|指出工作已經完成接收訊息。|  
|`MSMQEndSend`|指出工作已經完成傳送訊息。|  
|`MSMQTaskInfo`|提供有關工作的描述性資訊。|  
|`MSMQTaskTimeOut`|指出工作已經逾時。|  
  
###  <a name="Script"></a> 指令碼工作  
 下表描述「指令碼」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`ScriptTaskLogEntry`|報告在指令碼內實作記錄的結果。 每次呼叫都會寫入記錄項目`Log`方法`Dts`物件。 項目會在程式碼執行時寫入。 如需詳細資訊，請參閱 [Logging in the Script Task](extending-packages-scripting/task/logging-in-the-script-task.md)。|  
  
###  <a name="SendMail"></a> 傳送郵件工作  
 下表列出「傳送郵件」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`SendMailTaskBegin`|指出工作已經開始傳送電子郵件訊息。|  
|`SendMailTaskEnd`|指出工作已經完成傳送電子郵件訊息。|  
|`SendMailTaskInfo`|提供有關工作的描述性資訊。|  
  
###  <a name="TransferDatabase"></a> 傳送資料庫工作  
 下表列出「傳送資料庫」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`SourceDB`|指定工作所複製的資料庫。|  
|`SourceSQLServer`|指定從中複製資料庫的電腦。|  
  
###  <a name="TransferErrorMessages"></a> 傳送錯誤訊息工作  
 下表列出「傳送錯誤訊息」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`TransferErrorMessagesTaskFinishedTransferringObjects`|指出工作已經完成傳送錯誤訊息。|  
|`TransferErrorMessagesTaskStartTransferringObjects`|指出工作已經開始傳送錯誤訊息。|  
  
###  <a name="TransferJobs"></a> 傳送作業工作  
 下表列出「傳送作業」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`TransferJobsTaskFinishedTransferringObjects`|指出工作已經完成傳送 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 作業。|  
|`TransferJobsTaskStartTransferringObjects`|指出工作已經開始傳送 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 作業。|  
  
###  <a name="TransferLogins"></a> 傳送登入工作  
 下表列出「傳送登入」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`TransferLoginsTaskFinishedTransferringObjects`|指出工作已經完成傳送登入。|  
|`TransferLoginsTaskStartTransferringObjects`|指出工作已經開始傳送登入。|  
  
###  <a name="TransferMasterStoredProcedures"></a> 傳送主要預存程序工作  
 下表列出「傳送主要預存程序」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`TransferStoredProceduresTaskFinishedTransferringObjects`|指出工作已經完成傳送儲存在 **master** 資料庫中的使用者定義預存程序。|  
|`TransferStoredProceduresTaskStartTransferringObjects`|指出工作已經開始傳送儲存在 **master** 資料庫中的使用者定義預存程序。|  
  
###  <a name="TransferSQLServerObjects"></a> 傳送 SQL Server 物件工作  
 下表列出「傳送 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`TransferSqlServerObjectsTaskFinishedTransferringObjects`|指出工作已經完成傳送 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫物件。|  
|`TransferSqlServerObjectsTaskStartTransferringObjects`|指出工作已經開始傳送 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫物件。|  
  
###  <a name="WebServices"></a> Web 服務工作  
 下表列出您可以為「Web 服務」工作啟用的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`WSTaskBegin`|工作已經開始存取 Web 服務。|  
|`WSTaskEnd`|工作已經完成 Web 服務方法。|  
|`WSTaskInfo`|關於工作的描述性資訊。|  
  
###  <a name="WMIDataReader"></a> WMI 資料讀取器工作  
 下表列出「WMI 資料讀取器」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|指出工作已經開始讀取 WMI 資料。|  
|`WMIDataReaderOperation`|報告工作已執行的 WQL 查詢。|  
  
###  <a name="WMIEventWatcher"></a> WMI 事件監看員工作  
 下表列出「WMI 事件監看員」工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|表示發生工作正在監視的事件。|  
|`WMIEventWatcherTimedout`|指出工作已經逾時。|  
|`WMIEventWatcherWatchingForWMIEvents`|指出工作已經開始執行 WQL 查詢。 項目包含查詢。|  
  
###  <a name="XML"></a> XML 工作  
 下表描述 XML 工作的自訂記錄項目。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`XMLOperation`|提供有關工作執行之作業的資訊。|  
  
## <a name="related-content"></a>相關內容  
 dougbert.com 上的部落格文章： [記錄 Integration Services 工作的自訂事件](http://go.microsoft.com/fwlink/?LinkId=150580)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 記錄](performance/integration-services-ssis-logging.md)  
  
  