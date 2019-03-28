---
title: 疑難排解記憶體最佳化雜湊索引常見效能問題 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 1954a997-7585-4713-81fd-76d429b8d095
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d7ed4098feb8bfd2d156e3de2f81fbf7329915aa
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535540"
---
# <a name="troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes"></a>疑難排解記憶體最佳化雜湊索引的常見效能問題
  本主題將焦點放在疑難排解以及解決與雜湊索引相關的常見問題。  
  
## <a name="search-requires-a-subset-of-hash-index-key-columns"></a>搜尋需要雜湊索引鍵資料行的子集  
 **問題：** 雜湊索引需要所有的索引鍵資料行的值，以計算雜湊值，並在雜湊表中找出對應的資料列。 因此，如果查詢只包含 WHERE 子句中索引鍵子集的等號比較述詞，則 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 無法使用索引搜尋找出對應 WHERE 子句中述詞的資料列。  
  
 相反地，只要索引鍵資料行是索引中的前置資料行，像是磁碟非叢集索引和記憶體最佳化非叢集索引這類已排序索引就可支援在這些資料行的子集上進行索引搜尋。  
  
 **徵兆：** 這會導致效能變差，做為[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]需要執行完整資料表掃描，而不是索引搜尋，通常是較快速的作業。  
  
 **如何疑難排解：** 除了效能降低，查詢計劃的檢查將會顯示掃描而不是索引搜尋。 如果查詢相當簡單，則查詢文字和索引定義的檢查也會指出搜尋需要索引鍵資料行的子集。  
  
 請考慮下列資料表和查詢：  
  
```sql  
CREATE TABLE [dbo].[od]  
(  
     o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
     CONSTRAINT PK_od PRIMARY KEY NONCLUSTERED HASH (o_id, od_id) WITH (BUCKET_COUNT = 10000)  
)  
WITH (MEMORY_OPTIMIZED = ON)  
  
 SELECT p_id  
 FROM dbo.od  
 WHERE o_id=1  
```  
  
 資料表的兩個資料行 (o_id、od_id) 上有雜湊索引，而查詢在 (o_id) 上有等號比較述詞。 由於查詢只會在索引鍵資料行的子集上擁有等號比較述詞，因此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 無法使用 PK_od 執行索引搜尋作業，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 必須改為轉換成完整索引掃描。  
  
 **因應措施：** 有許多種可行的因應措施。 例如：  
  
-   重建索引做為非叢集類型，而不是非叢集雜湊。 記憶體最佳化非叢集索引已經過排序，因此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以在前置索引鍵資料行上執行索引搜尋。 範例產生的主索引鍵定義會是 `constraint PK_od primary key nonclustered`。  
  
-   變更目前的索引鍵以符合 WHERE 子句中的資料行。  
  
-   加入與查詢的 WHERE 子句中資料行相符的新雜湊索引。 在此範例中，產生的資料表定義如下：  
  
    ```sql  
    CREATE TABLE dbo.od  
     ( o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
  
     CONSTRAINT PK_od PRIMARY KEY   
     NONCLUSTERED HASH (o_id,od_id) WITH (BUCKET_COUNT=10000),  
  
     INDEX ix_o_id NONCLUSTERED HASH (o_id) WITH (BUCKET_COUNT=10000)  
  
     ) WITH (MEMORY_OPTIMIZED=ON)  
    ```  
  
 請注意，如果某個索引鍵值具有大量重複的資料列，則記憶體最佳化雜湊索引不會以最佳方式執行：在範例中，如果資料行 o_id 的唯一值數目比資料表中資料列的數目少許多，則在 (o_id) 上加入索引並不是最好的方式，較佳的解決方法是將索引 PK_od 的類型從雜湊變更為非叢集。 如需詳細資訊，請參閱＜ [Determining the Correct Bucket Count for Hash Indexes](../relational-databases/indexes/indexes.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表上的索引](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
