---
title: 錯誤處理 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ff79e19d-afca-42a4-81b0-62d759380d11
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a4aebf354f999b26be59efc2f3c25a205dd3d9d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298782"
---
# <a name="error-handling"></a>錯誤處理

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Oracle CDC 執行個體會針對單一 Oracle 來源資料庫中的變更進行採礦處理 (Oracle RAC 叢集會視為單一資料庫)，並將認可的變更寫入目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中 CDC 資料庫內的變更資料表。  
  
 CDC 執行個體會在稱為 **cdc.xdbcdc_state**的系統資料表中維護其狀態。 可以隨時查詢此資料表，以尋找 CDC 執行個體的狀態。 如需 cdc.xdbcdc_state 資料表的詳細資訊，請參閱 [cdc.xdbcdc_state](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state)。  
  
 下表描述 xdbcdc_state 資料表中的 CDC 執行個體狀態。  
  
 對於每個狀態而言，將會針對 cdc.xdbcdc_state 資料表中的對應資料行顯示以下兩個指標：  
  
-   執行個體未在使用中 (目前沒有任何 Windows 處理序正在處理它)。 如果 [使用中]  資料行值為 1，則表示處理這個特定 Oracle CDC 執行個體之 Oracle CDC 服務的子處理序正在執行中。  
  
-   如果 [錯誤]  資料行值為 0，則表示 Oracle CDC 執行個體不在錯誤狀況中。 如果 [錯誤]  資料行值為 1，則表示有錯誤阻止 Oracle CDC 執行個體處理變更。  
  
     如果 [錯誤]  資料行的值為 1 而且 [使用中]  資料行值也是 1，則表示 Oracle CDC 執行個體發生了可以復原的錯誤，而且系統可以自動解決此錯誤。 如果 [錯誤] 資料行的值為 1 而且 [使用中] 資料行的值是 0，則在大多數情況下可能需要採取手動因應措施來解決問題，然後才可以繼續處理。  
  
 下表描述 Oracle CDC 執行個體可能會在其狀態資料表中報告的各種狀態碼。  
  
|狀態|使用中狀態碼|錯誤狀態碼|描述|子狀態|  
|------------|------------------------|-----------------------|-----------------|---------------|  
|ABORTED|0|1|Oracle CDC 執行個體未在執行中。 ABORTED 子狀態表示 Oracle CDC 執行個體為 ACTIVE 狀態然後在未預期的情況下停止。|如果 Oracle CDC 服務偵測到當 Oracle CDC 執行個體於 ACTIVE 狀態下未在執行中時，Oracle CDC 服務的主要執行個體會建立 ABORTED 子狀態。|  
|ERROR|0|1|Oracle CDC 執行個體未在執行中。 ERROR 狀態表示 CDC 執行個體在 ACTIVE 狀態下，然後遇到無法復原的錯誤於是將自己停用。|MISCONFIGURED：偵測到無法復原的組態錯誤。<br /><br /> PASSWORD-REQUIRED：Attunity Oracle Change Data Capture (CDC) 設計工具未設定任何密碼，或是設定的密碼無效。 這可能是因為服務的非對稱金鑰密碼發生變更。|  
|RUNNING|1|0|CDC 執行個體正在執行及處理變更記錄。|IDLE：所有變更記錄都已經處理並儲存在目標控制 ( **_CT**) 資料表中。 控制資料表沒有使用中的交易。<br /><br /> PROCESSING：目前有正在處理但是尚未寫入控制 ( **_CT**) 資料表的變更記錄。|  
|STOPPED|0|0|CDC 執行個體未在執行中。|STOP 子狀態表示 CDC 執行個體為 ACTIVE 狀態然後在正確的情況下停止。|  
|SUSPENDED|1|1|CDC 執行個體正在執行中，但是因為發生可復原的錯誤所以暫停處理。|DISCONNECTED：無法建立與來源 Oracle 資料庫的連接。 一旦還原連接時，處理作業便會繼續。<br /><br /> STORAGE：儲存體已滿。 當有儲存體可用時，處理作業便會繼續。 某些情況下可能不會出現這個狀態，因為無法更新狀態資料表。<br /><br /> LOGGER：記錄器已連接到 Oracle，但是因為暫時性問題所以無法讀取 Oracle 交易記錄。|  
|DATAERROR|x|x|此狀態碼僅用於 **xdbcdc_trace** 資料表。 不會出現在 **xdbcdc_state** 資料表中。 具有此狀態的追蹤記錄表示 Oracle 記錄檔記錄發生問題。 錯誤的記錄檔記錄會儲存在 [資料]  資料行中當做 BLOB。|BADRECORD：無法剖析附加的記錄檔記錄。<br /><br /> CONVERT-ERROR：某些資料行中的資料無法轉換為擷取資料表中的目標資料行。 只有當組態指定轉換錯誤應該產生追蹤記錄時，才可能會出現這個狀態。|  
  
 因為 Oracle CDC 服務狀態會儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，所以資料庫中的狀態值可能不會影響此服務的實際狀態。 最常見的情況是此服務遺失與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連接，而且基於任何理由無法繼續。 在此情況下，儲存在 **cdc.xdbcdc_state** 中的狀態會過時。 如果上次更新時間戳記 (UTC) 已超過一分鐘，則狀態可能已過時。 在此情況下，請使用 Windows 事件檢視器來尋找有關此服務之狀態的其他資訊。  
  
## <a name="error-handling"></a>錯誤處理  
 本節描述 Oracle CDC 服務如何處理錯誤。  
  
### <a name="logging"></a>記錄  
 Oracle CDC 服務會在下列其中一個位置建立錯誤資訊。  
  
-   Windows 事件記錄檔，它會與記錄錯誤功能一起使用，並指示 Oracle CDC 服務生命週期事件 (啟動、停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體或是與它連接或重新連接)。  
  
-   MSXDBCDC.dbo.xdbcdc_trace 資料表，它是由 Oracle CDC 服務主要處理序用於一般記錄和追蹤。  
  
-   \<cdc-database>.cdc.xdbcdc_trace 資料表，它是由 Oracle CDC 執行個體用於一般記錄和追蹤。 這表示與特定 Oracle CDC 執行個體相關之錯誤都會記錄到該執行個體的追蹤資料表。  
  
 當 Oracle CDC 服務在以下情況時會記錄資訊：  
  
-   由服務控制管理員啟動或停止。  
  
-   無法連接到關聯的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，以及在失敗之後隨即成功地建立連接。  
  
-   啟動 Oracle CDC 服務執行個體時遇到錯誤。  
  
-   偵測到 Oracle CDC 執行個體已中止。  
  
-   遇到非預期的錯誤。  
  
 當 CDC 執行個體在以下情況時會記錄資訊：  
  
-   已啟用或停用。  
  
-   遇到錯誤。  
  
-   從可復原的錯誤復原。  
  
 追蹤資料表也用於記錄詳細追蹤資訊，以供疑難排解之用。  
  
### <a name="handling-source-oracle-connection-errors"></a>處理來源 Oracle 連接錯誤  
 Oracle CDC 服務需要具備與來源 Oracle 資料庫之間的持續性連接。 與服務組態不相關的許多連接錯誤 (例如網路錯誤) 會視為暫時性錯誤。 因此，如果 Oracle CDC 服務無法建立與 Oracle 資料庫之間的連接 (不論是在啟動時或是在中斷連接之後工作時)，此服務會將其狀態變更為 SUSPENDED/DISCONNECTED，然後進入重試迴圈 (在此迴圈中會以規律的間隔重試連接)。 當重新建立連接時，處理作業會繼續。  
  
 其他類型的連接錯誤不是暫時性 (例如，認證錯誤、權限不足及資料庫位址錯誤)。 當發生這些錯誤時，Oracle CDC 服務狀態會設定為 ERROR/MISCONFIGURED 或 ERROR/PASSWORD-REQUIRED，而且此服務會停用。 當使用者修正根本錯誤時，應該要手動重新啟用 Oracle CDC 執行個體，處理作業才會繼續。  
  
 如果不清楚錯誤是否為暫時性，最好先假定它是暫時性。  
  
### <a name="handling-target-sql-server-connection-errors"></a>處理目標 SQL Server 連接錯誤  
 Oracle CDC 服務需要具備與目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間的持續性連接。 此連接是用於：  
  
-   確定目前沒有同名的其他服務正在使用這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
-   檢查哪一個 Oracle CDC 執行個體已啟用或停用，並啟動 (或停止) 其子處理序。  
  
 當此服務建立與目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連接，並依據正在使用的這個名稱來驗證它是唯一的 Oracle CDC 服務時，它可以檢查哪些 Oracle CDC 執行個體已啟用，並開始其處理程序 (之後此服務會在這些程序停用時加以停止)。 Oracle CDC 執行個體會使用其 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接來處理 Oracle CDC 執行個體的 CDC 資料庫。  
  
 在連接目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 失敗時處理錯誤的方式取決於錯誤是否為暫時性。  
  
 如果是已知的非暫時性錯誤 (例如認證錯誤、權限不足、連接資訊錯誤)，此服務會將錯誤記錄到 Windows 事件記錄檔然後停止 (它無法寫入追蹤資料表，因為它無法連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。 在這個案例中，使用者必須解決此錯誤，並重新啟動 Oracle CDC Windows 服務。  
  
 如果是暫時性錯誤和非預期的錯誤，則會重試此作業數次，而且如果失敗持續一段很長的時間，CDC 服務會停止其 CDC 執行個體子處理序，並回到最初的連接嘗試 (這時候，另一部電腦上的 Oracle CDC 服務可能已經取得具名 CDC 服務的控制權)。  
  
### <a name="handling-target-sql-server-storage-full-errors"></a>處理目標 SQL Server 儲存體已滿的錯誤  
 當 Oracle CDC 服務偵測到它無法將新的變更資料插入目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 執行個體時，它會將一則警告寫入事件記錄檔，並嘗試插入追蹤記錄 (雖然可能會因為同樣的原因而失敗)。 然後它會以特定間隔重試作業，直到成功為止。  
  
### <a name="handling-oracle-cdc-errors"></a>處理 Oracle CDC 錯誤  
 Oracle CDC 執行個體會讀取 Oracle 交易記錄並進行處理。 如果 CDC 處理遇到錯誤，則會在 **cdc.xdbcdc_state** 資料表中報告此錯誤，而且使用者需要根據報告的錯誤來手動介入。  
  
 例如，Oracle CDC 執行個體可能有一段期間沒有活動，而且必要的 Oracle 交易記錄檔案不再可用。 在此情況下，Oracle DBA 必須還原必要的記錄，Oracle CDC 執行個體才能繼續處理。  
  
### <a name="handling-unexpected-oracle-cdc-instance-failures"></a>處理非預期的 Oracle CDC 執行個體失敗  
 Oracle CDC 服務會監視其 CDC 執行個體子處理序。 當 CDC 執行個體子處理序中止時，CDC 服務會在 MSXDBCDC.dbo.xdbcdc_databases 資料表中停用它，並將其 cdc.xdbcdc_state 狀態更新為 ABORTED。 在此情況下，標準 Windows 錯誤報告對話方塊會用來報告這個錯誤，以供進一步分析。  
  
## <a name="see-also"></a>另請參閱  
 [Attunity Oracle 異動資料擷取設計工具](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [Oracle CDC 執行個體](../../integration-services/change-data-capture/the-oracle-cdc-instance.md)  
  
  
