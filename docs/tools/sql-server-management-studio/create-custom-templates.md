---
title: "建立自訂範本 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "tql"
  - "範本 [Transact-SQL], 建立"
  - "範本 [Transact-SQL]"
ms.assetid: 41098e78-b482-410e-bfe8-2ac10769ac4a
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 建立自訂範本
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了許多一般工作的範本，但範本真正的威力，在於能夠建立您經常需要建立之複雜指令碼的自訂範本。 在這個練習中，您將利用幾個參數來建立簡單的指令碼，但冗長而重複的指令碼也適合使用範本。  
  
## 使用自訂範本  
  
#### 若要建立自訂範本  
  
1.  在範本總管中，展開 [SQL Server 範本]，以滑鼠右鍵按一下 [預存程序]，指向 [新增]，然後按一下 [資料夾]。  
  
2.  輸入 **Custom** 作為新範本資料夾的名稱，然後按 ENTER 鍵。  
  
3.  以滑鼠右鍵按一下 [Custom]，指向 [新增]，然後按一下 [範本]。  
  
4.  輸入 **WorkOrdersProc** 作為新範本的名稱，然後按 **Enter** 鍵。  
  
5.  以滑鼠右鍵按一下 [WorkOrdersProc]，然後按一下 [編輯]。  
  
6.  在 [連接到 Database Engine] 對話方塊中，驗證連接資訊，然後按一下 [連接]。  
  
7.  在 [查詢編輯器] 中，輸入下列指令碼來建立查閱特定零件的訂單之預存程序，這裡的零件是刀片 (Blade)。 (您可以從 [教學課程] 視窗中複製和貼上程式碼)。  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersForBlade')  
       DROP PROCEDURE dbo.WorkOrdersForBlade;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersForBlade  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = 'Blade';  
    GO  
    ```  
  
8.  按 F5 鍵來執行此指令碼，並建立 **WorkOrdersForBlade** 程序。  
  
9. 在物件總管中，以滑鼠右鍵按一下您的伺服器，然後按一下 [新增查詢]。 此時會開啟一個新的 [查詢編輯器] 視窗。  
  
10. 在 [查詢編輯器] 中，輸入 **EXECUTE dbo.WorkOrdersForBlade**，然後按 F5 鍵來執行查詢。 確認 [結果] 窗格會傳回刀鋒視窗的工單清單。  
  
11. 編輯範本指令碼 (步驟 7 中的指令碼)，在四個位置中，利用 ***\<*product_name**, **nvarchar(50)**、**name*>*** 參數來取代產品名稱 Blade。  
  
    > [!NOTE]  
    > 參數具備三個元素：想要取代的參數名稱、參數的資料類型和參數的預設值。  
  
12. 現在，指令碼看起來應該如下：  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersFor<product_name, nvarchar(50), name>')  
       DROP PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = '<product_name, nvarchar(50), name>';  
    GO  
    ```  
  
13. 在 [檔案] 功能表上，按一下 [儲存 WorkOrdersProc.sql] 來儲存您的範本。  
  
#### 若要測試自訂範本  
  
1.  在範本總管中，依序展開 [預存程序] 和 [Custom]，然後按兩下 [WorkOrderProc]。  
  
2.  在 [連接到 Database Engine] 對話方塊中，填妥連接資訊，然後按一下 [連接]。 此時會開啟一個新的 [查詢編輯器] 視窗，其中含有 [WorkOrderProc] 範本的內容。  
  
3.  在 **[查詢]** 功能表上，按一下 **[指定範本參數的值]**。  
  
4.  在 [取代範本參數] 對話方塊中，對於 [product_name] 值輸入 **FreeWheel** (覆寫預設內容)，然後按一下 [確定] 關閉 [取代範本參數] 對話方塊，並修改 [查詢編輯器] 中的指令碼。  
  
5.  按 F5 鍵來執行這項查詢，建立程序。  
  
## 本課程的下一項工作  
[將指令碼儲存成專案或方案](../../tools/sql-server-management-studio/save-scripts-as-projects-or-solutions.md)  
  
  
  
