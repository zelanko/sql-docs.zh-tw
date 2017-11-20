---
title: "定義狀態變數 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 45d66152-883a-49a7-a877-2e8ab45f8f79
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2ebec44b7492ead6e3417758ac653360f44d4df9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="define-a-state-variable"></a>定義狀態變數
  此程序描述如何定義 CDC 狀態儲存所在的封裝變數。  
  
 CDC 狀態變數是由 CDC 控制工作所載入、初始化及更新，並且由 CDC 來源資料流程元件用來判斷變更記錄目前的處理範圍。 CDC 狀態變數可定義於 CDC 控制工作和 CDC 來源通用的任何容器上。 這可以是在封裝層級，但也可以是在其他容器，如迴圈容器。  
  
 不建議手動修改 CDC 狀態變數值，但這有助於您了解其內容。  
  
 下表提供 CDC 狀態變數值各項元件的進階說明。  
  
|元件|Description|  
|---------------|-----------------|  
|**\<狀態名稱 >**|此為目前 CDC 狀態的名稱。|  
|**CS**|此標示目前處理範圍的起點 (Current Start)。|  
|**\<cs lsn >**|此為上一個 CDC 回合最後處理的 LSN (記錄序號)。|  
|**CE**|此標示目前處理範圍的終點 (Current End)。 CDC 狀態中若存在 CE 元件，代表目前正在處理 CDC 封裝，或是 CDC 封裝在其 CDC 處理範圍未處理完全之前即已失敗。|  
|**\<ce lsn >**|此為目前 CDC 回合要處理的最後一個 LSN。 處理的最後一個序號一律假設為最大值 (0xFFF…)。|  
|**IR**|此標示初始處理範圍。|  
|**\<ir 開始 >**|此為初始載入剛要開始前之異動的 LSN。|  
|**\<ir 端 >**|此為初始載入才剛結束後之異動的 LSN。|  
|**TS**|此標示上次 CDC 狀態更新的時間戳記。|  
|**\<時間戳記 >**|此為 64 位元 System.DateTime.UtcNow 屬性的十進位表示法。|  
|**ER**|此將在上次作業失敗時出現，且包含錯誤原因的簡短描述。 若存在此元件，則其一定出現於最後。|  
|**\<簡短的錯誤文字 >**|此為簡短的錯誤描述。|  
  
 每個 LSN 和序號都是編碼為多達 20 位數的十六進位字串，代表 Binary(10) 的 LSN 值。  
  
 下表描述可能的 CDC 狀態值。  
  
|State|說明|  
|-----------|-----------------|  
|(INITIAL)|這是目前的 CDC 群組上有任何封裝執行之前的初始狀態。 這也是 CDC 狀態為空白時呈現的狀態。|  
|ILSTART (初始載入開始)|這是在 CDC 控制工作的 **MarkInitialLoadStart** 作業呼叫之後，初始載入封裝開始時的狀態。|  
|ILEND (初始載入結束)|這是在 CDC 控制工作的 **MarkInitialLoadEnd** 作業呼叫之後，初始載入封裝順利結束時的狀態。|  
|ILUPDATE (初始載入更新)|這是緊接於初始載入之後而仍在處理初始處理範圍期間執行 Trickle 摘要更新封裝時的狀態。 發生於 CDC 控制工作的 **GetProcessingRange** 作業呼叫之後。<br /><br /> 如果使用了 __$reprocessing 資料行，其值就會設定為 1，表示封裝可能要重新處理已經位於目標上的資料列。|  
|TFEND (Trickle 摘要更新結束)|這是一般 CDC 回合所預期的狀態。 這種狀態表示上一個回合已順利完成，而且可以啟動具有新處理範圍的新回合。|  
|TFSTART|這是 **GetProcessingRange** 作業呼叫在 CDC 控制工作之後，非初次執行 Trickle 摘要更新封裝時的狀態。<br /><br /> 這種狀態表示一般 CDC 回合已啟動，但是沒有完成或者尚未全部完成 (**MarkProcessedRange**)。|  
|TFREDO (重新處理 Trickle 摘要更新)|這是在 TFSTART 之後發生 **GetProcessingRange** 時的狀態。 這種狀態表示上一個回合並未順利完成。<br /><br /> 如果使用了 __$reprocessing 資料行，其值就會設定為 1，表示封裝可能要重新處理已經位於目標上的資料列。|  
|ERROR|CDC 群組處於 ERROR 狀態。|  
  
 以下是 CDC 狀態變數值的範例。  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   TFEND/CS/0x0000025B000001BC0003/TS/2011-07-17T12:05:58.1001145/  
  
-   TFSTART/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:43.9344900/  
  
-   TFREDO/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:59.5544900/  
  
### <a name="to-define-a-cdc-state-variable"></a>若要定義 CDC 狀態變數  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟有需要定義變數之 CDC 流程的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
2.  按一下 **[封裝總管]** 索引標籤，並加入新的變數。  
  
3.  為變數指定可辨識的名稱，做為狀態變數。  
  
4.  為變數指定 **字串** 資料類型。  
  
 不要指定變數值做為其定義的一部分。 此值必須是由 CDC 控制工作所設定。  
  
 如果您打算將 CDC 控制工作與 **[自動狀態持續性]**搭配使用，CDC 狀態變數將會從您指定的資料庫狀態資料表讀取，並在其值變更時更新回該相同的資料表。 如需有關狀態變數的詳細資訊，請參閱＜ [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)＞和＜ [CDC Control Task Editor](../../integration-services/control-flow/cdc-control-task-editor.md)＞。  
  
 如果您不打算將 CDC 控制工作與 [自動狀態持續性] 搭配使用，則必須從上次封裝執行時儲存其值的永續性儲存體中載入變數值，並在目前處理範圍已完成處理時將變數值寫回該永續性儲存體。  
  
## <a name="see-also"></a>另請參閱  
 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)   
 [CDC 控制工作編輯器](../../integration-services/control-flow/cdc-control-task-editor.md)  
  
  

