---
title: 建立資料表別名 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e7172a7b9b17dfa4553d3179d8cc1a880040f13
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63306533"
---
# <a name="create-table-aliases-visual-database-tools"></a>建立資料表別名 (Visual Database Tools)
  別名可以更容易使用資料表名稱。 在下列狀況時，使用別名會非常有用：  
  
-   讓 [SQL 窗格](visual-database-tools.md) 中的陳述式更簡短、更容易閱讀。  
  
-   您經常在查詢中參閱資料表名稱 - 例如在限定資料行名稱中 - 並且希望確保維持在查詢的特定字元長度限制內。 (某些資料庫會限制查詢的最大長度)。  
  
-   您使用相同資料表的多個執行個體 (例如自我聯結)，然後需要參考到一個或另外一個執行個體的方式。  
  
 例如，您可以針對資料表名稱 `"e"` _ `employee`建立別名`information`，然後在整個查詢的其他部份以 `"e"` 的方式參考資料表。  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>若要建立資料表或資料表值物件的別名  
  
1.  將資料表或資料表值物件加入到查詢。  
  
2.  在 [圖表]  窗格中，在想要建立別名的物件按一下滑鼠右鍵，然後從快速鍵功能表中選取 [屬性]  。  
  
3.  在 [屬性]  視窗中的 [別名]  欄位，輸入別名。  
  
## <a name="see-also"></a>另請參閱  
 [將資料表加入至查詢 &#40;Visual Database Tools&#41;](add-tables-to-queries-visual-database-tools.md)   
 [排序和分組查詢結果 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [&#40;Visual Database Tools&#41;匯總查詢結果](summarize-query-results-visual-database-tools.md)   
 [使用查詢執行基本作業 &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
