---
title: 將資料行加入查詢 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aef64ed8031664dcbefa7d0e30bf9f63435b292c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52778940"
---
# <a name="add-columns-to-queries-visual-database-tools"></a>將資料行加入查詢 (Visual Database Tools)
  若要在查詢中使用資料行，您必須將資料行加入至查詢。 您可能會加入資料行以便在查詢輸出中顯示資料行、使用資料行進行排序、搜尋資料行內容，或者摘要資料行內容。 您可以決定在執行查詢時，結果窗格中包含哪些查詢中所使用的資料行。 如需詳細資訊，請參閱[移除查詢結果的資料行 &#40;Visual Database Tools&#41;](visual-database-tools.md)。  
  
> [!NOTE]  
>  若要在查詢和檢視表設計工具中檢視資料類型，可以在 [圖表] 窗格中選取資料表或資料表值物件，並且在 [屬性] 視窗中按一下 [資料行清單]。 然後按一下**省略符號 (…)** 以開啟 [資料行清單] 對話方塊。  
  
 無論在何處使用查詢中的資料行，您也可以使用由任何資料行、常值、運算子和函數組合所組成的運算式。  
  
### <a name="to-add-an-individual-column"></a>若要新增個別資料行  
  
-   在 [圖表] 窗格中，選取您要加入的資料行旁邊的核取方塊。  
  
     -或-  
  
-   在 [準則] 窗格中，移至第一個空白的方格資料列，按一下 [ 資料行] 資料行中的欄位，然後從下拉式清單中選取資料行名稱。  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>若要針對一個資料表或資料表值物件新增所有資料行  
  
-   在 **圖表窗格**，選取旁邊的核取方塊 **\*（所有資料行）**。  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>若要針對所有資料表和表格化物件 (Table-Structured Object) 新增所有資料表  
  
1.  請確定 [資料表運算] 窗格中未選取任何聯結線 (Join Line)。  
  
2.  在 [設計] 視窗的空白處按一下滑鼠右鍵，然後從快速鍵功能表中選擇 [屬性]。  
  
3.  在 [屬性] 視窗中，按一下 [輸出全部資料行]，然後從下拉式清單中選擇 [是] 或 [否]。  
  
## <a name="see-also"></a>另請參閱  
 [移除查詢結果中的資料行&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [從查詢移除資料行&#40;Visual Database Tools&#41;](remove-columns-from-queries-visual-database-tools.md)   
 [指定搜尋準則&#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [摘要查詢結果&#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [使用查詢執行基本作業 &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
