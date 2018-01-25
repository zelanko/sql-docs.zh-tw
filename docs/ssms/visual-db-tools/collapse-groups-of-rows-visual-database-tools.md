---
title: "摺疊資料列群組 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- group collapsing [SQL Server]
- collapsing rows
- row collapsing [SQL Server]
ms.assetid: 7338dad0-965d-44ba-8c1a-b993acb7156d
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4bc579ff02d58fbc4a06800af44e5eb514977aac
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="collapse-groups-of-rows-visual-database-tools"></a>摺疊資料列群組 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 可以建立一種查詢結果，其中各結果資料列對應至原始資料的完整資料列群組。 摺疊資料列時，請注意下列事項：  
  
-   **您可以排除重複的資料列** ：有些查詢建立的結果集中會產生許多完全相同的資料列。 例如，您可以建立結果集，其中每個資料列都包含城市以及某個城市 (含有一個作者) 所在的州名 － 但如果某個城市含有數個作者，則將產生數個相同的資料列。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT city, state  
    FROM authors  
    ```  
  
    上述查詢產生的結果集並不是很有用。 如果某個城市含有四個作者，該結果集將包含四個完全一樣的資料列。 由於結果列不包含城市和州以外的資料行，因此無法進一步區分這些完全相同的資料行。 要避免這種重複的資料列，將其他可區分這些資料列的其他資料行納入結果集。 例如，如果您納入作者名稱，則每個資料列都將變成不同 (假設任何一個城市中並沒有兩個命名相似的作者)。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT city, state, fname, minit, lname  
    FROM authors  
    ```  
  
    當然上述查詢只可排除這個問題，但無法真正解決該問題。 也就是說，雖然該結果集中沒有重複項目，但它再也不是城市的結果集了。 若要排除原始結果集中的重複項目，但同時仍然保有每個說明城市的資料列，您可以建立僅傳回不同資料列的查詢。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT DISTINCT city, state  
    FROM authors  
    ```  
  
    如需排除重複項目的詳細資訊，請參閱[排除重複的資料列 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/exclude-duplicate-rows-visual-database-tools.md)。  
  
-   **您可以計算資料列群組**：也就是說，您可以摘要報告資料列群組的資訊。 例如，您可以建立結果集，其中每個資料列都含有城市和含有某位作者的城市所在州名，以及該城市所含之作者數目。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ```  
  
    如需計算資料列群組的詳細資訊，請參閱[摘要查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md) 和 [排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)。  
  
-   **您可以使用選擇標準來包含資料列群組**：例如，您可以建立結果集，其中每個資料列都包含城市和含有數位作者的城市所在州名，以及該城市所含之作者數目。 產生的 SQL 將如下所示：  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    HAVING COUNT(*) > 1  
    ```  
  
    如需對資料列群組套用選取準則的詳細資訊，請參閱[指定群組條件 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-conditions-for-groups-visual-database-tools.md) 和[在相同查詢中使用 HAVING 和 WHERE 子句 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
