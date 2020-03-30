---
title: 準則窗格
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Criteria pane
- View Designer, Criteria pane
- entering query options into grid [SQL Server]
- Criteria pane
- inserting query options into grid
- grid showing query options [SQL Server]
- adding query options into grid
ms.assetid: 6291affe-580e-482f-a7ff-45ce3837956a
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 2e7bc19ea897e370617aeb8e0e0995e857489464
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75258706"
---
# <a name="criteria-pane-visual-database-tools"></a>準則窗格 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
只要將您的選擇輸入於類似方格的試算表，[準則] 窗格便可以讓您指定查詢選項 (例如，要顯示的資料行、如何排序結果，以及要選取的資料列)。 您可以在 [準則窗格] 中指定下列項目：  
  
-   要顯示的資料行和資料行名稱別名 (Alias)。  
  
-   資料行所屬的資料表。  
  
-   計算資料行之運算式。  
  
-   查詢的排序次序。  
  
-   搜尋條件。  
  
-   群組準則，包括摘要報告使用的彙總函式 (Aggregate Function)。  
  
-   UPDATE 或 INSERT INTO 查詢的新值  
  
-   INSERT FROM 查詢的目標資料行名稱。  
  
您在 [準則窗格] 中的變更將自動反映在 [圖表窗格] 和 [SQL 窗格] 中。 同樣的，[準則窗格] 會自動更新，以反映其他窗格的變更。  
  
## <a name="about-the-criteria-pane"></a>關於準則窗格  
[準則窗格] 的資料列顯示查詢中所用的資料行；[準則] 窗格中的資料行則顯示查詢選項。  
  
[準則窗格] 顯示的特定資訊將視您建立的查詢類型而定。  
  
若 [準則窗格] 未出現，請在設計師工具上按一下滑鼠右鍵，再指向 [窗格]  ，然後按一下 [準則]  。  
  
## <a name="options"></a>選項。  
  
|**資料行**|**查詢類型**|**說明**|  
|--------------|------------------|-------------------|  
|資料行|全部|顯示查詢使用的資料行名稱或計算資料行的運算式。 這個資料行將被鎖定，以便當您水平捲動時，都可以看到這個資料行。|  
|Alias|SELECT、INSERT FROM、UPDATE、MAKE TABLE|指定替代的資料行名稱或可用於計算資料行名稱。|  
|Table|SELECT、INSERT FROM、UPDATE、MAKE TABLE|指定關聯資料行的資料表或表格化物件名稱。 如果是計算資料行，這個欄位是空白的。|  
|輸出|SELECT、INSERT FROM、MAKE TABLE|指定查詢輸出中是否出現資料行。<br /><br />注意：若資料庫允許，您無須在結果集中顯示資料行，就能使用資料行來排序或搜尋子句。|  
|排序類型|SELECT、INSERT FROM|指定使用關聯資料欄來排序查詢結果，及其排序是否為遞增或遞減排序。|  
|排序次序|SELECT、INSERT FROM|指定用來排序結果集的資料行之排序優先順序。 當您變更資料行的排序次序時，所有其他資料行的排序次序也會一併更新。|  
|群組依據|SELECT、INSERT FROM、MAKE TABLE|指定使用關聯資料行來建立彙總查詢。 僅當您從 [工具]  功能表中選擇 [群組依據]  ，或將 GROUP BY 子句新增到 [SQL 窗格] 中，才會顯示格線欄。<br /><br />此資料行的預設值為 [群組依據]  ，而且此資料行將會成為 GROUP BY 子句的一部分。<br /><br />當您移到這個資料行的資料格並選取要套用到關聯資料行的彙總函式時，依照預設，其產生的運算式將加入至結果集並成為輸出資料行。|  
|準則|全部|指定關聯資料行的搜尋條件 (篩選條件)。 輸入運算子 (預設值為「=」) 及要搜尋的值。 使用單引號括住文字值。<br /><br />如果關聯資料行為 GROUP BY 子句的一部份，您輸入的運算式將供 HAVING 子句使用。<br /><br />若您在 [準則]  格線欄中，為多個資料格輸入值，產生的搜尋條件將會自動連結到邏輯 AND。<br /><br />若要為單一資料庫資料行指定多個搜尋條件運算式 (例如 (fname > 'A') AND (fname < 'M'))，可將資料行新增到 [準則窗格] 兩次，再個別於 [準則]  格線欄中，為每個資料行執行個體輸入值。|  
|或...|全部|指定資料行的其他搜尋條件運算式，連結至之前使用邏輯 OR 的運算式。 您可以按最右邊 [或...]  資料行中的 TAB 鍵，新增更多的 [或...]  格線欄。|  
|附加|INSERT FROM|指定相關資料行的目標資料行名稱。 當您建立 Insert From 查詢時，查詢和檢視設計工具將嘗試比對來源和正確的目標資料行。 如果查詢和檢視設計工具無法選擇符合的項目，您必須提供資料行名稱。|  
|新值|UPDATE、NSERT INTO|指定要放入關聯資料行的值。 輸入常值 (Literal) 或運算式。|  
  
## <a name="see-also"></a>另請參閱  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[圖表窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[輸入搜尋值的規則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[結果窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
[SQL 窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)  
  
