---
title: 堆積 (無叢集索引的資料表) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- heaps
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de71808c54264639aea82fe66cf23a7bfd6bd0ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162159"
---
# <a name="heaps-tables-without-clustered-indexes"></a>堆積 (無叢集索引的資料表)
  堆積是一種沒有叢集索引的資料表。 一個或多個可以建立在儲存為堆積之資料表上的非叢集索引。 資料會以無指定順序的方式儲存於堆積中。 一般來說，資料一開始是會以資料表中插入資料列的順序儲存，但是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會移動堆積中的資料，以有效率地儲存資料列，因此無法預期資料順序。 為確保從堆積中傳回之資料列順序，您必須使用 `ORDER BY` 子句。 若要指定儲存資料列的順序，請於資料表上建立叢集索引，如此一來資料表便不是堆積。  
  
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
  
## <a name="related-content"></a>相關內容  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
 [叢集與非叢集索引說明](clustered-and-nonclustered-indexes-described.md)  
  
  
