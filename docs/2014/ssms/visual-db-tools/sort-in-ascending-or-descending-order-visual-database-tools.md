---
title: 以遞增或遞減順序排序 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cdf37ab5b61e74ab04b9b58162325b580675c493
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63070778"
---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>以遞增或遞減順序排序 (Visual Database Tools)
  您可以使用 `ASC` 或 `DESC` 關鍵字搭配 `ORDER BY` 子句，針對結果集中一個或多個資料行，將查詢結果按照遞增或遞減排序。  
  
> [!NOTE]  
>  排序次序一部份取決於資料行的定序序列。 您可以在 [定序對話方塊](visual-database-tools.md)中變更定序序列。  
  
 以下程序假設您已經在查詢和檢視設計工具中使用 ORDER BY 子句排序一個或多個資料行開啟查詢。  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>指定或變更已經排序結果的順序  
  
1.  在 [準則窗格](criteria-pane-visual-database-tools.md) 中，對要重新排序的資料行按一下 [排序類型]  欄位。  
  
2.  選擇 [遞增]  或 [遞減]  以指定資料行的排序順序。  
  
 請注意，使用 [準則] 窗格時，查詢的 UNION 子句會變更，以符合您最近的動作。  
  
> [!NOTE]  
>  使用多個資料行排序結果時，可使用 [排序次序] 欄位指定資料行相互之間搜尋的順序。 如需詳細資訊，請參閱[排序查詢中的多個資料行 &#40;Visual Database Tools&#41;](sort-multiple-columns-in-queries-visual-database-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
 [排序和分組查詢結果 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [&#40;Visual Database Tools&#41;匯總查詢結果](summarize-query-results-visual-database-tools.md)   
 [設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
