---
title: 以遞增或遞減順序排序
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: fbef85b0211b49319298b29f7e935d6c2bc51db4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75255034"
---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>以遞增或遞減順序排序 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以使用  或  關鍵字搭配  子句，以遞增或遞減的方式，排序結果集中一個或多個資料行內的查詢結果。  
  
> [!NOTE]  
> 排序次序一部份取決於資料行的定序序列。 您可以在 [定序對話方塊](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md)中變更定序序列。  
  
以下程序假設您已經在查詢和檢視設計工具中使用 ORDER BY 子句排序一個或多個資料行開啟查詢。  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>指定或變更已經排序結果的順序  
  
1.  在 [準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) 中，對要重新排序的資料行按一下 [排序類型]  欄位。  
  
2.  選擇 [遞增]  或 [遞減]  以指定資料行的排序順序。  
  
請注意，使用 [準則] 窗格時，查詢的 UNION 子句會變更，以符合您最近的動作。  
  
> [!NOTE]  
> 使用多個資料行排序結果時，可使用 [排序次序] 欄位指定資料行相互之間搜尋的順序。 如需詳細資訊，請參閱[排序查詢中的多個資料行 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-multiple-columns-in-queries-visual-database-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
[排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[摘要查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
