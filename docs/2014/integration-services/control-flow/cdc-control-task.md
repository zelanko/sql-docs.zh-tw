---
title: CDC 控制工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.designer.cdccontroltask.f1
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a08279d772cd1274aed41610890290fed1797dd3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035478"
---
# <a name="cdc-control-task"></a>CDC 控制工作
  CDC 控制工作是用來控制異動資料擷取 (CDC) 封裝的開發週期。 它會處理 CDC 封裝與初始載入封裝的同步處理，以及 CDC 封裝執行中所處理之記錄序號 (LSN) 範圍的管理。 此外，CDC 控制工作也會處理錯誤狀況和復原。  
  
 CDC 控制工作在 SSIS 封裝變數中維護 CDC 封裝的狀態，也可以將它保存在資料庫資料表中，以便於跨封裝啟動和在一起執行通用 CDC 處理序的多個封裝之間維護狀態 (例如某個工作可能負責初始載入，而另一個工作則負責滴漏式饋送更新)。  
  
 CDC 控制工作支援兩個作業群組。 一個群組處理初始載入和變更處理的同步處理，另一個群組則管理 CDC 封裝執行期間 LSN 變更處理範圍及追蹤何者已成功處理。  
  
 下列作業會處理初始載入和變更處理的同步處理：  
  
|作業|描述|  
|---------------|-----------------|  
|ResetCdcState|此作業是用來重設與目前 CDC 內容相關聯的永續性 CDC 狀態。 執行此作業之後，LSN 時間戳記 `sys.fn_cdc_get_max_lsn` 資料表中的目前最大 LSN 就會變成下一個處理範圍的範圍開頭。 此作業需要來源資料庫的連接。|  
|MarkInitialLoadStart|在初始載入封裝開始時使用此作業，以便在初始載入封裝開始讀取來源資料表之前記錄來源資料庫中目前的 LSN。 這需要來源資料庫的連接，以呼叫 `sys.fn_cdc_get_max_lsn`。<br /><br /> 如果您在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (亦即，非 Oracle) 上工作時選取了 MarkInitialLoadStart，連線管理員中指定的使用者就必須是 db_owner 或系統管理員。|  
|MarkInitialLoadEnd|在初始載入封裝結束時使用此作業，以便在初始載入封裝完成讀取來源資料表之後記錄來源資料庫中目前的 LSN。 這個 LSN 的決定方式如下：記錄進行此作業時的目前時間，然後在 CDC 資料庫中查詢 `cdc.lsn_time_`mapping 資料表，尋找該時間之後發生的變更。<br /><br /> 如果您在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (亦即，非 Oracle) 上工作時選取了 MarkInitialLoadEnd，連線管理員中指定的使用者就必須是 db_owner 或系統管理員。|  
|MarkCdcStart|此作業是在從快照集資料庫進行初始載入時使用。 在此情況下，變更處理應該在快照集 LSN 之後立即開始。 您可以指定要使用的快照集資料庫名稱，CDC 控制工作就會在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中查詢快照集 LSN。 您還可以選擇直接指定快照集 LSN。<br /><br /> 如果您在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (亦即，非 Oracle) 上工作時選取了 MarkCdcStart，連線管理員中指定的使用者就必須是 db_owner 或系統管理員。|  
  
 下列作業用來管理處理範圍：  
  
|作業|描述|  
|---------------|-----------------|  
|GetProcessingRange|此作業是在叫用使用 CDC 來源資料流程的資料流程之前使用。 叫用此作業時，它會建立 CDC 來源資料流程所讀取的 LSN 範圍。 此範圍會儲存在資料流程處理期間 CDC 來源所使用的 SSIS 封裝變數中。<br /><br /> 如需儲存之狀態的詳細資訊，請參閱 [定義狀態變數](../data-flow/define-a-state-variable.md)。|  
|MarkProcessedRange|在每個 CDC 執行之後 (CDC 資料流程順利完成之後) 執行此作業，以便記錄 CDC 執行期間完整處理的最後一個 LSN。 下次執行 GetProcessingRange 時，這個位置就是下一個處理範圍的開頭。|  
  
## <a name="handling-cdc-state-persistency"></a>處理 CDC 狀態持續性  
 CDC 控制工作會在啟動之間維護永續性狀態。 儲存在 CDC 狀態中的資訊用來決定及維護 CDC 封裝的處理範圍，以及用於偵測錯誤狀態。 永續性狀態儲存為字串。 如需詳細資訊，請參閱 [定義狀態變數](../data-flow/define-a-state-variable.md)。  
  
 CDC 控制工作支援兩種狀態持續性類型。  
  
-   手動狀態持續性：在此情況下，CDC 控制工作會管理儲存在封裝變數中的狀態，但是封裝開發人員必須在呼叫 CDC 控制之前從永續性存放區讀取變數，然後在最後一次呼叫 CDC 控制而且 CDC 執行完成之後將變數寫回該永續性存放區。  
  
-   自動狀態持續性：CDC 狀態會儲存在資料庫資料表中。 此狀態是在 **[要用於儲存狀態的資料表]** 屬性 (位於儲存狀態的選定連接管理員) 所指名資料表中， **StateName** 屬性所提供的名稱下儲存。 預設是來源連接管理員，但常見作法是將它做為目標連接管理員。 CDC 控制工作會更新狀態資料表中的狀態值，並認可此值做為環境交易的一部分。  
  
## <a name="error-handling"></a>錯誤處理  
 在下列情況下，CDC 控制工作可能會報告錯誤：  
  
-   它無法讀取 CDC 永續性狀態或永續性狀態更新失敗。  
  
-   它無法從來源資料庫讀取目前的 LSN 資訊。  
  
-   CDC 狀態讀取不一致。  
  
 在所有這些情況下，CDC 控制工作都會報告錯誤，而 SSIS 則會以處理控制流程錯誤的標準方式予以處理。  
  
 在未呼叫標記處理的範圍的情況下，直接在取得處理範圍作業之後叫用另一個取得處理範圍作業時，CDC 控制工作可能也會報告警告。 這種情況表示上次執行失敗，或者另一個 CDC 封裝可能正在以相同的 CDC 狀態名稱下執行。  
  
## <a name="configuring-the-cdc-control-task"></a>設定 CDC 控制工作  
 您可以透過 SSIS 設計師或以程式設計方式設定屬性。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [CDC 控制工作編輯器](../cdc-control-task-editor.md)  
  
-   [CDC 控制工作自訂屬性](cdc-control-task-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 [定義狀態變數](../data-flow/define-a-state-variable.md)  
  
## <a name="related-content"></a>相關內容  
  
-   social.technet.microsoft.com 上的技術文章： [安裝 Microsoft SQL Server 2012 Change Data Capture for Oracle by Attunity](http://go.microsoft.com/fwlink/?LinkId=252958)。  
  
-   social.technet.microsoft.com 上的技術文章： [疑難排解 Microsoft SQL Server 2012 Change Data Capture for Oracle by Attunity 中的組態問題](http://go.microsoft.com/fwlink/?LinkId=252960)。  
  
-   social.technet.microsoft.com 上的技術文章： [疑難排解 Microsoft SQL Server 2012 Change Data Capture for Oracle by Attunity 中的 CDC 執行個體錯誤](http://go.microsoft.com/fwlink/?LinkId=252961)。  
  
  