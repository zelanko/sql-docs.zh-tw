---
title: 記憶體最佳化的系統版本設定時態表效能 | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2e110984-7703-4806-a24b-b41e8c3018c6
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 96897ca8889af1c227e6304a358d0ab2b8154e72
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33006485"
---
# <a name="memory-optimized-system-versioned-temporal-tables-performance"></a>記憶體最佳化的系統版本設定時態表效能
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主題討論使用系統版本設定記憶體最佳化時態表時的一些特定效能考量。  
  
-   當您將系統版本設定加入現有的非時態表時，因為記錄資料表會自動更新，所以預期會有更新和刪除作業的相關效能影響。  
  
-   每項更新和刪除作業都會記錄到內部記憶體最佳化記錄資料表，因此您可能會在工作負載大量使用這兩項作業時，遇到未預期的記憶體耗用量。 為此我們建議您︰  
  
    -   清除空間時，不要從目前的資料表執行大量刪除作業來增加可用的 RAM。 請考慮手動叫用資料清除 (叫用 [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)) 分批刪除資料，或在 **SYSTEM_VERSIONING = OFF**的情況下刪除資料。  
  
    -   不要一次執行大量資料表更新作業，這樣做可能會導致記憶體耗用量是更新非最佳化記憶體時態表所需之記憶體數量的兩倍。 由於資料排清工作會定期執行，以確保內部暫存資料表的記憶體耗用量在預期界限內維持穩定狀態 (約目前時態表記憶體耗用量的 10%)，因此會暫時有兩倍的記憶體耗用量。 請考慮分批或在 **SYSTEM_VERSIONING = OFF**的情況下執行大量更新，例如使用更新設定新加入資料行的預設值。  
  
-   您無法設定啟用資料排清工作的時間，但您可以叫用 [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)的情況下刪除資料。  
  
-   請考慮使用叢集資料行存放區作為磁碟型記錄資料表的儲存選項，尤其是在您打算對使用彙總或視窗型函數的歷程記錄資料執行分析查詢時。 在此情況下，叢集資料行存放區會是記錄資料表的最佳選擇，因為它提供良好的資料壓縮，而且「易於插入」，這與記錄資料表資料的產生方式一致。  
  
## <a name="see-also"></a>另請參閱  
 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [建立記憶體最佳化的系統版本設定時態表](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)   
 [使用記憶體最佳化的系統版本設定時態表](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [監視記憶體最佳化的系統建立版本時態表](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [時態表](../../relational-databases/tables/temporal-tables.md)   
 [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
