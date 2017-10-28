---
title: "將資料行加入查詢 (Visual Database Tools) | Microsoft Docs"
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
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7190609525c847d4a7ff62899e2e5879d41e04af
ms.contentlocale: zh-tw
ms.lasthandoff: 08/18/2017

---
# <a name="add-columns-to-queries-visual-database-tools"></a>將資料行加入查詢 (Visual Database Tools)
若要在查詢中使用資料行，您必須將資料行加入至查詢。 您可能會加入資料行以便在查詢輸出中顯示資料行、使用資料行進行排序、搜尋資料行內容，或者摘要資料行內容。 您可以決定在執行查詢時，結果窗格中包含哪些查詢中所使用的資料行。 如需詳細資訊，請參閱[移除查詢結果的資料行 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)。  
  
> [!NOTE]  
> 若要在查詢和檢視表設計工具中檢視資料類型，可以在 [圖表] 窗格中選取資料表或資料表值物件，並且在 [屬性] 視窗中按一下 [資料行清單]。 再按省略符號 (**…**) 以開啟 [資料行清單] 對話方塊。  
  
無論在何處使用查詢中的資料行，您也可以使用由任何資料行、常值、運算子和函數組合所組成的運算式。  
  
### <a name="to-add-an-individual-column"></a>若要新增個別資料行  
  
-   在 [圖表] 窗格中，選取您要加入的資料行旁邊的核取方塊。  
  
    -或-  
  
-   在 [準則] 窗格中，移至第一個空白的方格資料列，按一下 [ 資料行] 資料行中的欄位，然後從下拉式清單中選取資料行名稱。  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>若要針對一個資料表或資料表值物件新增所有資料行  
  
-   在 [圖表] 窗格中，選取 [\&#42;(所有資料行)] 旁邊的核取方塊。  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>若要針對所有資料表和表格化物件 (Table-Structured Object) 新增所有資料表  
  
1.  請確定 [資料表運算] 窗格中未選取任何聯結線 (Join Line)。  
  
2.  在 [設計] 視窗的空白處按一下滑鼠右鍵，然後從快速鍵功能表中選擇 [屬性]。  
  
3.  在 [屬性] 視窗中，按一下 [輸出全部資料行]，然後從下拉式清單中選擇 [是] 或 [否]。  
  
## <a name="see-also"></a>另請參閱  
[移除查詢結果的資料行 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
[移除查詢的資料行 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-queries-visual-database-tools.md)  
[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[摘要查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[使用查詢執行基本作業 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

