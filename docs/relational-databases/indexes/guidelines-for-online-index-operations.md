---
title: 線上索引作業的指導方針 | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- clustered indexes, online operations
- online index operations
- indexes [SQL Server], online operations
- disk space [SQL Server], indexes
- nonclustered indexes [SQL Server], online operations
- transaction logs [SQL Server], indexes
ms.assetid: d82942e0-4a86-4b34-a65f-9f143ebe85ce
caps.latest.revision: 64
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.suite: sql
ms.prod_service: table-view-index, sql-database
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d62566a8e5db1eaee81944d364f169ccfa6ef477
ms.sourcegitcommit: 70882926439a63ab9d812809429c63040eb9a41b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36262142"
---
# <a name="guidelines-for-online-index-operations"></a>線上索引作業的指導方針
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  當您執行線上索引作業時，下列指導方針將適用：  
  
-   當基礎資料表包含下列大型物件 (LOB) 資料類型時，必須離線建立、重建或卸除叢集索引： **image**、 **ntext**和 **text**。  
  
-   當資料表包含 LOB 資料類型，但這些資料行並未在索引定義中當做索引鍵或非索引鍵 (內含) 資料行使用時，您可以在線上建立非唯一的非叢集索引。  
  
-   您無法在線上建立、重建或卸除本機暫存資料表的索引。 此限制不適用於全域暫存資料表上的索引。
- 可以從非預期的失敗、資料庫容錯移轉或 **PAUSE** 命令之後的停止處繼續索引。 請參閱[改變索引](../../t-sql/statements/alter-index-transact-sql.md)。 

> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有版本都無法使用線上索引作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本所支援的功能清單，請參閱[版本支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 下表顯示可在線上執行的索引作業、從這些線上作業排除的索引，以及可繼續的索引限制。 也包含其他限制。  
  
| 線上索引作業 | 排除索引 | 其他限制 |  
|----------------------------|----------------------|------------------------|  
|ALTER INDEX REBUILD|已停用叢集索引或已停用索引檢視<br /><br /> XML 索引<br /><br />資料行存放區索引 <br /><br /> 本機暫存資料表上的索引|當資料表包含排除索引時，指定關鍵字 ALL 可能導致作業失敗。<br /><br /> 重建已停用索引的其他限制也適用。 如需詳細資訊，請參閱 [停用索引和條件約束](../../relational-databases/indexes/disable-indexes-and-constraints.md)。|  
|CREATE INDEX|XML 索引<br /><br /> 在檢視上的初始唯一叢集索引<br /><br /> 本機暫存資料表上的索引||  
|CREATE INDEX WITH DROP_EXISTING|已停用叢集索引或已停用索引檢視<br /><br /> 本機暫存資料表上的索引<br /><br /> XML 索引||  
|DROP INDEX|停用的索引<br /><br /> XML 索引<br /><br /> 非叢集索引<br /><br /> 本機暫存資料表上的索引|不能在單一陳述式中指定多個索引。|  
|ALTER TABLE ADD CONSTRAINT (PRIMARY KEY 或 UNIQUE)|本機暫存資料表上的索引<br /><br /> 叢集索引|一次僅允許一個子子句 (Subclause)。 例如，您無法在同一個 ALTER TABLE 陳述式中加入和卸除 PRIMARY KEY 或 UNIQUE 條件約束。|  
|ALTER TABLE DROP CONSTRAINT (PRIMARY KEY 或 UNIQUE)|叢集索引||  
  
 處理線上索引作業時，不能修改、截斷或卸除基礎資料表。  
  
 當您建立或卸除叢集時，指定的線上選項設定 (ON 或 OFF) 會套用到必須重建的任何非叢集索引。 例如，若是使用 CREATE INDEX WITH DROP_EXISTING, ONLINE=ON 線上建立叢集索引，那麼也會線上重建所有相關聯的非叢集索引。  
  
 線上建立或重建 UNIQUE 索引時，此索引產生器與並行使用者交易可能嘗試要插入同一個索引鍵，因此而違反了唯一性。 若在原始資料列從來源資料表移動到新索引之前，將使用者輸入的資料列插入至新索引(目標)，線上索引作業將失敗。  
  
 雖然這種情形並不常見，但是由於使用者或應用程序活動的原因，線上索引作業與資料庫更新互動時，即會導致死結。 在這些極少數情況下， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 將選擇使用者或應用程序活動作為死結的犧牲者。  
  
 只有在建立多個新的非叢集索引或重新組織非叢集索引時，才能在同一個資料表或檢視上執行並行線上索引 DDL 作業。 同時執行的所有其他線上索引作業都會失敗。 例如，在同一個資料表中線上重建現有索引時，是無法線上建立新的索引。  
  
 如果索引包含大型物件類型的資料行，且在同一交易中另有更新作業早於線上作業，便無法執行該線上作業。 若要解決此問題，請將線上作業移出交易之外，或使其比交易中的任何更新都更早執行。  
  
## <a name="disk-space-considerations"></a>磁碟空間考量因素  
 線上索引作業所需的磁碟空間需求高於離線索引作業。 
 - 在索引建立和索引重建作業期間，所建置 (或重建) 的索引都需要額外的空間。 
 - 此外，暫存對應索引需要磁碟空間。 此暫存索引用於建立、重建或卸除叢集索引的線上索引作業。
- 線上卸除叢集索引與線上建立 (或重建) 叢集索引需要一樣多的磁碟空間。 

如需詳細資訊，請參閱 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)。  
  
## <a name="performance-considerations"></a>效能考量  
 雖然線上索引作業允許並行使用者更新活動，但是若更新活動負載繁重，此索引作業將需要更長時間。 一般而言，無論並行更新活動的程度，線上索引作業都將低於同等的離線索引作業。  
  
 由於線上索引作業期間都會維護來源與目標結構，因此會增加插入、更新與刪除交易時所耗用的資源，甚至可能加倍。 這在索引作業期間可能導致效能降低與資源過度耗用，尤其是 CPU 時間。 線上索引作業會完整記錄下來。  
  
 儘管我們推薦線上作業，但您應該評估您的環境與特定要求。 離線執行索引作業可能會是最佳方式。 若要達到這種方式，在作業期間，使用者僅能有限地存取資料，但是將更快完成作業且使用較少的資源。  
  
 在執行 SQL Server 2016 的多處理器電腦上，索引陳述式可能會如同其他查詢，使用更多處理器來執行與索引陳述式建立關聯的掃描和排序作業。 您可以使用 MAXDOP 索引選項控制線上索引作業專用的處理器數目。 以此方式，您就可以平衡索引作業所使用的資源以及使用者並行所使用的資源。 如需詳細資訊，請參閱 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。 如需支援平行索引作業之 SQL Server 版本的詳細資訊，請參閱[版本支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 因為索引作業的最終階段會保留 S-lock 或 Sch-M 鎖定，所以在明確的使用者交易 (例如 BEGIN TRANSACTION...COMMIT 區塊) 內執行線上索引作業時要特別小心。 這樣做導致交易完後才執行鎖定，而妨礙使用者進行並行作業。  
  
 當線上索引重建可搭配 `MAX DOP > 1` 和 `ALLOW_PAGE_LOCKS = OFF` 選項執行時，可能會增加片段。 如需詳細資訊，請參閱 [運作方式：線上索引重建 - 可能會導致片段增加](http://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx)。  
  
## <a name="transaction-log-considerations"></a>交易記錄考量因素  
 大規模的索引作業，無論是離線或線上執行，都會產生大量資料負載，而很快就填滿了交易記錄。 若要確定可以回復索引作業，在索引作業完成以前，不能截斷交易記錄；不過，在索引作業期間可以備份此記錄。 因此，在索引作業期間，交易記錄必須有足夠的空間，才能儲存索引作業交易與任何並行使用者交易。 如需詳細資訊，請參閱 [索引作業的交易記錄磁碟空間](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)。  

## <a name="resumable-index-considerations"></a>可繼續索引考量因素

> [!NOTE]
> 可繼續的索引選項適用於 SQL Server (從 SQL Server 2017 開始) (僅限索引重建) 和 SQL Database (建立非叢集索引和索引重建)。 請參閱[建立索引](../../t-sql/statements/create-index-transact-sql.md) (目前處於僅限 SQL Database 公開預覽狀態) 和[更改索引](../../t-sql/statements/alter-index-transact-sql.md)。 

當您執行可繼續的線上索引建立或重建時，將適用下列指導方針：
-   管理、規劃和擴充索引的維護期間。 您可以暫停和重新啟動索引建立或重建作業多次，以符合您的維護期間。
- 從索引建立或重建失敗 (例如資料庫容錯移轉或磁碟空間不足) 中復原。
- 當索引作業暫停時，原始索引和新建立的索引都需要磁碟空間，而且必須在 DML 作業期間進行更新。

- 在索引建立或重建作業時，啟用交易記錄的截斷功能。
- 不支援 SORT_IN_TEMPDB=ON 選項

> [!IMPORTANT]
> 可繼續的索引建立或重建不需要您持續開啟長時間執行的交易，允許在此作業期間執行記錄截斷，而讓記錄空間管理的效能更佳。 利用新的設計，我們設法將資料庫中的必要資料與重新啟動可繼續作業所需的所有參考保存在一起。

一般而言，可繼續和不可繼續的線上索引重建之間沒有效能差異。 對於建立可繼續的索引，會有一定的額外負荷造成可繼續和不可繼續的索引建立之間出現細微的效能差異。 這種差異只有在較小的資料表上才非常明顯。

若在索引作業暫停時，更新可繼續的索引：
- 對於最常讀取的工作負載，效能影響微不足道。 
- 對於更新繁重的工作負載，您可能會遇到輸送量降低情況 (我們的測試顯示小於 10% 的降低情況)。

一般而言，可繼續和不可繼續的線上索引建立或重建之間的磁碟重組品質沒有差異。

## <a name="online-default-options"></a>線上預設選項 

> [!IMPORTANT]
> 這些選項處於公開預覽狀態。

您可以透過設定 ELEVATE_ONLINE 或 ELEVATE_RESUMABLE 資料庫範圍設定選項，在資料庫層級設定線上或可繼續的預設選項。 使用這些預設選項，您可以避免不小心執行讓資料庫資料表離線的作業。 這兩個選項都會使引擎自動將某些作業提升為線上或可繼續執行。  
您可以使用 [ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 命令，將選項設為 FAIL_UNSUPPORTED、WHEN_SUPPORTED 或 OFF。 您可以為線上和可繼續設定不同的值。 

ELEVATE_ONLINE 和 ELEVATE_RESUMABLE 僅適用於分別支援線上和可繼續語法的 DDL 陳述式。 例如，如果您嘗試建立 ELEVATE_ONLINE=FAIL_UNSUPORTED 的 XML 索引，由於 XML 索引不支援 ONLINE= 語法，因此會離線執行作業。 該選項只會影響未指定 ONLINE 或 RESUMABLE 選項所送出的 DDL 陳述式。 例如，藉由送出 ONLINE=OFF 或 RESUMABLE=OFF 的陳述式，使用者可以覆寫 FAIL_UNSUPPORTED 設定，並離線及/或以不可繼續的方式執行陳述式。 
 
> [!NOTE]
> ELEVATE_ONLINE 和 ELEVATE_RESUMABLE 不適用於 XML 索引作業。 
 
## <a name="related-content"></a>相關內容  
 [線上索引作業如何運作](../../relational-databases/indexes/how-online-index-operations-work.md)  
  
 [線上執行索引作業](../../relational-databases/indexes/perform-index-operations-online.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  
