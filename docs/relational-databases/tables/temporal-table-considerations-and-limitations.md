---
title: "時態表考量與限制 | Microsoft Docs"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8a21481-0f0e-41e3-a1ad-49a84091b422
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 30791ad9733446f664db1592b95d1ffec5fc9a1b
ms.openlocfilehash: 5ee3aa9223ae8ab832eff23a1da1755278e86d0b
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="temporal-table-considerations-and-limitations"></a>時態表考量與限制
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  使用時態表時由於系統版本性質使然，因此需要瞭解某些考量與限制。  
  
 當您使用時態表時，請考量以下事項。  
  
-   時態表必須具有定義的主索引鍵，以將目前資料表與歷程記錄資料表的記錄相互關聯，且歷程記錄資料表不可具有定義的主索引鍵。  
  
-   記錄 **SysStartTime** 和 **SysEndTime** 值所用的 SYSTEM_TIME 期間資料行，必須使用 datetime2 的資料類型加以定義。  
  
-   若在建立歷程記錄資料表時指定歷程記錄資料表名稱，則您必須指定結構描述和資料表名稱。  
  
-   根據預設，歷程記錄資料表會採 **PAGE** 壓縮處理。  
  
-   若目前的資料表已分割，則會在預設檔案群組上建立歷程記錄資料表，這是因為資料分割設定不會自動從目前的資料表複寫至歷程記錄資料表。  
  
-   時態表與歷程記錄資料表不可為 **FILETABLE** ，且會包含 **FILESTREAM** 以外所有受支援的資料類型資料行，這是因為 **FILETABLE** 和 **FILESTREAM** 允許在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之外操作資料，以致無法保證系統版本設定。  
  
-   時態表支援 Blob 資料類型 (例如 **(n)varchar(max)**、**varbinary(max)**、**(n)text** 和 **image**)，但會產生龐大的儲存成本，且其大小會影響效能。 因此您在設計系統時，應小心使用這些資料類型。  
  
-   歷程記錄資料表必須建立於與目前資料表相同的資料庫中。 不支援針對 **Linked Server** 的時態查詢。  
  
-   歷程記錄資料表不可具有條件約束 (主索引鍵、外部索引鍵、資料表或資料行條件約束)。  
  
-   不支援在時態查詢 (使用 **FOR SYSTEM_TIME** 子句的查詢) 上方的索引檢視表  
  
-   若為系統版本設定時態表，ONLINE 選項 (**WITH (ONLINE = ON**) 對 **ALTER TABLE ALTER COLUMN** 無效。 無論針對 ONLINE 選項指定何值，皆不會將 ALTER 資料行執行為線上。  
  
-   **INSERT** 和 **UPDATE** 陳述式無法參考 SYSTEM_TIME 期間資料行。 若嘗試將值直接插入這些資料行，則會遭到系統封鎖。  
  
-   當**TRUNCATE TABLE** 為 **TRUNCATE TABLE** 時，不支援 **TRUNCATE TABLE**。  
  
-   不允許直接修改歷程記錄資料表中的資料。  
  
-   **ON DELETE CASCADE** 和 **ON UPDATE CASCADE** 不得位於目前資料表。 換言之，若時態表參考外部索引鍵關係中的資料表 (對應至 sys.foreign_keys 中的 *parent_object_id* )，則不允許 CASCADE 選項。 若要解決此限制，請使用應用程式邏輯或 after 觸發程序，以維持在主索引鍵資料表執行刪除的一致性 (對應至 sys.foreign_keys 中的  *referenced_object_id* )。 若主索引鍵資料表為時態，且參考資料表為非時態，則不會有這些限制。 

    **注意：**這項限制僅適用於 SQL Server 2016。 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 和 SQL Server 2017 (從 CTP 2.0 開始) 支援 CASCADE 選項。  
  
-   目前或歷程記錄資料表不允許使用**INSTEAD OF** 觸發程序，以避免使 DML 邏輯無效。 **AFTER** 觸發程序僅允許針對目前的資料表使用。 這些觸發程序在歷程記錄資料表上會遭到封鎖，以避免使 DML 邏輯無效。  
  
-   複寫技術的使用會受到限制。  
  
    -   **Always On：** 完全支援  
  
    -   **異動資料擷取和變更資料追蹤︰** 僅支援目前的資料表  
  
    -   **快照集與異動複寫**：僅支援未啟用時態的單一發行者，以及已啟用時態的單一訂閱者。 在此情況下，當訂閱者執行卸載報表時會針對 OLTP 工作負載使用發行者 (包括 ‘AS OF’ 查詢)。    
        不支援使用多位訂閱者，這是因為在此案例中每個時態資料皆取決於本機系統時鐘，因此會導致這些資料出現不一致。  
  
    -   **合併式複寫︰** 不支援時態表  
  
-   一般查詢只會影響目前資料表中的資料。 若要查詢歷程記錄資料表中的資料，您必須使用時態查詢。 我們會在本文件後面的＜查詢時態資料＞一節中加以詳述。  
  
-   最佳的索引策略，是在目前的資料表上加入叢集資料行存放區索引和/或 B 型樹狀結構資料列存放區索引，以及在歷程記錄資料表上加入叢集資料行存放區索引，藉以取得最佳儲存大小和效能。 若您建立 / 使用專屬的歷程記錄資料表，強烈建議您建立由期間資料行組成的索引類型，其會以期間資料行結尾開頭來加速 時態查詢，並可加速屬於資料一致性檢查作業的查詢。 預設的歷程記錄資料表已根據期間資料行 (結尾、開頭)，為您建立叢集資料列存放區索引。 至少建議您使用非叢集資料列存放區索引。  
  
-   建立歷程記錄資料表時，下列物件/屬性不會從目前資料表複寫至歷程記錄資料表  
  
    -   期間定義  
  
    -   識別定義  
  
    -   索引  
  
    -   Statistics  
  
    -   檢查條件約束  
  
    -   觸發程序  
  
    -   資料分割設定  
  
    -   Permissions  
  
    -   資料列層級安全性述詞  
  
-   歷程記錄資料表不可設定為一連串歷程記錄資料表中的目前資料表。  
  
## <a name="did-this-article-help-you-were-listening"></a>這篇文章對您有幫助嗎？ 我們會持續聽取您的意見  
 您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請將您的意見傳送到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Table%20Considerations%20and%20Limitations%20page)  
  
## <a name="see-also"></a>另請參閱  
 [時態表](../../relational-databases/tables/temporal-tables.md)   
 [開始使用系統建立版本的時態表](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [對時態表進行資料分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [時態表安全性](../../relational-databases/tables/temporal-table-security.md)   
 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

