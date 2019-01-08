---
title: 估計堆積的大小 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- disk space [SQL Server], indexes
- estimating heap size
- size [SQL Server], heap
- space [SQL Server], indexes
- heaps
ms.assetid: 81fd5ec9-ce0f-4c2c-8ba0-6c483cea6c75
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 80ba5505204f592ef04c939b3e84b6f3ca3c7c89
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52778421"
---
# <a name="estimate-the-size-of-a-heap"></a>估計堆積的大小
  您可以使用下列步驟，估計儲存堆積中的資料所需的空間量：  
  
1.  指定資料表中將會有的資料列數目：  
  
     ***Num_Rows***  = 資料表中的資料列數目  
  
2.  指定固定長度與可變長度資料行的數目，並計算儲存這些資料行所需的空間：  
  
     計算這兩組資料行在資料列內各佔多少空間。 資料行的大小取決於資料類型和長度規格。  
  
     ***Num_Cols***  = 資料行 (固定長度和可變長度) 總數  
  
     ***Fixed_Data_Size***  = 所有固定長度資料行的總位元組大小  
  
     ***Num_Variable_Cols***  = 可變長度資料行的數目  
  
     ***Max_Var_Size***  = 所有可變長度資料行的總位元組大小上限  
  
3.  資料列中有一部分 (稱為 Null 點陣圖) 是保留的空間，用來管理資料行的 Null 屬性。 計算它的大小：  
  
     ***Null_Bitmap***  = 2 + ((***Num_Cols*** + 7) / 8)  
  
     您應該僅使用這個運算式的整數部分。 請捨去任何餘數。  
  
4.  計算可變長度資料的大小：  
  
     如果在索引中有可變長度的資料行，請決定將資料行儲存到索引列中所需的空間大小。  
  
     ***Variable_Data_Size***  = 2 + (***Num_Variable_Cols*** x 2) + ***Max_Var_Size***  
  
     加入至 ***Max_Var_Size*** 的位元組是用於追蹤每個可變長度的資料行。 這個公式假設所有可變長度的資料行是 100% 填滿的。 如果您預期可變長度資料行儲存所佔空間的百分比會比較低，您可以經由調整百分比所得的 ***Max_Var_Size*** 值，取得更精確的整體資料表大小。  
  
    > [!NOTE]  
    >  您可以結合使定義的資料表總寬度超過 8,060 個位元組的 `varchar`、`nvarchar`、`varbinary` 或 `sql_variant` 資料行。 這些資料行的每個長度仍必須符合 8,000 個位元組的限制內`varchar`， `nvarchar,``varbinary`，或`sql_variant`資料行。 然而，結合的寬度可能超過資料表中 8,060 位元組的限制。  
  
     如果沒有可變長度資料行，請將 ***Variable_Data_Size*** 設成 0。  
  
5.  計算資料列總大小：  
  
     ***Row_Size***  = ***Fixed_Data_Size*** + ***Variable_Data_Size*** + ***Null_Bitmap*** + 4  
  
     公式中 4 這個值是資料列的資料列標頭負擔。  
  
6.  計算每個分頁的資料列數目 (每個分頁包含 8096 個可用位元組)：  
  
     ***Rows_Per_Page***  = 8096 / (***Row_Size*** + 2)  
  
     因為資料列不能跨頁，每個分頁的資料列數目必須無條件捨去小數，而取最接近的整數資料列。 公式中的 2 這個值是給分頁位置陣列中的該資料列項目。  
  
7.  計算儲存所有資料列所需的分頁數目：  
  
     ***Num_Pages***  = ***Num_Rows*** / ***Rows_Per_Page***  
  
     估計的分頁數目應該要將小數進位到最接近的整分頁數。  
  
8.  計算儲存堆積內的資料所需的空間 (每個頁面共有 8192 個位元組)：  
  
     堆積大小 (位元組) = 8192 x ***Num_Pages***  
  
 上述計算未考慮下列項目：  
  
-   資料分割  
  
     從資料分割而來的空間負擔非常小，但是計算起來很複雜。 不一定要包含它。  
  
-   配置頁面  
  
     至少有一個 IAM 頁面用以追蹤配置到堆積的頁面，但是空間負擔非常小，而且沒有演算法來決定性地計算要使用多少 IAM 頁面。  
  
-   大型物件 (LOB) 值  
  
     若要判斷確切使用多少空間來儲存 LOB 資料類型的演算法`varchar(max)`， `varbinary(max)`， `nvarchar(max)`， `text`， **ntextxml**，和`image`值很複雜。 只要加入預期的 LOB 值平均大小，並將此值加入堆積大小總計，這樣就已足夠。  
  
-   壓縮  
  
     您無法預先計算壓縮堆積的大小。  
  
-   疏鬆資料行  
  
     如需有關疏鬆資料行空間需求的詳細資訊，請參閱＜ [Use Sparse Columns](../tables/use-sparse-columns.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [堆積 &#40;無叢集索引的資料表&#41;](../indexes/heaps-tables-without-clustered-indexes.md)   
 [叢集與非叢集索引說明](../indexes/clustered-and-nonclustered-indexes-described.md)   
 [建立叢集索引](../indexes/create-clustered-indexes.md)   
 [建立非叢集索引](../indexes/create-nonclustered-indexes.md)   
 [估計資料表的大小](estimate-the-size-of-a-table.md)   
 [估計叢集索引的大小](estimate-the-size-of-a-clustered-index.md)   
 [估計非叢集索引的大小](estimate-the-size-of-a-nonclustered-index.md)   
 [估計資料庫的大小](estimate-the-size-of-a-database.md)  
  
  
