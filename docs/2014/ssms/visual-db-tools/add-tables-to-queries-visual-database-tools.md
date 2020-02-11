---
title: 將資料表加入查詢 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting tables
- adding tables
- queries [SQL Server], tables
ms.assetid: 6551aa7e-31a1-4636-852a-819bc53d658b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ba3957eb5b0c88396376d615033107b13d0621ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63297859"
---
# <a name="add-tables-to-queries-visual-database-tools"></a>將資料表加入查詢 (Visual Database Tools)
  建立查詢時，您會從資料表或結構與資料表類似的其他物件 (檢視和某些使用者定義函式) 擷取資料。 若要在查詢中使用上述物件，請將這些物件新增到 [圖表窗格]  。  
  
### <a name="to-add-a-table-or-table-valued-object-to-a-query"></a>若要將資料表或資料表值物件加入至查詢  
  
1.  在查詢和檢視表設計工具之 [圖表窗格]  的背景上按一下滑鼠右鍵，再從捷徑功能表中選擇 [加入資料表]  。  
  
2.  在 [加入資料表]  對話方塊中，選取您要新增到查詢中之物件類型所屬的索引標籤。  
  
3.  在項目清單中，按兩下您要加入的每個項目。  
  
4.  當您完成新增項目時，請按一下 [關閉]  。  
  
     查詢和檢視表設計工具會據此更新 [圖表窗格]  、[準則窗格]  及 [SQL 窗格]  。  
  
 當您在 [SQL] 窗格的陳述式中參考資料表和檢視時，這些資料表和檢視會自動加入至查詢中。  
  
 如果您沒有足夠的存取權限，或如果提供者無法傳回相關資訊，查詢和檢視設計工具將不會顯示資料表或表格化物件 (Table-Structured Object) 的資料行。 在這個情況中，資料表或表格化物件只會顯示標題列和 [* (所有資料行)] 核取方塊。  
  
### <a name="to-add-an-existing-query-to-a-new-query"></a>若要將現有查詢加入至新查詢  
  
1.  請確定您建立的新查詢中顯示有 [SQL 窗格]  。  
  
2.  在 [SQL 窗格]  中，於 FROM 一字之後輸入左、右括號 ()。  
  
3.  開啟現有查詢的 [查詢設計工具] \(您現在已開啟兩個 [查詢設計工具])。  
  
4.  顯示內部查詢 (即您要加入所新增外部查詢之現有查詢) 的 [SQL 窗格]  。  
  
5.  選取 [SQL 窗格]  中的所有文字，再將其複製到剪貼簿中。  
  
6.  按一下新查詢中的 [SQL 窗格]  ，並將游標置於先前新增的括號之中，然後貼上剪貼簿的內容。  
  
7.  在 [SQL 窗格]  中，於右括號之後新增別名。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Visual Database Tools 建立資料表別名&#41;](visual-database-tools.md)   
 [從查詢中移除資料表 &#40;Visual Database Tools&#41;](remove-tables-from-queries-visual-database-tools.md)   
 [&#40;Visual Database Tools 指定搜尋準則&#41;](specify-search-criteria-visual-database-tools.md)   
 [&#40;Visual Database Tools&#41;匯總查詢結果](summarize-query-results-visual-database-tools.md)   
 [使用查詢執行基本作業 &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
