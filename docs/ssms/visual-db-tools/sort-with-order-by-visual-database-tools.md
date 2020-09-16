---
description: 使用 ORDER BY 排序 (Visual Database Tools)
title: 使用 ORDER BY 排序
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [Visual Database Tools]
ms.assetid: 459f5640-8058-4c24-97e7-7bbd6168bc39
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 0b356e2fd46ac86b3b4a8060a18e5cc54c10128f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491566"
---
# <a name="sort-with-order-by-visual-database-tools"></a>使用 ORDER BY 排序 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
您可以使用 ORDER BY 子句，藉此根據傳回資料列中的一或多個資料行，排序查詢結果。 您可以在 [準則細節] 窗格中選擇選項，定義 ORDER BY 子句。  
  
### <a name="to-sort-a-query-using-an-order-by-clause"></a>若要使用 ORDER BY 子句排序查詢  
  
1.  開啟查詢或建立新查詢。  
  
2.  在[準則窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，針對對應到您要用來排序查詢結果之資料行的資料列，按一下 [排序類型]****。  
  
3.  從下拉式清單選擇 [遞增]** 或 [遞減]**。  
  
> [!NOTE]  
> 清除資料行的 [排序類型]**** 項目時，會從 ORDER BY 子句移除該資料行。  
  
請注意，使用 [準則] 窗格時，查詢的 UNION 子句會變更，以符合您最近的動作。  
  
> [!NOTE]  
> 使用多個資料行排序結果時，可使用 [排序次序] 欄位指定資料行相互之間搜尋的順序。 如需詳細資訊，請參閱**如何：對查詢中的多個資料行進行排序**。  
  
## <a name="see-also"></a>另請參閱  
[排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[摘要查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
