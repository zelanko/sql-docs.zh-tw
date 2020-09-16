---
description: 排除重複的資料列 (Visual Database Tools)
title: 排除重複的資料列
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: fcd3d8c3b45e98c6fe0d46c8f596c1d5ff42a8ac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497152"
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>排除重複的資料列 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
如果您只想在結果集中查看唯一的值，您可以指定您要從結果集排除重複的項目。  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>若要從結果集排除重複資料列  
  
1.  在 [圖表] 窗格的背景上按一下滑鼠右鍵，然後從快速鍵功能表中選擇 [屬性]****。  
  
2.  在 [屬性] 視窗中，按一下 [重複資料僅顯示一筆]****，並且將值設定為 [是]****。  
  
    [查詢和檢視設計師] 會將關鍵字 DISTINCT 插入至 SQL 陳述式中顯示資料行清單的前面。  
  
    > [!NOTE]  
    > 如果使用 DISTINCT 關鍵字，您可能無法在 [結果] 窗格中修改結果集。  
  
## <a name="see-also"></a>另請參閱  
[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
