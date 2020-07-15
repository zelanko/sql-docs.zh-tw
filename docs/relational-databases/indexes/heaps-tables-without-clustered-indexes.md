---
title: 堆積 (無叢集索引的資料表) | Microsoft Docs
ms.custom: ''
ms.date: 11/01/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- heaps
- forward record
- forwarded record
- forwarding pointer
- RID
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e186d1da5ab42b25c120303a545c9164d949ad45
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786475"
---
# <a name="heaps-tables-without-clustered-indexes"></a>堆積 (無叢集索引的資料表)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  堆積是一種沒有叢集索引的資料表。 一個或多個可以建立在儲存為堆積之資料表上的非叢集索引。 資料會以無指定順序的方式儲存於堆積中。 一般來說，資料一開始是會以資料表中插入資料列的順序儲存，但是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會移動堆積中的資料，以有效率地儲存資料列，因此無法預期資料順序。 為確保從堆積中傳回之資料列順序，您必須使用 `ORDER BY` 子句。 若要指定儲存資料列的永久邏輯順序，請於資料表上建立叢集索引，如此一來資料表便不是堆積。  
  
> [!NOTE]  
> 有些時候不建立叢集索引，而讓資料表保持為堆積反而有助於工作，但有效地使用堆積是一項進階的技巧。 除非有將資料表保留為堆積的特殊理由，否則大多數的資料表都應該選擇一個適合的叢集索引。  
  
## <a name="when-to-use-a-heap"></a>使用堆積的時機  
當資料表儲存為堆積時，參考會將各個資料列識別為 8 位元組資料列識別碼 (RID)，該識別碼由檔案編號、資料頁碼及頁面上的位置 (FileID:PageID:SlotID) 所構成。 資料列識別碼是一種小型而高效率的結構。 

堆積可用來作為未排序插入作業的大型暫存表格。 由於插入資料時不會強制執行嚴格的順序，因此插入作業通常會比同等的插入叢集索引作業快。 如果堆積的資料會讀取並處理到最終目的地，則建立包含讀取查詢所用搜尋述詞的窄小非叢集索引可能會很有用。 

> [!NOTE]  
> 資料會依資料頁的順序從堆積中擷取，但不一定是插入資料的順序。 

當資料一律透過非叢集索引存取且 RID 比叢集索引鍵還小時，資料專業人員有時候也會使用堆積。 

如果資料表為堆積且沒有任何非叢集索引，則必須讀取整份資料表 (資料表掃描) 才能找到資料列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法直接在堆積上尋找 RID。 當資料表很小時，此種方式是可接受的。  
  
## <a name="when-not-to-use-a-heap"></a>切勿使用堆積的情況  
 經常按排序順序傳回資料時，請勿使用堆積。 在排序資料行中的叢集索引，可免去進行排序作業。  
  
 當資料經常組合在一起時，請勿使用堆積。 資料組合前必須先排序，而在排序資料行中建立叢集索引，可免去排序作業。  
  
 經常要從資料表中查詢資料範圍時，請勿使用堆積。 在範圍資料行中若有叢集索引，可以免去排序整個堆積。  
  
 如果沒有非叢集索引且資料表很大，則請勿使用堆積，除非想要傳回不含任何指定順序的整個資料表內容。 在堆積中若要尋找某一資料列，就必須讀取堆積中的所有資料列。  
 
 如果經常更新資料，則請勿使用堆積。 如果您更新記錄，而該更新在資料頁中所使用空間比目前使用的還要更多，則必須將記錄移至具有足夠可用空間的資料頁。 此動作會建立一筆指向資料新位置的**轉送記錄**，且**轉送指標**必須寫入先前保留該資料的頁面中，以此指示新的實體位置。 這會採用堆積中的片段。 掃描堆積時，必須遵循這些指標來限制預先讀取的效能，且可能會產生降低掃描效能的額外 I/O。 
  
## <a name="managing-heaps"></a>管理堆積  
 若要建立堆積，請建立不含叢集索引的資料表。 如果資料表中已有叢集索引，則請卸除叢集索引，將資料表還原為堆積。  
  
 若要移除堆積，請在堆積上建立叢集索引。  
  
 若要重建堆積以回收浪費的空間：
 -  在堆積上建立叢集索引，然後卸除該叢集索引。  
 -  使用 `ALTER TABLE ... REBUILD` 命令來重建堆積。
  
> [!WARNING]  
> 建立或卸除叢集索引時必須重寫整份資料表。 若資料表具有非叢集索引，則一旦變更叢集索引之後，所有的非叢集索引都必須重建。 因此，在堆積與叢集索引結構之間的來回往返將會花費許多時間，且需要足夠的磁碟空間，才可在 tempdb 中重新排序資料。  

## <a name="heap-structures"></a>堆積結構
堆積是一種沒有叢集索引的資料表。 堆積的 [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)中有一個資料列包含堆積所用之每一個資料分割的 `index_id = 0` 。 依預設，堆積只有一個資料分割。 當堆積有多個資料分割時，每個資料分割都有一個堆積結構來包含該特定資料分割的資料。 例如，如果堆積有四個資料分割，則有四個堆積結構；每個資料分割中各有一個堆積結構。

視堆積中的資料類型而定，每個堆積結構都會有一個或多個配置單位來儲存和管理特定資料分割的資料。 每個資料分割的每一個堆積至少會有一個 `IN_ROW_DATA` 配置單位。 若堆積包含大型物件 (LOB) 資料行，則每個資料分割在堆積中將會有一個 `LOB_DATA` 配置單位。 若堆積包含變數長度資料行，且其超過 8,060 個位元組的資料列大小限制，則每個資料分割的每個堆積也會有一個 `ROW_OVERFLOW_DATA` 配置單位。

`first_iam_page` 系統檢視中的資料行 `sys.system_internals_allocation_units` 會指向 IAM 頁面鏈結中的的第一個 IAM 頁面。此頁面負責管理配置到特定資料分割中之堆積的空間。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 IAM 頁面在堆積中移動。 資料頁以及其中的資料列並沒有特定順序，也不會連結在一起。 資料頁之間的唯一邏輯連接為 IAM 頁面中所記錄的資訊。

> [!IMPORTANT]  
> 此 `sys.system_internals_allocation_units` 系統檢視僅保留為供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部使用。 我們無法保證未來的相容性。
 
堆積的資料表掃描或循序讀取可以藉著掃描 IAM 頁面找出包含堆積頁面的範圍來執行。 因為 IAM 會以範圍存在於檔案中的順序來表示它們，這代表循序的堆積掃描都將依檔案順序進行。 使用 IAM 分頁設定掃描順序也表示堆積中的資料列通常不會依插入順序傳回。

下圖顯示 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 如何使用 IAM 頁面來擷取單一資料分割堆積中的資料列。 

![iam_heap](../../relational-databases/indexes/media/iam-heap.gif)
  
## <a name="related-content"></a>相關內容  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)     
[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)     
[叢集與非叢集索引說明](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)     
  
  
