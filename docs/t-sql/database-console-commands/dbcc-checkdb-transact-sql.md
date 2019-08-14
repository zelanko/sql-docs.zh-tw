---
title: DBCC CHECKDB (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKDB_TSQL
- DBCC_CHECKDB_TSQL
- DBCC CHECKDB
- CHECKDB
dev_langs:
- TSQL
helpviewer_keywords:
- CHECKDB [DBCC statement]
- database objects [SQL Server], checking
- counting pages
- per-index row counts
- per-table row counts
- DBCC CHECKDB statement
- per-table page counts
- allocation checks
- integrity [SQL Server], database objects
- per-index page counts
- counting rows
- table integrity checks [SQL Server]
- row count accuracy [SQL Server]
- negative counts
- checking database objects
- page count accuracy [SQL Server]
ms.assetid: 2c506167-0b69-49f7-9282-241e411910df
author: pmasl
ms.author: umajay
ms.openlocfilehash: 15c1fc0789ff665569ed17be9415bdbdd8047714
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809897"
---
# <a name="dbcc-checkdb-transact-sql"></a>DBCC CHECKDB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

藉由執行下列作業，檢查指定資料庫中所有物件的邏輯完整性和實體完整性：    
    
-   對資料庫執行 [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)。    
-   對資料庫中每一資料表和檢視執行 [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)。    
-   對資料庫執行 [DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)。    
-   驗證資料庫中每一索引檢視的內容。    
-   當使用 FILESTREAM 將 **varbinary(max)** 資料儲存在檔案系統中時，驗證資料表中繼資料與檔案系統目錄和檔案之間的連結層級一致性。    
-   驗證資料庫中的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 資料。    
    
這表示 DBCC CHECKALLOC、DBCC CHECKTABLE 或 DBCC CHECKCATALOG 命令不需要與 DBCC CHECKDB 分開獨立執行。 如需有關這些命令執行之檢查的詳細資訊，請參閱這些命令的描述。    
 
> [!NOTE]
> 在包含記憶體最佳化資料表的資料庫中，可支援 DBCC CHECKDB，但是只會在磁碟資料表上進行驗證。 不過，在資料庫備份和復原的過程中，會針對記憶體最佳化檔案群組中的檔案執行 CHECKSUM 驗證。    
>     
> 因為 DBCC 修復選項無法用於記憶體最佳化資料表，所以您必須定期備份資料庫，並測試備份。 如果記憶體最佳化資料表中發生資料完整性問題，您必須從最後已知的良好備份還原。    

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>語法    
    
```    
DBCC CHECKDB     
    [ ( database_name | database_id | 0    
        [ , NOINDEX     
        | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]    
    ) ]    
    [ WITH     
        {    
            [ ALL_ERRORMSGS ]    
            [ , EXTENDED_LOGICAL_CHECKS ]     
            [ , NO_INFOMSGS ]    
            [ , TABLOCK ]    
            [ , ESTIMATEONLY ]    
            [ , { PHYSICAL_ONLY | DATA_PURITY } ]    
            [ , MAXDOP  = number_of_processors ]    
        }    
    ]    
]    
```    
    
## <a name="arguments"></a>引數    
 *database_name* | *database_id* | 0  
 這是要執行完整性檢查的資料庫識別碼或名稱。 若未指定，或指定 0，就會使用目前的資料庫。 資料庫名稱必須符合[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。  
    
NOINDEX  
 指定不應該執行使用者資料表之非叢集索引的大量檢查。 這會減少整體的執行時間。 NOINDEX 不會影響系統資料表，因為系統資料表索引一律會執行完整性檢查。  
    
REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 指定 DBCC CHECKDB 修復發現的錯誤。 最好不要使用這些 REPAIR 選項。 指定的資料庫必須為單一使用者模式，才能使用下列修復選項之一。  
    
REPAIR_ALLOW_DATA_LOSS  
 嘗試修復所有報告的錯誤。 這些修復可能會造成某些資料的遺失。  
    
> [!WARNING]
> REPAIR_ALLOW_DATA_LOSS 選項是支援的功能，但不一定是讓資料庫處於實體一致狀態的最佳選項。 如果成功的話，REPAIR_ALLOW_DATA_LOSS 選項可能會導致部分資料遺失。 事實上，這個選項遺失的資料，可能會比使用者從上次已知良好備份還原資料庫所遺失的資料多。 
>
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一律建議使用者從上次已知良好的備份還原，做為修復 DBCC CHECKDB 所報告之錯誤的主要方法。 REPAIR_ALLOW_DATA_LOSS 選項無法取代從已知良好的備份還原方法。 只有在不可能從備份還原時，才建議使用這個「上次還原」緊急選項。    
>     
> 某些只能透過 REPAIR_ALLOW_DATA_LOSS 選項修復的錯誤，可能需要取消配置資料列、頁面或一系列頁面，才能清除錯誤。 使用者將無法再存取或復原任何已取消配置的資料，也無法判斷其確切內容。 因此，取消配置任何資料列或頁面之後，參考完整性可能會不正確，因為在這項修復作業期間不會檢查或維護外部索引鍵條件約束。 使用者在使用 REPAIR_ALLOW_DATA_LOSS 選項之後，必須檢查其資料庫的參考完整性 (使用 DBCC CHECKCONSTRAINTS)。    
>     
> 在執行修復之前，請建立屬於這個資料庫的檔案實體複本。 這包括主要資料檔 (.mdf)、任何次要資料檔 (.ndf)、所有交易記錄檔 (.ldf) 以及其他構成資料庫的容器，包括全文檢索目錄、檔案資料流資料夾、記憶體最佳化的資料等。    
>     
> 在執行修復之前，請考慮將資料庫的狀態變更為「緊急」模式，並嘗試從關鍵資料表中擷取盡可能最多的資訊，然後儲存該資料。    
    
REPAIR_FAST  
 維護這個語法的目的，只是為了與舊版相容。 不會執行任何修復動作。  
    
REPAIR_REBUILD  
 執行不可能造成資料遺失的修復， 這可包括快速修復 (例如，修復非叢集索引中遺失的資料列) 以及更耗時的修復 (例如，重建索引)。  
 此引數不會修復涉及 FILESTREAM 資料的錯誤。  
    
> [!IMPORTANT] 
> 由於搭配任何 REPAIR 選項的 DBCC CHECKDB 已完整記錄下來並可復原，因此 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一律會建議使用者在交易內 (執行命令前先執行 BEGIN TRANSACTION) 搭配任何 REPAIR 選項使用 CHECKDB，以便使用者可以確認要接受作業的結果。 接著使用者可執行 COMMIT TRANSACTION，來認可修復作業完成的所有工作。 如果使用者不想接受作業的結果，可執行 ROLLBACK TRANSACTION 恢復修復作業的結果。    
>     
> 若要修復錯誤，我們建議您從備份中還原。 修復作業並不考慮資料表或資料表之間的任何條件約束。 如果指定的資料表涉及一或多項條件約束，建議您在修復作業之後，執行 DBCC CHECKCONSTRAINTS。 如果您必須使用 REPAIR，請執行不含修復選項的 DBCC CHECKDB 來尋找要使用的修復層級。 如果您使用 REPAIR_ALLOW_DATA_LOSS 層級，建議您在搭配這個選項執行 DBCC CHECKDB 之前，先備份資料庫。    
    
ALL_ERRORMSGS  
 根據每個物件顯示所有報告的錯誤。 系統預設會顯示所有錯誤訊息。 指定或省略這個選項沒有任何作用。 錯誤訊息是依物件識別碼排序，但從 [tempdb 資料庫](../../relational-databases/databases/tempdb-database.md)產生的訊息除外。     

EXTENDED_LOGICAL_CHECKS  
 如果相容性層級為 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 或更高，則會針對索引檢視表、XML 索引和空間索引 (如果有的話) 執行邏輯一致性檢查。  
 如需詳細資訊，請參閱本主題稍後[備註](#remarks)一節中的＜對索引執行邏輯一致性檢查＞  。  
    
NO_INFOMSGS  
 隱藏所有參考訊息。  
    
TABLOCK  
 使 DBCC CHECKDB 取得鎖定，而不使用內部資料庫快照集。 這包括資料庫上的短期獨佔 (X) 鎖定。 TABLOCK 可讓 DBCC CHECKDB 在負載沉重的資料庫上執行得快一些，但 DBCC CHECKDB 執行時，資料庫可用的並行會降低。  
    
> [!IMPORTANT] 
> TABLOCK 會限制執行的檢查；不會對資料庫執行 DBCC CHECKCATALOG，也不會驗證 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 資料。
    
ESTIMATEONLY  
 顯示搭配所有其他指定的選項來執行 DBCC CHECKDB 所需要的 tempdb 估計空間量。 不會執行實際的資料庫檢查。  
    
PHYSICAL_ONLY  
 將檢查限制於頁面實體結構、記錄標頭的完整性，以及資料庫配置的一致性。 這是設計來對資料庫實體一致性提供少量負擔檢查，這項檢查還能偵測到可能危及使用者資料的損毀頁、總和檢查碼失敗以及常見的硬體錯誤。  
 完整執行 DBCC CHECKDB 所需要的完成時間可能比舊版長許多。 此行為的發生狀況如下：  
 -   邏輯檢查更完整。  
 -   部分要檢查的基礎結構更複雜。  
 -   導入了許多新的檢查，以包含新的功能。  
 因此，使用 PHYSICAL_ONLY 選項可能使 DBCC CHECKDB 對大型資料庫的執行階段縮短許多，因此，建議您在實際系統上經常使用它。 我們仍建議您定期完整執行 DBCC CHECKDB。 這些執行動作的頻率取決於個別商務和實際執行環境特有的因素。    
此引數一律隱含 NO_INFOMSGS，且不允許搭配任何修復選項使用。  
    
> [!WARNING] 
> 指定 PHYSICAL_ONLY 會造成 DBCC CHECKDB 略過 FILESTREAM 資料的所有檢查。
    
DATA_PURITY  
 使 DBCC CHECKDB 檢查資料庫，找出無效或超出範圍的資料行值。 例如，DBCC CHECKDB 會偵測具有大於或小於 **datetime** 資料類型可接受範圍之日期和時間值的資料行；或是 **decimal** 或近似數值資料類型資料行具有無效的小數位數或有效位數值。  
 預設會啟用資料行值的完整性檢查，而不需要 DATA_PURITY 選項。 對於從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級的資料庫，在毫無錯誤的情況下完成對資料庫執行 DBCC CHECKDB WITH DATA_PURITY 之前，依預設不啟用資料行值的完整性檢查。 此後，依預設 DBCC CHECKDB 會檢查資料行值的完整性。 如需有關從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級資料庫可能對 CHECKDB 造成何種影響的詳細資訊，請參閱本主題稍後的「備註」一節。  
    
> [!WARNING]
> 如果指定 PHYSICAL_ONLY，則不會執行資料行完整性檢查。
    
 這個選項報告的驗證錯誤無法使用 DBCC 修復選項更正。 如需手動更正這些錯誤的相關資訊，請參閱知識庫文章 923247：[針對 SQL Server 2005 和更新版本中的 DBCC 錯誤 2570 進行疑難排解](https://support.microsoft.com/kb/923247)。  
    
 MAXDOP  
 **適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。  
    
 覆寫陳述式之 **sp_configure** 的 **max degree of parallelism** 設定選項。 MAXDOP 可能會超過使用 sp_configure 所設定的值。 如果 MAXDOP 超過使用 Resource Governor 所設定的值，[!INCLUDE[ssDEnoversion](../../includes/ssDEnoversion_md.md)] 就會使用 [ALTER WORKLOAD GROUP](../../t-sql/statements/alter-workload-group-transact-sql.md) 中所描述的 Resource Governor MAXDOP 值。 當您使用 MAXDOP 查詢提示時，適用所有搭配 max degree of parallelism 組態選項使用的語意規則。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
 
> [!WARNING] 
> 如果 MAXDOP 設定為零，SQL Server 會選擇要使用之平行處理原則的最大程度。    

## <a name="remarks"></a>Remarks    
DBCC CHECKDB 不會檢查停用的索引。 如需詳細資訊，請參閱[停用索引和條件約束](../../relational-databases/indexes/disable-indexes-and-constraints.md)。    

如果使用者定義型別標示為按位元組排序，該使用者定義型別只能有一個序列。 按位元組排序之使用者定義型別如果沒有一致的序列，DBCC CHECKDB 執行期間將會發生錯誤 2537。 如需詳細資訊，請參閱[使用者定義類型需求](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-requirements.md)。    

因為[資源資料庫](../../relational-databases/databases/resource-database.md)只能在單一使用者模式中進行修改，因此無法直接對其執行 DBCC CHECKDB 命令。 然而，針對 [master 資料庫](../../relational-databases/databases/master-database.md)執行 DBCC CHECKDB 時，在內部也會對 Resource 資料庫執行第二個 CHECKDB。 這表示 DBCC CHECKDB 可能會傳回額外的結果。 這個命令在未設定選項或僅設定 `PHYSICAL_ONLY` 或 `ESTIMATEONLY` 選項其中之一時，會傳回額外的結果集。    

從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2 開始，執行 DBCC CHECKDB **不會再**清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的計畫快取。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2 之前，執行 DBCC CHECKDB 會清除計畫快取。 清除計畫快取會導致重新編譯所有後續執行計畫，而且可能會導致查詢效能突然暫時下降。 
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>對索引執行邏輯一致性檢查    
對索引進行的邏輯一致性檢查會根據資料庫的相容性層級而異，如下所示：
-   如果相容性層級為 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 或更高：    
-   除非指定了 `NOINDEX`，否則 DBCC CHECKDB 會針對單一資料表及它的所有非叢集索引進行實體和邏輯一致性檢查。 但是根據預設，XML 索引、空間索引和索引檢視表只會進行實體一致性檢查。
-   如果指定了 `WITH EXTENDED_LOGICAL_CHECKS`，將會針對索引檢視表、XML 索引和空間索引 (如果有的話) 執行邏輯檢查。 根據預設，實體一致性檢查會在邏輯一致性檢查之前執行。 如果也指定了 `NOINDEX`，則只會執行邏輯檢查。
    
這些邏輯一致性檢查會交叉檢查索引物件的內部索引資料表 (其中包含它所參考的使用者資料表)。 若要尋找外圍的資料列，則會建構內部查詢來執行內部和使用者資料表的完整交集。 執行這個查詢對於效能會有極大的影響，而且無法追蹤其進度。 因此，只有當您懷疑發生了與實體損毀無關的索引問題，或是頁面層級總和檢查碼已經關閉，而且您懷疑發生了資料行層級的硬體損毀時，才建議您指定 `WITH EXTENDED_LOGICAL_CHECKS`。
-   如果此索引為已篩選的索引，DBCC CHECKDB 會執行一致性檢查，以確認索引項目可滿足篩選述詞。
-   如果相容性層級為 90 以下，則除非指定了 `NOINDEX`，否則 DBCC CHECKDB 會針對單一資料表或索引檢視表及它的所有非叢集索引和 XML 索引進行實體和邏輯一致性檢查。 不支援空間索引。  
- 從 SQL Server 2016 開始，預設不會針對保存的計算資料行、UDT 資料行和篩選的索引上執行額外檢查，以避免需耗費大量資源的運算式評估作業。 這項變更可大幅減少對包含這些物件的資料庫執行 CHECKDB 的持續時間。 不過，系統一律會完成這些物件的實體一致性檢查。 只有在指定 `EXTENDED_LOGICAL_CHECKS` 選項時，才會執行運算式評估，以及執行 `EXTENDED_LOGICAL_CHECKS` 選項中已存在的邏輯性檢查 (索引檢視表、XML 索引及空間索引)。   
    
**了解資料庫的相容性層級**
-   [檢視或變更資料庫的相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>內部資料庫快照集    
DBCC CHECKDB 使用內部資料庫快照集來維護執行這些檢查時所需的交易一致性。 這可以防止在執行這些命令時，發生封鎖和並行問題。 如需詳細資訊，請參閱[檢視資料庫快照集的疏鬆檔案大小 &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) 和 [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md) 中的＜DBCC 內部資料庫快照集使用方式＞一節。 如果無法建立快照集，或指定了 TABLOCK，則 DBCC CHECKDB 會獲取鎖定來取得必要的一致性。 在這個情況下，則需要獨佔資料庫鎖定，才能執行配置檢查，而且需要共用資料表鎖定，才能執行資料表檢查。
如果無法建立內部資料庫快照集，針對 master 執行 DBCC CHECKDB 將會失敗。
針對 tempdb 執行 DBCC CHECKDB 並不會執行任何配置或目錄檢查，且需要取得共用資料表鎖定來執行資料表檢查。 這是因為基於效能的考量，tempdb 並無法使用資料庫快照集。 這表示無法取得必要的交易一致性。
在 Microsoft SQL Server 2012 或舊版的 SQL Server 中，您在針對檔案位於 ReFS 格式磁碟區上的資料庫執行 DBCC CHECKDB 命令時，可能會遇到錯誤訊息。 如需詳細資訊，請參閱知識庫文章 2974455：[DBCC CHECKDB behavior when the SQL Server database is located on an ReFS volume](https://support.microsoft.com/kb/2974455) (SQL Server 資料庫位於 ReFS 磁碟區時的 DBCC CHECKDB 行為)。    
    
## <a name="checking-and-repairing-filestream-data"></a>檢查及修復 FILESTREAM 資料    
針對資料庫和資料表啟用 FILESTREAM 時，您可以選擇將 **varbinary(max)** 二進位大型物件 (BLOB) 儲存在檔案系統中。 當您針對將 BLOB 儲存於檔案系統中的資料庫使用 DBCC CHECKDB 時，DBCC 會檢查檔案系統與資料庫之間的連結層級一致性。
例如，如果資料表包含使用 FILESTREAM 屬性的 **varbinary(max)** 資料行，DBCC CHECKDB 將會檢查檔案系統目錄和檔案與資料表資料列、資料行和資料行值之間是否有一對一的對應。 如果您指定 REPAIR_ALLOW_DATA_LOSS 選項，則 DBCC CHECKDB 可以修復損毀。 為了修復 FILESTREAM 損毀，DBCC 將刪除遺失檔案系統資料的任何資料表資料列。
    
## <a name="best-practices"></a>最佳作法    
我們建議您在生產環境系統上，使用 `PHYSICAL_ONLY` 選項作為常用的選項。 使用 PHYSICAL_ONLY 可以大幅縮減在大型資料庫上執行 DBCC CHECKDB 所需的時間。 我們也建議您不搭配使用任何選項，定期執行 DBCC CHECKDB。 執行這些作業的頻率是依個別公司及其實際執行環境而定。
    
## <a name="checking-objects-in-parallel"></a>平行檢查物件    
依預設，DBCC CHECKDB 會執行物件的平行檢查。 查詢處理器會自動判斷平行處理原則的程度。 最大平行處理原則程度的設定方式與平行查詢相同。 若要限制 DBCC 檢查所能使用的最大處理器數目，請使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 您可以利用追蹤旗標 2528 來停用平行檢查。 如需詳細資訊，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。
    
> [!NOTE]
> 並非所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本都提供此功能。 如需詳細資訊，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)之＜RDBMS 管理能力＞一節中的平行處理一致性檢查。    
    
## <a name="understanding-dbcc-error-messages"></a>了解 DBCC 錯誤訊息    
DBCC CHECKDB 命令執行完成之後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中會寫入一則訊息。 如果 DBCC 命令執行成功，該訊息將指出命令已順利完成，並顯示命令執行的時間量。 如果 DBCC 命令由於發生錯誤而在完成檢查之前停止執行，則訊息會指出命令已經結束，並顯示狀態值以及命令執行的時間量。 下表列出並描述可以包含在訊息中的狀態值。
    
|State|Description|    
|-----------|-----------------|    
|0|已引發錯誤號碼 8930。 這表示中繼資料中的損毀導致 DBCC 命令結束。|    
|1|已引發錯誤號碼 8967。 發生內部 DBCC 錯誤。|    
|2|修復緊急模式資料庫期間發生失敗。|    
|3|這表示中繼資料中的損毀導致 DBCC 命令結束。|    
|4|偵測到判斷提示或存取違規。|    
|5|發生使 DBCC 命令終止的未知錯誤。|    
    
## <a name="error-reporting"></a>錯誤報告    
每當 DBCC CHECKDB 偵測到損毀錯誤時，都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] LOG 目錄中建立傾印檔案 (`SQLDUMP*nnnn*.txt`)。 當針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體啟用*功能使用方式*資料收集及*錯誤報告*功能時，這個檔案會自動轉送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。 收集的資料是用來提升 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的功能。
傾印檔案包含 DBCC CHECKDB 命令的結果以及其他診斷輸出。 存取權會限制為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶及系統管理員 (sysadmin) 角色的成員。 依預設，系統管理員 (sysadmin) 角色包含 Windows `BUILTIN\Administrators` 群組及本機系統管理員群組的所有成員。 如果資料收集程序失敗，DBCC 命令不會失敗。
    
## <a name="resolving-errors"></a>解決錯誤    
如果 DBCC CHECKDB 報告任何錯誤，建議您從資料庫備份還原資料庫，而不要設定下列 REPAIR 選項之一來執行 REPAIR。 如果沒有任何備份，執行修復可以更正所報告的錯誤。 要用的 REPAIR 選項指定在報告的錯誤清單尾端。 不過，利用 REPAIR_ALLOW_DATA_LOSS 選項來更正錯誤，可能需要刪除某些頁面，因而也需要刪除某些資料。    

在某些情況下，可能會將對資料行的資料類型無效或超出範圍的值輸入資料庫中。 DBCC CHECKDB 可以偵側到對所有資料行資料類型無效的資料行值。 因此，配合 DATA_PURITY 選項對從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級的資料庫執行 DBCC CHECKDB，可以發現預先存在的資料行值錯誤。 因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法自動修復這些錯誤，所以資料行值必須手動更新。 如果 CHECKDB 偵測到這類錯誤，CHECKDB 會傳回警告、錯誤碼 2570，以及識別受影響之資料列和手動更正錯誤的資訊。    

修復動作可在某項使用者交易之下執行，讓使用者可以回復所做的變更。 如果回復修復，資料庫仍會包含錯誤，且必須從備份中還原。 修復動作完成之後，請備份資料庫。
    
## <a name="resolving-errors-in-database-emergency-mode"></a>以資料庫緊急模式解決錯誤    
當使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式將資料庫設為緊急模式時，DBCC CHECKDB 便可以在資料庫上執行某些特殊的修復作業 (如果已指定 REPAIR_ALLOW_DATA_LOSS 選項)。 這些修復可讓一般無法修復的資料庫以實體一致的狀態重新上線。 只有在資料庫無法從備份還原時，才應該使用上述修復來當做最後手段。 當資料庫設為緊急模式時，該資料庫會被標示為 READ_ONLY、停用記錄功能，並限制只有系統管理員 (sysadmin) 固定伺服器角色的成員才可存取。
    
> [!NOTE]
> 使用緊急模式時，無法在使用者交易內執行 DBCC CHECKDB 命令並在執行後回復交易。    
    
當資料庫處於緊急模式且執行了 DBCC CHECKDB (具有 REPAIR_ALLOW_DATA_LOSS 子句) 時，將會採取下列動作：
-   DBCC CHECKDB 會使用因 I/O 或總和檢查碼錯誤而標示為無法存取的頁面，如同未發生錯誤一樣。 執行這個動作，可增加從資料庫復原資料的機會。    
-   DBCC CHECKDB 會試圖利用正規記錄式復原技術來復原資料庫。    
-   如果資料庫復原因交易記錄損毀而無法成功，就會重建交易記錄。 重建交易記錄可能會導致無法維持交易一致性。    
    
> [!WARNING]
> REPAIR_ALLOW_DATA_LOSS 選項是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援的功能。 不過，這個選項不一定是讓資料庫處於實體一致狀態的最佳選項。 如果成功的話，REPAIR_ALLOW_DATA_LOSS 選項可能會導致部分資料遺失。 事實上，這個選項遺失的資料，可能會比使用者從上次已知良好備份還原資料庫所遺失的資料多。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一律建議使用者從上次已知良好的備份還原，做為修復 DBCC CHECKDB 所報告之錯誤的主要方法。 REPAIR_ALLOW_DATA_LOSS 選項**不是**從已知良好備份進行還原的替代方法。 只有在不可能從備份還原時，才建議使用這個「上次還原」緊急選項。    
>     
>  重建記錄檔之後，不保證會有完整的 ACID。    
>     
>  重建記錄檔之後，系統會自動執行 DBCC CHECKDB，並會同時回報及更正實體一致性問題。    
>     
>  您必須手動驗證邏輯資料一致性和商務邏輯這兩個條件約束。    
>     
>  交易記錄檔大小會保持為其預設大小，因此必須手動調整回最新的大小。    
    
如果 DBCC CHECKDB 命令成功完成，則資料庫會處於實體一致的狀態，且資料庫狀態會設為 ONLINE。 不過，資料庫可能會包含一個或多個交易不一致的狀況。 建議您執行 [DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md) 以識別是否有任何商務邏輯的缺陷，並且立即備份資料庫。
如果 DBCC CHECKDB 命令失敗，資料庫就無法修復。
    
## <a name="running-dbcc-checkdb-with-repair_allow_data_loss-in-replicated-databases"></a>在複寫的資料庫中搭配執行 DBCC CHECKDB 與 REPAIR_ALLOW_DATA_LOSS    
搭配執行 DBCC CHECKDB 命令與 REPAIR_ALLOW_DATA_LOSS 選項時，可能會影響使用者資料庫 (發行集和訂閱資料庫) 以及複寫所使用的散發資料庫。 發行集和訂閱資料庫包含已發行資料表和複寫中繼資料表。 請注意這些資料庫中的下列潛在問題：
-   已發行資料表。 由 CHECKDB 處理序執行以修復損毀使用者資料的動作可能並未複寫：    
-   合併式複寫使用觸發程序來追蹤已發行之資料表的變更。 如果資料列是由 CHECKDB 處理序插入、更新或刪除，將不會引發觸發程序；因此，也不會複寫變更。
-   異動複寫使用交易記錄來追蹤已發行之資料表的變更。 記錄讀取器代理程式接著會將這些變更移到散發資料庫。 某些 DBCC 修復雖然已經記錄，但卻不能由記錄讀取器代理程式加以複寫。 例如，如果資料頁已由 CHECKDB 處理序取消配置，記錄讀取器代理程式就不會將它轉譯成 DELETE 陳述式；因此，也不會複寫變更。
-   複寫中繼資料表。 由 CHECKDB 處理序執行以修復損毀複寫中繼資料表的動作需要移除及重新設定複寫。    
    
如果您必須在使用者資料庫或散發資料庫上搭配執行 DBCC CHECKDB 命令與 REPAIR_ALLOW_DATA_LOSS 選項：
1.  停止系統：停止該資料庫以及複寫拓撲中其他所有資料庫的活動，然後嘗試同步處理所有節點。 如需詳細資訊，請參閱[停止複寫拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)。    
1.  執行 DBCC CHECKDB。    
1.  如果 DBCC CHECKDB 報表包含散發資料庫中任何資料表的修復，或包含使用者資料庫中任何複寫中繼資料表的修復，請移除並重新設定複寫。 如需詳細資訊，請參閱[停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)。    
1.  如果 DBCC CHECKDB 報表包含任何已複寫資料表的修復，請執行資料驗證以判斷發行集與訂閱資料庫之間的資料是否有差異。    
    
## <a name="result-sets"></a>結果集    
DBCC CHECKDB 會傳回下列結果集。 這些值可能會不同，除非指定了 ESTIMATEONLY、PHYSICAL_ONLY 或 NO_INFOMSGS 選項：
    
```
 DBCC results for 'model'.    
    
 Service Broker Msg 9675, Level 10, State 1: Message Types analyzed: 13.    
    
 Service Broker Msg 9676, Level 10, State 1: Service Contracts analyzed: 5.    
    
 Service Broker Msg 9667, Level 10, State 1: Services analyzed: 3.    
    
 Service Broker Msg 9668, Level 10, State 1: Service Queues analyzed: 3.    
    
 Service Broker Msg 9669, Level 10, State 1: Conversation Endpoints analyzed: 0.    
    
 Service Broker Msg 9674, Level 10, State 1: Conversation Groups analyzed: 0.    
    
 Service Broker Msg 9670, Level 10, State 1: Remote Service Bindings analyzed: 0.    
    
 DBCC results for 'sys.sysrowsetcolumns'.    
    
 There are 630 rows in 7 pages for object 'sys.sysrowsetcolumns'.    
    
 DBCC results for 'sys.sysrowsets'.    
    
 There are 97 rows in 1 pages for object 'sys.sysrowsets'.    
    
 DBCC results for 'sysallocunits'.    
    
 There are 195 rows in 3 pages for object 'sysallocunits'.    
    
 There are 0 rows in 0 pages for object "sys.sysasymkeys".    
    
 DBCC results for 'sys.syssqlguides'.    
    
 There are 0 rows in 0 pages for object "sys.syssqlguides".    
    
 DBCC results for 'sys.queue_messages_1977058079'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_1977058079".    
    
 DBCC results for 'sys.queue_messages_2009058193'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2009058193".    
    
 DBCC results for 'sys.queue_messages_2041058307'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2041058307".    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'model'.    
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```

指定 NO_INFOMSGS 時，DBCC CHECKDB 會傳回下列結果集 (訊息)：
    
```
 The command(s) completed successfully.
 ```
 
指定 PHYSICAL_ONLY 時，DBCC CHECKDB 會傳回下列結果集：
    
```
 DBCC results for 'model'.    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'master'.  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
 ```
 
指定 ESTIMATEONLY 時，DBCC CHECKDB 會傳回下列結果集。
    
```
 Estimated TEMPDB space needed for CHECKALLOC (KB)    
    
 -------------------------------------------------  
    
 13   
    
 (1 row(s) affected)   
    
 Estimated TEMPDB space needed for CHECKTABLES (KB)    
    
 --------------------------------------------------    
    
 57 
    
 (1 row(s) affected)  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
    
## <a name="permissions"></a>權限    
需要系統管理員 (sysadmin) 固定伺服器角色或 db_owner 固定資料庫角色中的成員資格。
    
## <a name="examples"></a>範例    
    
### <a name="a-checking-both-the-current-and-another-database"></a>A. 同時檢查目前的資料庫與另一個資料庫    
下列範例會針對目前資料庫和 `DBCC CHECKDB` 資料庫執行 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。
    
```sql    
-- Check the current database.    
DBCC CHECKDB;    
GO    
-- Check the AdventureWorks2012 database without nonclustered indexes.    
DBCC CHECKDB (AdventureWorks2012, NOINDEX);    
GO    
```    
    
### <a name="b-checking-the-current-database-suppressing-informational-messages"></a>B. 檢查目前的資料庫，隱藏參考訊息    
下列範例會檢查目前資料庫，且隱藏所有參考訊息。
    
```sql    
DBCC CHECKDB WITH NO_INFOMSGS;    
GO    
```    
    
## <a name="see-also"></a>另請參閱    
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[檢視資料庫快照集的疏鬆檔案大小 &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)  
[sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)  
[系統資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  

