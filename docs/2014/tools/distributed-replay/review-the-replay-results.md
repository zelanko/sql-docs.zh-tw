---
title: 查看重新執行結果 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: da999781-f0ff-47eb-ba7a-09c0ed8f61ad
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b81d4e1aeb2192e6a32a34bed74b9cd55a1cb9a9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63149699"
---
# <a name="review-the-replay-results"></a>檢閱重新執行結果
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributed Replay 功能完成分散式重新執行之後，即可擷取每個用戶端的重新執行活動，並將其儲存在每個用戶端的結果追蹤檔案中。 若要擷取此活動，您必須在以 **replay** 選項執行管理工具時使用 **-o** 參數。 如需詳細資訊，請參閱[重新執行選項 &#40;Distributed Replay 管理工具&#41;](replay-option-distributed-replay-administration-tool.md)。  
  
 結果追蹤檔案的儲存位置是由每個用戶端上用戶端組態檔 `<ResultDirectory>` 中的 `DReplayClient.xml`XML 元素所指定。 每次重新執行時都會覆寫用戶端結果目錄中的追蹤檔案。  
  
 若要指定結果追蹤檔案中應該擷取何種輸出，請修改重新執行組態檔 `DReplay.exe.replay.config`。 您可以使用 `<OutputOptions>` XML 項目來指定是否應該記錄資料列計數或結果集內容。  
  
 如需這些執行組態檔設定的詳細資訊，請參閱 [Configure Distributed Replay](configure-distributed-replay.md)(設定 Distributed Replay)。  
  
## <a name="event-classes-captured-in-result-trace-files"></a>結果追蹤檔案中擷取的事件類別  
 下表列出結果追蹤資料中擷取的所有事件類別。  
  
|類別|EventClass 名稱|擷取頻率|擷取點|  
|--------------|---------------------|-----------------------|----------------------|  
|可重新執行的事件|稽核登入|原始追蹤資料中每個 Audit Login 事件一次|在事件成功完成或失敗時。|  
||稽核登出|原始追蹤資料中每個 Audit Logout 事件一次|在事件成功完成或失敗時。|  
||SQL:BatchCompleted|原始追蹤資料中每個 SQL:BatchStarting 事件一次|在事件成功完成或失敗時。|  
||RPC:Completed|原始追蹤資料中每個 RPC:Starting 事件一次|在事件成功完成或失敗時。|  
|統計資料和結果|Replay Settings Event|一次性|結果追蹤的第一個事件|  
||Replay Statistics Event|一次性|結果追蹤的最後一個事件|  
||Replay Result Set Event|每個 SQL:BatchStarting 和 RPC:Starting 事件一次。<br /><br /> 只有在重新執行組態檔中 `<RecordResultSet>` 選項的值設為 `Yes`時才擷取。||  
||Replay Result Row Event|SQL:BatchStarting 和 RPC:Starting 事件結果集中的每個資料列一次。<br /><br /> 只有在重新執行組態檔中 `<RecordResultSet>` 選項的值設為 `Yes`時才擷取。||  
|錯誤和警告|Replay Internal Error|每個內部錯誤一次|在發生內部錯誤狀況時|  
||Replay Provider Error|每個提供者錯誤一次|在發生提供者錯誤狀況時|  
  
 請注意：  
  
-   在目標伺服器上每個順利重新執行的事件都有一個對應的輸出事件類別。  
  
-   每個事件失敗或取消時，可能會產生多個錯誤。  
  
## <a name="event-class-column-mapping"></a>事件類別資料行對應  
 下圖列出結果追蹤的哪些資料行可用於重新執行期間所擷取的每種事件類別。  
  
 ![事件類別資料行對應](../../database-engine/media/eventclassmappings.gif "事件類別資料行對應")  
  
## <a name="column-descriptions-for-result-trace"></a>結果追蹤的資料行說明  
 下表描述結果追蹤資料的資料行。  
  
|資料行名稱|資料類型|描述|資料行識別碼|  
|----------------------|---------------|-----------------|---------------|  
|EventClass|`nvarchar`|事件類別的名稱。|1|  
|EventSequence|`bigint`|針對提供者錯誤以及內部錯誤和警告，這是對應於錯誤或警告的擷取事件順序。<br /><br /> 針對所有其他事件類別，這是原始追蹤資料中的事件順序。|2|  
|ReplaySequence|`bigint`|針對提供者錯誤以及內部錯誤和警告，這是對應於錯誤或警告的重新執行事件順序。<br /><br /> 針對所有其他事件類別，這是重新執行期間指派的事件順序。|3|  
|TextData|`ntext`|TextData 的內容取決於 EventClass。<br /><br /> 針對 Audit Login 和 ExistingConnection，這是連接的設定選項。<br /><br /> 針對 SQL:BatchStarting，這是批次要求的主體。<br /><br /> 針對 RPC:Starting，這是呼叫的預存程序。<br /><br /> 針對 Replay Settings Event，此資料行包含重新執行組態檔中所定義的設定。<br /><br /> 針對 Replay Statistics Event，這包含下列資訊：<br />重新執行目標 SQL Server<br />可重新執行的事件總數<br />提供者錯誤數目<br />內部錯誤數目<br />內部警告<br />錯誤總數<br />整體成功率<br />重新執行時間 (HH:MM:SS:MMM)<br /><br /> 針對 Replay Result Set Event，這會顯示傳回結果資料行標頭的清單。<br /><br /> 針對 Replay Result Row Event，這會顯示該資料列所有資料行的傳回值。<br /><br /> 針對 Replay Internal Warning 和 Replay Provider Error，此資料行包含提供者警告或錯誤。|4|  
|Attention|`bigint`|事件的注意事項持續期間 (毫秒)。 這是從擷取追蹤的注意事項事件計算出來。 如果沒有指定事件的查詢逾時，此資料行不會擴展 (Null)。|5|  
|SubmitTime|`datetime`|事件提交至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的時間。|6|  
|IsSuccessful|`int`|布林旗標，指出特定事件是否已成功執行，而且結果集傳回至用戶端。<br /><br /> 產生警告的事件 (例如因為注意事項或使用者指定逾時而取消事件時) 會被視為成功。<br /><br /> IsSuccessful 可以是下列其中一個值：<br /><br /> 1 = 成功<br /><br /> 0 = 失敗|7|  
|Duration [microsec]|`bigint`|事件的回應持續期間 (毫秒)。 從登入/登出/RPC/語言事件提交至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時開始測量。<br /><br /> 如果事件成功，則會在已耗用完整的結果集時結束測量。<br /><br /> 如果事件不成功，則會在事件失敗或取消時結束測量。|8|  
|RowCount|`bigint`|依據重新執行組態檔中 `<RecordRowCount>` 的值而擴展：<br /><br /> 如果 `<RecordRowCount>` 等於 Yes，此資料格包含結果集中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]所傳回的資料列數目。<br /><br /> 如果 `<RecordRowCount>` 等於 No，此儲存格不會擴展 (Null)。|9|  
|CaptureSPID|`int`|事件的擷取工作階段識別碼。|10|  
|ConnectionID|`int`|事件的擷取連接識別碼。|11|  
|ReplaySPID|`int`|事件的重新執行工作階段識別碼。|12|  
|DatabaseName|`nvarchar`|正在其中執行使用者陳述式的資料庫名稱。|13|  
|LoginName|`nvarchar`|使用者登入名稱。 這可以是[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安全性登入或 Microsoft Windows 登入認證，格式*domain_name*\\*user_name*。|14|  
|CaptureHostName|`nvarchar`|擷取期間用戶端服務執行所在之電腦的名稱。|15|  
|ReplayHostName|`nvarchar`|重新執行期間用戶端執行所在的電腦名稱。|16|  
|ApplicationName|`nvarchar`|擷取期間建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 連線的用戶端應用程式名稱。|17|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Distributed Replay 需求](distributed-replay-requirements.md)   
 [系統管理工具命令列選項 &#40;Distributed Replay 公用程式&#41;](administration-tool-command-line-options-distributed-replay-utility.md)   
 [設定 Distributed Replay](configure-distributed-replay.md)  
  
  
