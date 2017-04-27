---
title: "以遞增或遞減順序排序 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d287c698a353442efa64c9195702540e4b52f522
ms.lasthandoff: 04/11/2017

---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>以遞增或遞減順序排序 (Visual Database Tools)
您可以使用  或  關鍵字搭配  子句，以遞增或遞減的方式，排序結果集中一個或多個資料行內的查詢結果。  
  
> [!NOTE]  
> 排序次序一部份取決於資料行的定序序列。 您可以在 [定序] [](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md)對話方塊中變更定序序列。  
  
以下程序假設您已經在查詢和檢視設計工具中使用 ORDER BY 子句排序一個或多個資料行開啟查詢。  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>指定或變更已經排序結果的順序  
  
1.  在 [準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) 中，對要重新排序的資料行按一下 [排序類型] 欄位。  
  
2.  選擇 [遞增] 或 [遞減]以指定資料行的排序順序。  
  
請注意，使用 [準則窗格] 時，查詢的 UNION 子句會變更，以符合您最近的動作。  
  
> [!NOTE]  
> 使用多個資料行排序結果時，可使用 [排序次序] 欄位指定資料行相互之間搜尋的順序。 如需詳細資訊，請參閱[排序查詢中的多個資料行 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-multiple-columns-in-queries-visual-database-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
[排序及分組查詢結果 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[摘要查詢結果 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  

