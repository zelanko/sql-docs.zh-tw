---
title: "估計叢集索引的大小 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- disk space [SQL Server], indexes
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- space [SQL Server], indexes
- clustered indexes, table size
- nonclustered indexes [SQL Server], table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: 2b5137f8-98ad-46b5-9aae-4c980259bf8d
caps.latest.revision: "49"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c750d3887f36b5f8d4a0dd826d6cc1b5e990bf3f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="estimate-the-size-of-a-clustered-index"></a>估計叢集索引的大小
  您可以使用下列步驟，估計在叢集索引中儲存資料所需的空間量：  
  
1.  計算用來在叢集索引的分葉層級中儲存資料的空間。  
  
2.  計算用來儲存叢集索引之索引資訊的空間。  
  
3.  加總計算的值。  
  
## <a name="step-1-calculate-the-space-used-to-store-data-in-the-leaf-level"></a>步驟 1： 計算用來在分葉層級中儲存資料的空間  
  
1.  指定資料表中將會有的資料列數目：  
  
     ***Num_Rows***  = 資料表中的資料列數目  
  
2.  指定固定長度與可變長度資料行的數目，並計算儲存這些資料行所需的空間：  
  
     計算這兩組資料行在資料列內各佔多少空間。 資料行的大小取決於資料類型和長度規格。  
  
     ***Num_Cols***  = 資料行 (固定長度和可變長度) 總數  
  
     ***Fixed_Data_Size***  = 所有固定長度資料行的總位元組大小  
  
     ***Num_Variable_Cols***  = 可變長度資料行的數目  
  
     ***Max_Var_Size***  = 所有可變長度資料行的位元組大小上限  
  
3.  如果叢集索引為非唯一的索引，請將 *uniqueifier* 資料行列入考慮：  
  
     uniqueifier 是可為 Null 的可變長度資料行。 在具有非唯一索引鍵值的資料列中，它將會是非 Null 並且為 4 個位元組大小。 此值是索引鍵的一部分，必須用來確定每個資料列都有唯一的索引鍵值。  
  
     ***Num_Cols***  = ***Num_Cols*** + 1  
  
     ***Num_Variable_Cols***  = ***Num_Variable_Cols*** + 1  
  
     ***Max_Var_Size***  = ***Max_Var_Size*** + 4  
  
     這些修改假設所有值均為非唯一的值。  
  
4.  資料列中有一部分 (稱為 Null 點陣圖) 是保留的空間，用來管理資料行的 Null 屬性。 計算它的大小：  
  
     ***Null_Bitmap***  = 2 + ((***Num_Cols*** + 7) / 8)  
  
     上述運算式中只有整數部分應該使用，請捨棄餘數。  
  
5.  計算可變長度資料的大小：  
  
     如果在索引中有可變長度的資料行，請決定將資料行儲存到索引列中所需的空間大小。  
  
     ***Variable_Data_Size***  = 2 + (***Num_Variable_Cols*** x 2) + ***Max_Var_Size***  
  
     加入 ***Max_Var_Size*** 的位元組是用於追蹤每個可變資料行。 這個公式假設所有可變長度的資料行是 100% 填滿的。 如果您預期可變長度資料行儲存所佔空間的百分比會比較低，您可以經由調整百分比所得的 ***Max_Var_Size*** 值，取得更精確的整體資料表大小。  
  
    > [!NOTE]  
    >  您可以結合使定義的資料表總寬度超過 8,060 個位元組的 **varchar**、 **nvarchar**、 **varbinary**或 **sql_variant** 資料行。 這些資料行的每個長度必須仍然在 **varchar**、 **varbinary**或 **sql_variant** 資料行的 8,000 個位元組限制內，以及 **nvarchar** 資料行的 4,000 個位元組限制。 然而，結合的寬度可能超過資料表中 8,060 位元組的限制。  
  
     如果沒有可變長度資料行，請將 ***Variable_Data_Size*** 設成 0。  
  
6.  計算資料列總大小：  
  
     ***Row_Size***  = ***Fixed_Data_Size*** + ***Variable_Data_Size*** + ***Null_Bitmap*** + 4  
  
     4 這個值是資料列的資料列標頭負擔。  
  
7.  計算每個分頁的資料列數目 (每個分頁包含 8096 個可用位元組)：  
  
     ***Rows_Per_Page***  = 8096 / (***Row_Size*** + 2)  
  
     因為資料列不能跨頁，每個分頁的資料列數目必須無條件捨去小數，而取最接近的整數資料列。 公式中的 2 這個值是給分頁位置陣列中的該資料列項目。  
  
8.  根據指定的 [填滿因數](../../relational-databases/indexes/specify-fill-factor-for-an-index.md) ，計算每個分頁所保留的可用資料列數目：  
  
     ***Free_Rows_Per_Page***  = 8096 x ((100 - ***Fill_Factor***) / 100) / (***Row_Size*** + 2)  
  
     計算中所使用的填滿因數是整數值而不是百分比。 因為資料列不能跨頁，每個分頁的資料列數目必須無條件捨去小數，而取最接近的整數資料列。 當填滿因數變大時，每個分頁上會儲存更多資料，分頁也會比較少。 公式中的 2 這個值是給分頁位置陣列中的該資料列項目。  
  
9. 計算儲存所有資料列所需的分頁數目：  
  
     ***Num_Leaf_Pages***  = ***Num_Rows*** / (***Rows_Per_Page*** - ***Free_Rows_Per_Page***)  
  
     估計的分頁數目應該要將小數進位到最接近的整分頁數。  
  
10. 計算在分葉層級中儲存資料所需的空間量 (每個分頁共有 8192 個位元組)：  
  
     ***Leaf_space_used***  = 8192 x ***Num_Leaf_Pages***  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information"></a>步驟 2： 計算用來儲存索引資訊的空間  
 您可以使用下列步驟，估計儲存較高索引層級所需的空間量：  
  
1.  指定索引鍵中固定長度和可變長度資料行的數目，並計算儲存它們所需的空間：  
  
     索引的索引鍵資料行可以包含固定長度和可變長度的資料行。 若要估計內部層級的索引資料列大小，請計算這些資料行群組在索引資料列中佔用的空間。 資料行的大小取決於資料類型和長度規格。  
  
     ***Num_Key_Cols***  = 索引鍵資料行 (固定長度和可變長度) 總數  
  
     ***Num_Key_Cols***  = 所有固定長度索引鍵資料行的總位元組大小  
  
     ***Num_Variable_Key_Cols***  = 可變長度索引鍵資料行的數目  
  
     ***Max_Var_Key_Size***  = 所有可變長度索引鍵資料行的最大位元組大小  
  
2.  如果索引為非唯一的索引，請將任何所需的 uniqueifier 列入考慮：  
  
     uniqueifier 是可為 Null 的可變長度資料行。 在具有非唯一索引鍵值的資料列中，它將會是非 Null 並且為 4 個位元組大小。 此值是索引鍵的一部分，必須用來確定每個資料列都有唯一的索引鍵值。  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 1  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 1  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 4  
  
     這些修改假設所有值均為非唯一的值。  
  
3.  計算 Null 點陣圖大小：  
  
     若索引鍵中有可為 Null 的資料行，索引資料列的一部分會保留給 Null 點陣圖。 計算它的大小：  
  
     ***Index_Null_Bitmap***  = 2 + ((索引資料列中的資料行數目 + 7) / 8)  
  
     您應該僅使用先前運算式的整數部分。 請捨去任何餘數。  
  
     如果沒有可為 Null 的索引鍵資料行，請將 ***Index_Null_Bitmap*** 設成 0。  
  
4.  計算可變長度資料的大小：  
  
     如果在索引中有可變長度的資料行，請決定要在索引資料列中儲存資料行的空間。  
  
     ***Variable_Key_Size***  = 2 + (***Num_Variable_Key_Cols*** x 2) + ***Max_Var_Key_Size***  
  
     加入 ***Max_Var_Key_Size*** 的位元組是用於追蹤每個可變長度資料行。 這個公式假設所有可變長度的資料行是 100% 填滿的。 如果您預期可變長度資料行所使用的儲存空間百分比會比較小，您可以經由調整百分比所得的 ***Max_Var_Key_Size*** 值，產生更精確的整體資料表大小之估計。  
  
     若沒有可變長度的資料行，請將 ***Variable_Key_Size*** 設成 0。  
  
5.  計算索引資料列的大小：  
  
     ***Index_Row_Size***  = ***Fixed_Key_Size*** + ***Variable_Key_Size*** + ***Index_Null_Bitmap*** + 1 (索引資料列的資料列標頭上方) + 6 (子頁面識別碼指標)  
  
6.  計算每個分頁的索引資料列數目 (每個分頁包含 8096 個可用位元組)：  
  
     ***Index_Rows_Per_Page***  = 8096 / (***Index_Row_Size*** + 2)  
  
     由於索引資料列並不會跨越分頁，因此每個分頁索引資料列的數目應該捨去小數，而取最接近的整數列數。 公式中的 2 是給分頁位置陣列中的該資料列項目。  
  
7.  計算索引中的層級數目：  
  
     ***Non-leaf_Levels***  = 1 + log (Index_Rows_Per_Page) (***Num_Leaf_Pages*** / ***Index_Rows_Per_Page***)  
  
     將這個值無條件向上進位到最近的整數。 此值不包含叢集索引的分葉層級。  
  
8.  計算索引中的非分葉頁面數目：  
  
     ***Num_Index_Pages =*** ∑Level ***(Num_Leaf_Pages / (Index_Rows_Per_Page***^Level***))***  
  
     其中 1 <= Level <= ***Non-leaf_Levels***  
  
     將每個被加數無條件向上進位到最近的整數。 簡單舉例說明，假設有個索引，其中 ***Num_Leaf_Pages*** = 1000 和 ***Index_Rows_Per_Page*** = 25。 分葉層級上方的第一個索引層級會儲存 1000 個索引資料列，這是每個分葉頁面的一個索引資料列，而且每個頁面可以容納 25 個索引資料列。 這表示儲存這 1000 個索引資料列需要 40 頁。 索引的下一個層級必須儲存 40 個資料列， 這表示它需要 2 頁。 索引的最後一個層級必須儲存 2 個資料列。 這表示它需要 1 頁。 這會提供 43 個非分葉索引頁面。 在上述公式中使用這些數字時，結果如下：  
  
     ***Non-leaf_Levels***  = 1 + log(25) (1000 / 25) = 3  
  
     ***Num_Index_Pages*** = 1000/(25^3)+ 1000/(25^2) + 1000/(25^1) = 1 + 2 + 40 = 43，這是範例中所描述的頁數。  
  
9. 計算索引的大小 (每個分頁共有 8192 個位元組)：  
  
     ***Index_Space_Used***  = 8192 x ***Num_Index_Pages***  
  
## <a name="step-3-total-the-calculated-values"></a>步驟 3： 加總計算的值  
 將前兩個步驟所取得的值加總：  
  
 叢集索引大小 (位元組) = ***Leaf_Space_Used*** + ***Index_Space_used***  
  
 上述計算未考慮下列項目：  
  
-   資料分割  
  
     從資料分割而來的空間負擔非常小，但是計算起來很複雜。 不一定要包含它。  
  
-   配置頁面  
  
     至少有一個 IAM 頁面用以追蹤配置到堆積的頁面，但是空間負擔非常小，而且沒有演算法來決定性地計算要使用多少 IAM 頁面。  
  
-   大型物件 (LOB) 值  
  
     決定到底要使用多少空間來儲存 LOB 資料類型 **varchar(max)**、 **varbinary(max)**、 **nvarchar(max)**、 **text**、 **ntext**、 **xml**和 **image** 值的演算法是很複雜的。 只要加上預期的 LOB 值平均大小，乘以 ***Num_Rows***，再將此值加上叢集索引總大小，這就足夠。  
  
-   壓縮  
  
     您無法預先計算壓縮索引的大小。  
  
-   疏鬆資料行  
  
     如需有關疏鬆資料行空間需求的詳細資訊，請參閱＜ [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [叢集與非叢集索引說明](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [估計資料表的大小](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [建立叢集索引](../../relational-databases/indexes/create-clustered-indexes.md)   
 [建立非叢集索引](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [估計非叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)   
 [估計堆積的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [估計資料庫的大小](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
