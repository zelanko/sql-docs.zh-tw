---
title: 基數估計 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.openlocfilehash: 5a81849f65e5b71acf233febb61e7725ec1e804e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031843"
---
# <a name="cardinality-estimation-sql-server"></a>基數估計 (SQL Server)
  基數估計邏輯，稱為基數估計工具經過重新設計中[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]來改善查詢計畫品質，因此若要改善查詢效能。 新的基數估計工具併入了可搭配新型 OLTP 和資料倉儲工作負載完善運作的假設和演算法。 這項發展乃是憑藉著我們針對新型工作負載進行深入的基數估計研究，以及過去 15 年來改進 SQL Server 基數估計工具的經驗。 由客戶的意見反應得知，儘管無論變更與否都能讓大多數的查詢獲益，但與舊版基數估計工具相比，少數的查詢可能會顯現效能退化。  
  
> [!NOTE]  
>  基數估計值是對查詢結果中的資料列數所做的預測。 查詢最佳化工具會使用這些估計值選擇執行查詢的計劃。 查詢計劃的品質對於提升查詢效能有著直接的影響。  
  
## <a name="performance-testing-and-tuning-recommendations"></a>效能測試與微調建議  
 在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中建立的所有新資料庫都將啟用新的基數估計工具。 不過，升級到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 並不會為現有的資料庫啟用新的基數估計工具。  
  
 為確保獲得最佳查詢效能，請使用以下建議搭配新的基數估計工具測試您的工作負載，然後再由實際執行系統予以啟用。  
  
1.  升級所有現有的資料庫以使用新的基數估計工具。 若要這樣做，請使用[ALTER DATABASE 相容性層級&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)資料庫相容性層級設定為 120。  
  
2.  搭配新的基數估計工具執行您的測試工作負載，然後依照您目前疑難排解效能問題的相同方式，疑難排解任何新的效能問題。  
  
3.  一旦您的工作負載以執行新的基數估計工具 （資料庫相容性層級 120 (SQL Server 2014)），而特定查詢具有迴歸，您可以使用追蹤旗標 9481 使用中使用的基數估計工具版本來執行查詢[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更早版本。 若要使用追蹤旗標執行查詢，請參閱知識庫文件＜ [啟用會影響計劃而可在特定的查詢層級透過不同的追蹤旗標加以控制的 SQL Server 查詢最佳化工具行為](http://support.microsoft.com/kb/2801413)＞(機器翻譯)。  
  
4.  如果您不能變更所有資料庫，一次，以便使用新的基數估計工具，您可以使用的所有資料庫使用原先的基數估計工具[ALTER DATABASE 相容性層級&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)至設定資料庫相容性層級為 110。  
  
5.  如果您是以資料庫相容性層級 110 執行工作負載，而想要搭配新的基數估計工具來測試或執行特定的查詢，請用追蹤旗標 2312 執行查詢，即可使用 SQL Server 2014 版本的基數估計工具。  若要使用追蹤旗標執行查詢，請參閱知識庫文件＜ [啟用會影響計劃而可在特定的查詢層級透過不同的追蹤旗標加以控制的 SQL Server 查詢最佳化工具行為](http://support.microsoft.com/kb/2801413)＞(機器翻譯)。  
  
## <a name="new-xevents"></a>新的 XEvents  
 現已有兩個新的 query_optimizer_estimate_cardinality XEvents 支援新的查詢計劃。  
  
-   *query_optimizer_estimate_cardinality* 會在查詢最佳化工具估計關聯運算式的基數時發生。  
  
-   *query_optimizer_force_both_cardinality_estimation*_behaviors 會在一併啟用追蹤旗標 2312 和 9481 而嘗試同時強制新舊兩版的基數估計行為時發生。  
  
## <a name="examples"></a>範例  
 下列範例示範新的基數估計值的部分變更。 估計基數的程式碼已經改寫。 其邏輯相當複雜，因此無法提供所有變更的詳盡清單。  
  
> [!NOTE]  
>  這些範例的用意是提供概念性資訊。 您不需要採取任何動作變更資料庫和查詢的設計方式。  
  
### <a name="example-a-new-cardinality-estimates-use-an-average-cardinality-for-recently-added-ascending-data"></a>範例 A：新的基數估計值會針對最近加入的遞增資料使用平均基數  
 此範例示範新的基數估計工具如何針對在最近更新統計資料期間超出資料表最大值的遞增資料，改善基數估計值。  
  
```  
SELECT item, category, amount FROM dbo.Sales AS s WHERE Date = '2013-12-19';  
```  
  
 在此範例中，Sales 資料表每天都會加入新的資料列，而查詢則要求 12/19/2013 當天的銷售額，且統計資料上次更新的日期是 12/18/2013。 舊版基數估計工具會假設 12/19/2013 的值不存在，因為該日期並未超過最大日期，而且統計資料尚未更新成包含 12/19/2013 的值。 如果您是載入當天的資料，然後對統計資料更新之前的資料執行查詢，就會發生這種情況，又稱為遞增索引鍵問題。  
  
 此行為已經變更。 現在，即使統計資料尚未更新到自從統計資料上次更新後最近加入的遞增資料，新的基數估計工具也將假設其值存在，並且使用資料行內每個值的平均基數做為基數估計值。  
  
### <a name="example-b-new-cardinality-estimates-assume-filtered-predicates-on-the-same-table-have-some-correlation"></a>範例 B：新的基數估計值會假設相同資料表上的篩選述詞具有若干相互關聯性  
 此範例假設 Cars 資料表有 1000 個資料列，其中 Make (品牌) 符合 'Honda' 者為 200 列，Model (車款) 符合 'Civic' 者為 50 列，而且所有的 Civic 車款都是 Honda 品牌。 因此，Make 資料行的值有 20% 為 'Honda'，Model 資料行的值有 5% 為 'Civic'，而且 Honda Civic 的實際數目是 50。 原本的基數估計值假設 Make 和 Model 資料行的值彼此獨立。 舊版查詢最佳化工具估計的結果為 10 部 Honda Civic (.05 *.20 \* 1000 個資料列 = 10 個資料列)。  
  
```  
SELECT year, purchase_price FROM dbo.Cars WHERE Make = 'Honda' AND Model = 'Civic';  
```  
  
 此行為已經變更。 現在，新的基數估計值會假設 Make 和 Model 資料行具有「若干」  相互關聯性。 查詢最佳化工具會為估計方程式加入指數元件，以估計出較高的基數。 查詢最佳化工具現在估計，22.36 個資料列 (.05 * SQRT(.20) \* 1000 個資料列 = 22.36 個資料列) 符合述詞。 就此案例和具體資料分佈來看，22.36 個資料列更趨近於查詢將會傳回的實際數目 50 個資料列。  
  
 請注意，新的基數估計工具邏輯會對述詞選擇性排序並增加指數乘冪。 例如，若述詞選擇性是.05、.20 和.25，基數估計值即為 (.05 * SQRT(.20) \* .25)。  
  
### <a name="example-c-new-cardinality-estimates-assume-filtered-predicates-on-different-tables-are-independent"></a>範例 C：新的基數估計值會假設不同資料表上的篩選述詞彼此無關  
 就此範例而言，舊版基數估計工具假設述詞篩選 s.type 和 r.date 相互關聯。 不過，對新型工作負載測試的結果顯示，不同資料表中各資料行的述詞篩選通常並非彼此相互關聯。  
  
```  
SELECT s.ticket, s.customer, r.store FROM dbo.Sales AS s CROSS JOIN dbo.Returns AS r  
WHERE s.ticket = r.ticket AND s.type = 'toy' AND r.date = '2013-12-19';  
```  
  
 此行為已經變更。 現在，新的基數估計工具邏輯會假設 s.type 並未與 r.date 相互關聯。 實際的講法就是，其假設每天都會有玩具退貨，而非只限特定的哪一天。 在此情況下，新的基數估計值將小於原本的基數估計值。  
  
## <a name="see-also"></a>另請參閱  
 [效能的監視與微調](monitor-and-tune-for-performance.md)  
  
  
