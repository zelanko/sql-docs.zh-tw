---
title: 使用 ORDER BY 排序 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [Visual Database Tools]
ms.assetid: 459f5640-8058-4c24-97e7-7bbd6168bc39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30a2fca3dd0f2fcc6f22f2330c37fb8e333d9994
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771930"
---
# <a name="sort-with-order-by-visual-database-tools"></a>使用 ORDER BY 排序 (Visual Database Tools)
  您可以使用 ORDER BY 子句，藉此根據傳回資料列中的一或多個資料行，排序查詢結果。 您可以在 [準則細節] 窗格中選擇選項，定義 ORDER BY 子句。  
  
### <a name="to-sort-a-query-using-an-order-by-clause"></a>若要使用 ORDER BY 子句排序查詢  
  
1.  開啟查詢或建立新查詢。  
  
2.  在[準則窗格](visual-database-tools.md)中，針對對應到您要用來排序查詢結果之資料行的資料列，按一下 [排序類型]。  
  
3.  從下拉式清單選擇 [遞增] 或 [遞減]。  
  
> [!NOTE]  
>  清除資料行的 [排序類型] 項目時，會從 ORDER BY 子句移除該資料行。  
  
 請注意，使用 [準則] 窗格時，查詢的 UNION 子句會變更，以符合您最近的動作。  
  
> [!NOTE]  
>  使用多個資料行排序結果時，可使用 [排序次序] 欄位指定資料行相互之間搜尋的順序。 如需詳細資訊，請參閱**How to:排序查詢中的多個資料行**。  
  
## <a name="see-also"></a>另請參閱  
 [排序及群組查詢結果&#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [摘要查詢結果&#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
