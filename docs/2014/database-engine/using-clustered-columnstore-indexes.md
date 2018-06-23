---
title: 使用叢集資料行存放區索引 |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5af6b91c-724f-45ac-aff1-7555014914f4
caps.latest.revision: 6
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.openlocfilehash: 527905bc0b0be07c178c873ae22fd06a0166b963
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032615"
---
# <a name="using-clustered-columnstore-indexes"></a>使用叢集資料行存放區索引
  在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中使用叢集資料行存放區索引的工作。  
  
 如需資料行存放區索引的概觀，請參閱[Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md)。  
  
 叢集資料行存放區索引的相關資訊，請參閱[Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md)。  
  
## <a name="contents"></a>目錄  
  
-   [建立叢集資料行存放區索引](#create)  
  
-   [卸除叢集資料行存放區索引](#drop)  
  
-   [將資料載入叢集資料行存放區索引](#load)  
  
-   [變更叢集資料行存放區索引中的資料](#change)  
  
-   [重建叢集資料行存放區索引](#rebuild)  
  
-   [重新組織叢集資料行存放區索引](#reorganize)  
  
##  <a name="create"></a> 建立叢集資料行存放區索引  
 若要建立非叢集資料行存放區索引，先建立資料列存放區資料表做為堆積或叢集的索引，，然後使用[建立叢集資料行存放區索引&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql)陳述式，將資料表轉換成叢集資料行存放區索引。 如果您要讓叢集資料行存放區索引使用與叢集索引相同的名稱，請使用 DROP_EXISTING 選項。  
  
 此範例會建立資料表做為堆積，然後將它轉換成名為 cci_Simple 的叢集資料行存放區索引。 這會將整個資料表的儲存體從資料列存放區變更為資料行存放區。  
  
```  
CREATE TABLE T1(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_T1 ON T1;  
GO  
```  
  
 如需其他範例，請參閱 < 範例 > 一節中的[CREATE CLUSTERED COLUMNSTORE INDEX &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)。  
  
##  <a name="drop"></a> 卸除叢集資料行存放區索引  
 使用[DROP INDEX &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/drop-index-transact-sql)陳述式來卸除叢集資料行存放區索引。 此作業將卸除索引並將資料行存放區資料表轉換成資料列存放區堆積。  
  
##  <a name="load"></a> 將資料載入叢集資料行存放區索引  
 您可以利用任何一種標準的載入方法，將資料加入至現有的叢集資料行存放區索引中。  例如，bcp 大量載入工具、Integration Services 和 INSERT... SELECT 都可以將資料載入叢集資料行存放區索引中。  
  
 叢集資料行存放區索引會運用差異存放區防止資料行存放區中出現資料行區段的片段。  
  
### <a name="loading-into-a-partitioned-table"></a>載入至資料分割資料表  
 對於分割資料， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會先將每個資料列指派至一個分割區，然後在分割區內對資料執行資料行存放區作業。 每個分割區都有自己的資料列群組以及至少一個差異存放區。  
  
### <a name="deltastore-loading-scenarios"></a>差異存放區載入案例  
 資料列會在差異存放區中累積，直到資料列數達到一個資料列群組允許的資料列數上限。 當差異存放區達到每個資料列群組的資料列數上限時，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會將該資料列群組標示為 "CLOSED"。 背景處理序稱為「Tuple 移動器」，會尋找 CLOSED 資料列群組並移入資料行存放區中，資料列群組會在其中壓縮至資料行區段內，而資料行區段會儲存在資料行存放區中。  
  
 每一個叢集資料行存放區索引可以有多個差異存放區。  
  
-   如果差異存放區已鎖定， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 將嘗試鎖定另一個差異存放區。 如果沒有可用的差異存放區， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 將建立新的差異存放區。  
  
-   若是資料分割資料表，每個分割區可以有一個或多個差異存放區。  
  
 下列案例僅適用於叢集資料行存放區索引，將描述載入的資料列何時會直接進入資料行存放區，或何時會進入差異存放區。  
  
 在範例中，每個資料列群組可以有 102,400-1,048,576 個資料列。  
  
|大量載入的資料列|加入至資料行存放區的資料列|加入至差異存放區的資料列|  
|-----------------------|-----------------------------------|----------------------------------|  
|102,000|0|102,000|  
|145,000|145,000<br /><br /> 資料列群組大小：145,000|0|  
|1,048,577|1,048,576<br /><br /> 資料列群組大小：1,048,576。|@shouldalert|  
|2,252,152|2,252,152<br /><br /> 資料列群組大小：1,048,576、1,048,576、155,000|0|  
  
 下列範例顯示將 1,048,577 個資料列載入分割區的結果。 結果顯示，資料行存放區中有一個 COMPRESSED 資料列群組 (壓縮的資料行區段)，而差異存放區中有 1 個資料列。  
  
```  
SELECT * FROM sys.column_store_row_groups  
```  
  
 ![批次載入的資料列群組和差異存放區](../../2014/database-engine/media/sql-server-pdw-columnstore-batchload.gif "批次載入的資料列群組和差異存放區")  
  

  
##  <a name="change"></a> 變更叢集資料行存放區索引中的資料  
 叢集資料行存放區索引支援插入、更新及刪除 DML 作業。  
  
 使用[插入&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/insert-transact-sql)插入資料列。 資料列會加入至差異存放區。  
  
 使用 [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) 刪除資料列。  
  
-   如果資料列位於資料行存放區中，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會將該資料列標示為邏輯刪除，但不會回收該資料列的實體儲存體，直到重建索引為止。  
  
-   如果資料列位於差異存放區中，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會以邏輯方式實際刪除該資料列。  
  
 使用 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) 更新資料列。  
  
-   如果資料列位於資料行存放區中，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會將該資料列標示為邏輯刪除，然後將更新的資料列插入差異存放區中。  
  
-   如果資料列位於差異存放區中，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會更新差異存放區中的該資料列。  
  
##  <a name="rebuild"></a> 重建叢集資料行存放區索引  
 使用[CREATE CLUSTERED COLUMNSTORE INDEX &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql)或[ALTER INDEX &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/alter-index-transact-sql)執行完整重建現有的叢集資料行存放區索引。 此外，您可以使用 ALTER INDEX... REBUILD 重建特定分割區。  
  
### <a name="rebuild-process"></a>重建程序  
 為了重建叢集資料行存放區索引，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會進行以下作業：  
  
-   在進行重建時，取得資料表或分割區上的獨佔鎖定。  在重建期間，資料處於「離線」狀態而且無法使用。  
  
-   藉由實際刪除已經以邏輯方式從資料表刪除的資料列，以重組資料行存放區，而已刪除的位元組會在實體媒體上回收。  
  
-   在重建索引之前，合併差異存放區中的資料列存放區資料與資料行存放區中的資料。 重建完成時，所有資料都會以資料行存放區格式儲存，且差異存放區會是空的。  
  
-   將所有資料重新壓縮到資料行存放區。 當重建進行時，有兩個資料行存放區索引複本存在。 當重建完成時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會刪除原始資料行存放區索引。  
  
### <a name="recommendations-for-rebuilding-a-clustered-columnstore-index"></a>重建叢集資料行存放區索引的建議  
 重建叢集資料行存放區索引對於移除片段以及將所有資料列移入資料行存放區而言相當實用。 以下是我們的建議：  
  
-   重建分割區，而非整份資料表。  
  
    1.  如果索引很大，重建整個資料表將花上很長的時間，而且需要足夠的磁碟空間來存放重建期間額外的索引副本。 通常只需要重建最近使用的分割區。  
  
    2.  對於資料分割資料表，您不需要重建整個資料行存放區索引，因為片段可能只會出現在最近修改過的分割區中。 事實資料表和大型維度資料表通常會進行分割區，以便在資料表區塊上執行備份和管理作業。  
  
-   在繁重的 DML 作業之後重建分割區。  
  
     重建分割區將會重組分割區並減少磁碟儲存體。 重建將會刪除資料行存放區中所有標示為刪除的資料列，並且將所有資料列從差異存放區移至資料行存放區。  
  
-   載入資料後重建分割區。  
  
     如此可確保所有資料都儲存在資料行存放區中。 如果同時進行多項載入，每個分割區最後可能會有多個差異存放區。 重建會將所有差異存放區資料列移至資料行存放區。  
  
##  <a name="reorganize"></a> 重新組織叢集資料行存放區索引  
 重新組織叢集資料行存放區索引會將所有 CLOSED 資料列群組移到資料行存放區中。 若要執行重新組織，使用[ALTER INDEX &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)與 REORGANIZE 選項。  
  
 不需要進行重新組織，也能將 CLOSED 資料列群組移到資料行存放區中。 Tuple 移動處理序最後會找到所有 CLOSED 資料列群組並加以移動。 不過，Tuple 移動是單一執行緒，而且移動資料列群組的速度對於您的工作負載可能不夠快。  
  
### <a name="recommendations-for-reorganizing"></a>對重新組織的建議  
 重新組織叢集資料行存放區索引的時機：  
  
-   在一次或多次資料載入後重新組織叢集資料行存放區索引，以便盡快獲得查詢效能的優勢。 進行重新組織一開始會需要額外的 CPU 資源來壓縮資料，這可能會拖慢整體系統效能。 不過，只要資料壓縮完成，查詢效能就能獲得改善。  
  
  
