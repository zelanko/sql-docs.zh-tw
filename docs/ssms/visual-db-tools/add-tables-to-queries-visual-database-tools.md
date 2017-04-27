---
title: "將資料表加入查詢 (Visual Database Tools) | Microsoft Docs"
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
- inserting tables
- adding tables
- queries [SQL Server], tables
ms.assetid: 6551aa7e-31a1-4636-852a-819bc53d658b
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ffa0dc48650d116f76df704ceae1d10f96b2b5be
ms.lasthandoff: 04/11/2017

---
# <a name="add-tables-to-queries-visual-database-tools"></a>將資料表加入查詢 (Visual Database Tools)
建立查詢時，您會從資料表或結構與資料表類似的其他物件 (檢視和某些使用者定義函數) 擷取資料。 若要在查詢中使用上述物件，請將這些物件新增到 [圖表窗格]。  
  
### <a name="to-add-a-table-or-table-valued-object-to-a-query"></a>若要將資料表或資料表值物件加入至查詢  
  
1.  在查詢和檢視表設計工具之 [圖表窗格]的背景上按一下滑鼠右鍵，再從捷徑功能表中選擇 [加入資料表]。  
  
2.  在 [加入資料表] 對話方塊中，選取您要新增到查詢中之物件類型所屬的索引標籤。  
  
3.  在項目清單中，按兩下您要加入的每個項目。  
  
4.  當您完成新增項目時，請按一下 [關閉]。  
  
    查詢和檢視表設計工具會據此更新 [圖表窗格]、[準則窗格]及 [SQL 窗格]。  
  
當您在 [SQL] 窗格的陳述式中參考資料表和檢視時，這些資料表和檢視會自動加入至查詢中。  
  
如果您沒有足夠的存取權限，或如果提供者無法傳回相關資訊，查詢和檢視設計工具將不會顯示資料表或表格化物件 (Table-Structured Object) 的資料行。 在這個情況中，資料表或表格化物件只會顯示標題列和 [* (所有資料行)] 核取方塊。  
  
### <a name="to-add-an-existing-query-to-a-new-query"></a>若要將現有查詢加入至新查詢  
  
1.  請確定您建立的新查詢中顯示有 [SQL 窗格]。  
  
2.  在 [SQL 窗格] 中，於 FROM 一字之後輸入左、右括號 ()。  
  
3.  開啟現有查詢的 [查詢設計工具]  (您現在已開啟兩個 [查詢設計工具])。  
  
4.  顯示內部查詢 (即您要加入所新增之外部查詢現有查詢) 的 [SQL 窗格]。  
  
5.  選取 [SQL 窗格]中的所有文字，再將其複製到剪貼簿中。  
  
6.  按一下新查詢中的 [SQL 窗格]，並將游標置於先前新增的括號之中，然後貼上剪貼簿的內容。  
  
7.  在 [SQL 窗格]中，於右括號之後新增別名。  
  
## <a name="see-also"></a>另請參閱  
[建立資料表別名 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[從查詢移除資料表 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/remove-tables-from-queries-visual-database-tools.md)  
[指定搜尋準則 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[摘要查詢結果 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[使用查詢執行基本作業 &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

