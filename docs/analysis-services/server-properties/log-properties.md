---
title: 記錄屬性 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- QueryLogFileSize property
- QueryLogTableName property
- TraceBackgroundDistributionPeriod property
- TraceMaxRowsetSize property
- NullKeyConvertedToUnknown property
- CrashReportsFolder property
- TraceDefinitionFile property
- SQLDumperFlagsOn property
- KeyErrorLimit property
- SnapshotDefinitionFile property
- MinidumpErrorList property
- ErrorLogFileName property
- KeyDuplicate property
- IgnoreDataTruncation property
- logs [Analysis Services]
- Enabled property
- FileSizeMB property
- TraceFileWriteTrailerPeriod property
- TraceQueryResponseTextChunkSize property
- File property
- FileBufferSize property
- TraceRowsetBackgroundFlushPeriod property
- ErrorLogFileSize property
- TraceRequestParameters property
- KeyErrorLimitAction property
- CreateQueryLogTable property
- LogDir property
- TraceBackgroundFlushPeriod property
- TraceFileBufferSize property
- SQLDumperFlagsOff property
- QueryLogConnectionString property
- KeyNotFound property
- KeyErrorLogFile property
- TraceReportFQDN property
- KeyErrorAction property
- QueryLogFileName property
- MessageLogs property
- MiniDumpFlagsOn property
- SnapshotFrequencySec property
- QueryLogSampling property
- CreateAndSendCrashReports property
- LogDurationSec property
ms.assetid: 33fd90ee-cead-48f0-8ff9-9b458994c766
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b76b9011d6c138669d75fb9ff3caebf6f74bc00a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="log-properties"></a>記錄屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的記錄伺服器屬性。 如需其他伺服器屬性以及如何設定伺服器屬性的詳細資訊，請參閱 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
## <a name="general"></a>一般  
 **檔案**  
 此為字串屬性，識別伺服器記錄檔的名稱。 這個屬性只適用於當記錄會儲存到磁碟檔案，而非資料庫資料表時 (預設行為)。  
  
 此屬性的預設值為 msmdsrv.log。  
  
 **FileBufferSize**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **MessageLogs**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="error-log"></a>錯誤記錄檔  
 您可以在伺服器執行個體層級設定這些屬性，以修改顯示在其他工具和設計師中之錯誤組態的預設值。 請參閱[Cube、 分割區和維度處理的錯誤組態&#40;SSAS-多維度&#41;](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)和<xref:Microsoft.AnalysisServices.MiningStructure.ErrorConfiguration%2A>如需詳細資訊。  
  
 **ErrorLog\ErrorLogFileName**  
 此屬性在伺服器執行處理作業期間，用來作為預設值。  
  
 **ErrorLog\ErrorLogFileSize**  
 此屬性在伺服器執行處理作業期間，用來作為預設值。  
  
 **ErrorLog\KeyErrorAction**  
 指定伺服器在發生 **KeyNotFound** 錯誤時所採取的動作。 此錯誤的有效回應包括：  
  
-   **ConvertToUnknown** 會要求伺服器將錯誤索引鍵值配置給未知的成員。  
  
-   **DiscardRecord** 會要求伺服器排除這個記錄。  
  
 **ErrorLog\KeyErrorLogFile**  
 這是副檔名必須為 .log 的使用者定義檔案名稱，位於服務帳戶具有讀寫權限的資料夾內。 此記錄檔只會包含處理期間產生的錯誤。 如果需要更詳細的資訊，請使用飛行記錄器。  
  
 **ErrorLog\KeyErrorLimit**  
 這是伺服器允許的資料完整性錯誤數上限，達到此上限之後，即無法繼續處理。 值為 -1 表示沒有限制。 預設值為 0，表示在發生第一個錯誤之後停止處理。 您也可以將其設為整數。  
  
 **ErrorLog\KeyErrorLimitAction**  
 指定伺服器在索引鍵錯誤數目達到上限時所採取的動作。 此動作的有效回應包括：  
  
-   **StopProcessing** 會要求伺服器在達到錯誤限制時停止處理。  
  
-   **StopLogging** 會要求伺服器在達到錯誤限制時停止記錄錯誤，但允許繼續處理。  
  
 **ErrorLog\ LogErrorTypes\KeyNotFound**  
 指定伺服器在發生 **KeyNotFound** 錯誤時所採取的動作。 此錯誤的有效回應包括：  
  
-   **IgnoreError** 會要求伺服器繼續處理，但不記錄錯誤或將其計入索引鍵錯誤限制。 如果忽略錯誤，您僅允許繼續處理，而不將錯誤加入錯誤計數，或將其記錄至畫面或記錄檔。 有問題的記錄發生資料完整性問題，無法加入資料庫。 依據 **KeyErrorAction** 屬性的判斷，該記錄將會被捨棄或彙總至未知的成員。  
  
-   **ReportAndContinue** 會要求伺服器記錄錯誤、將其計入索引鍵錯誤限制，並繼續處理。 觸發錯誤的記錄會被捨棄，或是轉換成未知的成員。  
  
-   **ReportAndStop** 會要求伺服器記錄錯誤，並立即停止處理，而不管索引鍵錯誤限制。 觸發錯誤的記錄會被捨棄，或是轉換成未知的成員。  
  
 **ErrorLog\ LogErrorTypes\KeyDuplicate**  
 指定伺服器在發現索引鍵重複狀況時所採取的動作。 **IgnoreError** 有效值包括 **ReportAndContinue** (繼續處理，就像沒有發生錯誤一樣)、 **ReportAndStop** (記錄錯誤並繼續處理)，以及  (記錄錯誤並立即停止處理，即使錯誤計數未達錯誤限制也一樣)。  
  
 **ErrorLog\ LogErrorTypes\NullKeyConvertedToUnknown**  
 指定伺服器在 Null 索引鍵轉換為未知的成員時所採取的動作。 **IgnoreError** 有效值包括 **ReportAndContinue** (繼續處理，就像沒有發生錯誤一樣)、 **ReportAndStop** (記錄錯誤並繼續處理)，以及  (記錄錯誤並立即停止處理，即使錯誤計數未達錯誤限制也一樣)。  
  
 **ErrorLog\ LogErrorTypes\NullKeyNotAllowed**  
 指定伺服器在維度屬性的 **NullProcessing** 設為 **Error** 時所採取的動作。 當給定的屬性中不允許 Null 值時，會產生錯誤。 此錯誤組態屬性會通知下一個步驟，也就是報告錯誤並繼續處理，直到達到錯誤限制為止。 **IgnoreError** 有效值包括 **ReportAndContinue** (繼續處理，就像沒有發生錯誤一樣)、 **ReportAndStop** (記錄錯誤並繼續處理)，以及  (記錄錯誤並立即停止處理，即使錯誤計數未達錯誤限制也一樣)。  
  
 **ErrorLog\ LogErrorTypes\CalculationError**  
 此屬性在伺服器執行處理作業期間，用來作為預設值。  
  
 **ErrorLog\IgnoreDataTruncation**  
 此屬性在伺服器執行處理作業期間，用來作為預設值。  
  
## <a name="exception"></a>例外狀況  
 **Exception\CreateAndSendCrashReports**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Exception\CrashReportsFolder**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Exception\SQLDumperFlagsOn**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Exception\SQLDumperFlagsOff**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Exception\MiniDumpFlagsOn**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Exception\MinidumpErrorList**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="flight-recorder"></a>飛行記錄器  
 **FlightRecorder\Enabled**  
 此為布林值屬性，指出是否啟用飛行記錄器功能。  
  
 **FlightRecorder\FileSizeMB**  
 此為帶正負號的 32 位元整數屬性，定義飛行記錄器磁碟檔案的大小 (以 MB 表示)。  
  
 **FlightRecorder\LogDurationSec**  
 此為帶正負號的 32 位元整數屬性，定義飛行記錄器換用的頻率 (以秒為單位)。  
  
 **FlightRecorder\SnapshotDefinitionFile**  
 此為字串屬性，定義快照集定義檔案的名稱，包含採取快照集時，發給伺服器的探索命令。  
  
 此屬性的預設值是空白，因而會預設為 FlightRecorderSnapshotDef.xml 檔案名稱。  
  
 **FlightRecorder\SnapshotFrequencySec**  
 此為帶正負號的 32 位元整數屬性，定義快照集頻率 (以秒為單位)。  
  
 **FlightRecorder\TraceDefinitionFile**  
 此為字串屬性，指定飛行記錄器追蹤定義檔案的名稱。  
  
 此屬性的預設值是空白，因而會預設為 FlightRecorderTraceDef.xml。  
  
## <a name="query-log"></a>查詢記錄  
 **適用於** ：僅限於多維度伺服器模式  
  
 **QueryLog\QueryLogFileName**  
 此為字串屬性，指定查詢記錄檔的名稱。 這個屬性只適用於當記錄會儲存到磁碟檔案，而非資料庫資料表時 (預設行為)。  
  
 **QueryLog\QueryLogSampling**  
 此為帶正負號的 32 位元整數屬性，指定查詢記錄取樣率。  
  
 此屬性的預設值為 10，表示每 10 筆伺服器查詢會記錄 1 筆。  
  
 **QueryLog\QueryLogFileSize**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **QueryLog\QueryLogConnectionString**  
 此為字串屬性，指定查詢記錄資料庫的連接。  
  
 **QueryLog\QueryLogTableName**  
 此為字串屬性，指定查詢記錄資料表的名稱。  
  
 此屬性的預設值為 OlapQueryLog。  
  
 **QueryLog\CreateQueryLogTable**  
 此為布林值屬性，指定是否建立查詢記錄資料表。  
  
 此屬性的預設值為 False，表示伺服器不會自動建立記錄資料表，也不會記錄查詢事件。  
  
> [!NOTE]  
>  如需設定查詢記錄的詳細資訊，請參閱 [設定 Analysis Services 查詢記錄](http://go.microsoft.com/fwlink/?LinkId=81890)。  
  
## <a name="trace"></a>Trace  
 **Trace\TraceBackgroundDistributionPeriod**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Trace\TraceBackgroundFlushPeriod**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Trace\TraceFileBufferSize**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Trace\TraceFileWriteTrailerPeriod**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Trace\TraceMaxRowsetSize**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Trace\TraceProtocolTraffic**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Trace\TraceQueryResponseTextChunkSize**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Trace\TraceReportFQDN**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Trace\TraceRequestParameters**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **Trace\TraceRowsetBackgroundFlushPeriod**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
