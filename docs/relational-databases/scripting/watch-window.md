---
title: "監看式視窗 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vs.debug.watch"
helpviewer_keywords: 
  - "監看式視窗 [Transact-SQL]"
ms.assetid: 23f3baa4-14c2-4262-92f7-3f43fcfa0436
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 監看式視窗
  **[監看式]** 視窗會顯示有關您已選取之運算式的資訊。 最多可以有四個監看式視窗： **Watch 1**、 **Watch 2、Watch 3**和 **Watch 4**。 運算式會在 **[呼叫堆疊]** 視窗內選取的目前呼叫堆疊框架範圍內評估。 您必須在偵錯模式下，才能監看變數和運算式。  
  
## 工作清單  
 **存取監看式視窗**  
  
-   在 **[偵錯]** 功能表上，按一下 **[視窗]**，再按一下 **[監看式]**，然後按一下 **Watch 1**、 **Watch 2、Watch 3**或 **Watch 4**。  
  
 **變更運算式的值**  
  
-   以滑鼠右鍵按一下運算式，然後選取 [編輯值]。  
  
## 資料行  
 **名稱**  
 為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具所列出的運算式。 以下為支援的運算式：  
  
-   變數。  
  
-   參數。  
  
-   名稱開頭為 @@ 的系統函數。  
  
-   透過將運算子套用至一個或多個變數、參數或系統函數 (例如 @IntegerCounter + 1 或 FirstName + LastName) 的方式建立的運算式。  
  
-   傳回單一值的 Transact-SQL 陳述式，例如 SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1。  
  
 **值**  
 顯示當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具評估 [名稱] 內指定的運算式以後所傳回的值。  
  
 如果運算式的長度超過 **[值]** 資料行的寬度，當您將指標放在該運算式的 **[值]** 資料格上方時，工具提示會顯示完整的值。  
  
 **[值]** 資料格內的放大鏡圖示表示可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具視覺化檢視。 在此清單中，您可以指定 **[文字視覺化檢視]**、 **[XML 視覺化檢視]**或 **[HTML 視覺化檢視]**。 若要啟動偵錯工具視覺化檢視，請按一下放大鏡圖示。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具會開啟一個對話方塊，其中會以對資料類型適合的格式顯示資料。  
  
 **型別**  
 顯示此運算式的資料類型。  
  
## 另請參閱  
 [Transact-SQL 偵錯工具](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 偵錯工具資訊](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [本機視窗](../../relational-databases/scripting/locals-window.md)   
 [呼叫堆疊視窗](../../relational-databases/scripting/call-stack-window.md)   
 [快速監看式對話方塊](../../relational-databases/scripting/quickwatch-dialog-box.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  