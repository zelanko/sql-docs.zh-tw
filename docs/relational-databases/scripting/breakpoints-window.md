---
title: "中斷點視窗 | Microsoft Docs"
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
  - "vs.debug.breakpoints"
helpviewer_keywords: 
  - "中斷點視窗 [Transact-SQL]"
ms.assetid: bad88d10-fdd5-4d3d-b5ea-a4f063847485
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 中斷點視窗
  [中斷點] 視窗會列出目前 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中設定的所有中斷點。 若要管理中斷點，請使用 [中斷點] 視窗內的工具列。 中斷點是偵錯模式下暫停執行的程式碼位置，好讓您可以檢視偵錯資料。  
  
## 工作清單  
 **存取中斷點視窗**  
  
-   在 **[偵錯]** 功能表上，按一下 **[視窗]**，然後按一下 **[中斷點]**。  
  
## 中斷點視窗資料行  
 根據預設，[中斷點] 視窗會列出以下資料行。  
  
 **名稱**  
 顯示中斷點的名稱。 中斷點名稱是由偵錯工具所提供。 此名稱包含內含中斷點的 Database Engine 查詢編輯器視窗名稱，以及查詢編輯器內中斷點設定所在的行號。  
  
 **條件**  
 顯示 [(無條件)]。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具不支援中斷點條件的設定。  
  
 **叫用計數**  
 顯示 [永遠中斷]。  
  
 您可以加入及移除以下資料行，其方式是在 [資料行] 清單中選取這些資料行。  
  
 **篩選**  
 顯示 [(無)]。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具不支援中斷點篩選的設定。  
  
 **叫用時**  
 顯示 [中斷]。  
  
 **語言**  
 顯示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的 [Transact-SQL]。  
  
 **函數**  
 顯示設定中斷點的行號。  
  
 **檔案**  
 顯示包含中斷點的來源檔案名稱以及設定中斷點的行號。  
  
 **位址**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具不支援這個功能。  
  
 **處理**  
 顯示 [SQL] 來指示這個是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理序。 這後面接著程式碼執行所在的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體名稱。  
  
## 中斷點視窗工具列  
 當目前的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [查詢編輯器] 視窗有使用中的中斷點時，[中斷點] 視窗會顯示一個可用來管理中斷點的工具列。  
  
 **Delete**  
 刪除選取的中斷點。  
  
 **刪除所有中斷點**  
 刪除 [中斷點] 視窗內顯示的所有中斷點。  
  
 **停用所有中斷點**  
 停用所有中斷點，好讓它們不再停止執行程式碼；但是，中斷點仍會留著。 當所有中斷點都停用以後，這個按鈕會變成 [啟用所有中斷點]。  
  
 **啟用所有中斷點**  
 啟用所有中斷點，好讓它們停止執行程式碼。 當所有中斷點都啟用以後，這個按鈕會變成 [停用所有中斷點]。  
  
 **移至原始程式碼**  
 將游標放在查詢編輯器中包含選定中斷點的那一行上面。  
  
 **資料行**  
 列出可以在 [中斷點] 視窗內顯示的所有資料行。 核取方塊表示已選取資料行。 若要加入或移除 [中斷點] 視窗中的資料行，請在清單中選取該資料行。  
  
## 另請參閱  
 [Transact-SQL 偵錯工具](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  