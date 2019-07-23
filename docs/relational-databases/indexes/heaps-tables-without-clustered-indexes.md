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
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5234820dbf88067aad2ff76b0bd373c7f70cb3e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909778"
---
# <a name="heaps-tables-without-clustered-indexes"></a>堆積 (無叢集索引的資料表)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  堆積是一種沒有叢集索引的資料表。 一個或多個可以建立在儲存為堆積之資料表上的非叢集索引。 資料會以無指定順序的方式儲存於堆積中。 一般來說，資料一開始是會以資料表中插入資料列的順序儲存，但是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會移動堆積中的資料，以有效率地儲存資料列，因此無法預期資料順序。 為確保從堆積中傳回之資料列順序，您必須使用 **ORDER BY** 子句。 若要指定儲存資料列的順序，請於資料表上建立叢集索引，如此一來資料表便不是堆積。  
  
> [!NOTE]  
>  有些時候不建立叢集索引，而讓資料表保持為堆積反而有助於工作，但有效地使用堆積是一項進階的技巧。 除非有將資料表保留為堆積的特殊理由，否則大多數的資料表都應該選擇一個適合的叢集索引。  
  
## <a name="when-to-use-a-heap"></a>使用堆積的時機  
 如果資料表為堆積且沒有任何非叢集索引，那麼您必須查看整份資料表 (資料表掃描) 才能找到資料列。 當您的資料表很短，例如只是一張您公司 12 處地區性辦公室的清單時，還不算太麻煩。  
  
 當資料表儲存為堆積時，參照會將各個資料列識別為資料列識別碼 (RID) (由檔案編號、資料頁碼及頁面上的位置所構成)。 資料列識別碼是一個小而高效率的結構。 有時候當資料總是透過非叢集索引存取，且 RID 比叢集索引鍵還小時，資料工程師會使用堆積。  
  
## <a name="when-not-to-use-a-heap"></a>切勿使用堆積的情況  
 經常按排序順序傳回資料時，請勿使用堆積。 在排序資料行中的叢集索引，可免去進行排序作業。  
  
 當資料經常組合在一起時，請勿使用堆積。 資料組合前必須先排序，而在排序資料行中建立叢集索引，可免去排序作業。  
  
 經常要從資料表中查詢資料範圍時，請勿使用堆積。  在範圍資料行中若有叢集索引，可以免去排序整個堆積。  
  
 沒有非叢集索引且資料表相當龐大時，請勿使用堆積。 在堆積中若要尋找某一資料列，就必須讀取堆積中的所有資料列。  
  
## <a name="managing-heaps"></a>管理堆積  
 若要建立堆積，請建立不含叢集索引的資料表。 如果資料表中已有叢集索引，則請卸除叢集索引，將資料表還原為堆積。  
  
 若要移除堆積，請在堆積上建立叢集索引。  
  
 若要重建堆積以回收浪費掉的空間，請先在堆積上建立叢集索引，然後再卸除該叢集索引。  
  
> [!WARNING]  
>  建立或卸除叢集索引時必須重寫整份資料表。 若資料表具有非叢集索引，則一旦變更叢集索引之後，所有的非叢集索引都必須重建。 因此，在堆積與叢集索引結構之間的來回往返將會花費許多時間，且需要足夠的磁碟空間，才可在 tempdb 中重新排序資料。  

## <a name="heap-structures"></a>堆積結構


堆積是一種沒有叢集索引的資料表。 堆積的 [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)中有一個資料列包含堆積所用之每一個資料分割的 `index_id = 0` 。 依預設，堆積只有一個資料分割。 當堆積有多個資料分割時，每個資料分割都有一個堆積結構來包含該特定資料分割的資料。 例如，如果堆積有四個資料分割，則有四個堆積結構；每個資料分割中各有一個堆積結構。

視堆積中的資料類型而定，每個堆積結構都會有一個或多個配置單位來儲存和管理特定資料分割的資料。 每個資料分割的每一個堆積至少會有一個 `IN_ROW_DATA` 配置單位。 若堆積包含大型物件 (LOB) 資料行，則每個資料分割在堆積中將會有一個 `LOB_DATA` 配置單位。 若堆積包含變數長度資料行，且其超過 8,060 個位元組的資料列大小限制，則每個資料分割的每個堆積也會有一個 `ROW_OVERFLOW_DATA` 配置單位。

`first_iam_page` 系統檢視中的資料行 `sys.system_internals_allocation_units` 會指向 IAM 頁面鏈結中的的第一個 IAM 頁面。此頁面負責管理配置到特定資料分割中之堆積的空間。 SQL Server 使用 IAM 頁面在堆積中移動。 資料頁以及其中的資料列並沒有特定順序，也不會連結在一起。 資料頁之間的唯一邏輯連接為 IAM 頁面中所記錄的資訊。

> [!IMPORTANT]  
> `sys.system_internals_allocation_units` 系統檢視保留供 Microsoft SQL Server 內部使用。 我們無法保證未來的相容性。
 
堆積的資料表掃描或循序讀取可以藉著掃描 IAM 頁面找出包含堆積頁面的範圍來執行。 因為 IAM 會以範圍存在於檔案中的順序來表示它們，這代表循序的堆積掃描都將依檔案順序進行。 使用 IAM 分頁設定掃描順序也表示堆積中的資料列通常不會依插入順序傳回。

下圖顯示 SQL Server Database Engine 如何利用 IAM 頁面擷取單一資料分割堆積中的資料列。 

![iam_heap](../../relational-databases/indexes/media/iam-heap.gif)

  
## <a name="related-content"></a>相關內容  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)     
[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)     
[叢集與非叢集索引說明](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)     
  
  
