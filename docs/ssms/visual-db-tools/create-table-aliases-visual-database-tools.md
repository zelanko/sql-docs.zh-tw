---
title: 建立資料表別名
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 14c8defcabde99a42993b4f1490094670a890cee
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75254232"
---
# <a name="create-table-aliases-visual-database-tools"></a>建立資料表別名 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
別名可以更容易使用資料表名稱。 在下列狀況時，使用別名會非常有用：  
  
-   讓 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) 中的陳述式更簡短、更容易閱讀。  
  
-   您經常在查詢中參閱資料表名稱 - 例如在限定資料行名稱中 - 並且希望確保維持在查詢的特定字元長度限制內。 (某些資料庫會限制查詢的最大長度)。  
  
-   您使用相同資料表的多個執行個體 (例如自我聯結)，然後需要參考到一個或另外一個執行個體的方式。  
  
例如，您可以針對資料表名稱 `"e"` 建立別名 `employee_information`，然後在整個查詢的其他部分以 `"e"` 的方式參考資料表。  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>若要建立資料表或資料表值物件的別名  
  
1.  將資料表或資料表值物件加入到查詢。  
  
2.  在 [圖表]  窗格中，在想要建立別名的物件按一下滑鼠右鍵，然後從快速鍵功能表中選取 [屬性]  。  
  
3.  在 [屬性]  視窗中的 [別名]  欄位，輸入別名。  
  
## <a name="see-also"></a>另請參閱  
[將資料表新增至查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[摘要查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[使用查詢執行基本作業 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
