---
title: 指定群組條件 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query groups
- group query conditions [SQL Server]
ms.assetid: 269ad9c5-3261-4526-badf-7be3c869f229
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8fbf1ea1a9793ae8d0aad56ee6f524e2e225d26a
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65098959"
---
# <a name="specify-conditions-for-groups-visual-database-tools"></a>指定群組條件 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以指定套用至整體群組的條件 (即 HAVING 子句)，以限制出現在查詢中的群組。 在資料經過分組及彙總 (Aggregate) 之後，便會套用 HAVING 子句中的條件。 只有符合條件的群組才會出現在查詢結果中。  
  
例如，您可能想查看 `titles` 資料表中每個發行者的所有書籍的平均價格，但是只限於平均價格超過 $10.00。 在此情況下，您可以指定包含 `AVG(price) > 10`之類條件的 HAVING 子句。  
  
> [!NOTE]  
> 在某些情況下，您可能想在將條件套用到整體群組之前，從群組排除個別的資料列。 如需詳細資訊，請參閱[在相同查詢中使用 HAVING 和 WHERE 子句 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md)。  
  
您可以使用 AND 和 OR 連結條件，以建立 HAVING 子句的複雜條件。 如需在搜尋條件中使用 AND 和 OR 的詳細資訊，請參閱[指定單一資料行的多重搜尋條件 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md)。  
  
### <a name="to-specify-a-condition-for-a-group"></a>若要指定群組條件  
  
1.  為您的查詢指定群組。 如需詳細資訊，請參閱[群組查詢結果中的資料列 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md)。  
  
2.  如果[準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中沒有您要做為條件基礎的資料行，請新增它。 (條件通常牽涉已經是群組或摘要資料行的資料行)。您無法使用不屬於彙總函式 (Aggregate Function) 或 GROUP BY 子句一部分的資料行。  
  
3.  在 [篩選條件] 欄位中，指定要套用至群組的條件。  
  
    [查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)會自動在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)的陳述式中建立 HAVING 子句，如下列範例所示：  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
4.  對想要指定的每個額外條件重複步驟 2 和 3。  
  
## <a name="see-also"></a>另請參閱  
[排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
