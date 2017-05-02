---
title: "建立 DML 觸發程序 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption [SQL Server], DML triggers
- deferred name resolution, DML triggers
- WITH ENCRYPTION clause
- IF UPDATE
- SET statement, DML triggers
- DML triggers, programming
- testing column changes
- results [SQL Server], DML triggers
ms.assetid: b2b52258-642b-462e-8e0f-18c09d2eccf4
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 21011d77337e517154b4732071253a934984363d
ms.lasthandoff: 04/11/2017

---
# <a name="create-dml-triggers"></a>建立 DML 觸發程序
  此主題描述如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 以及使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] CREATE TRIGGER 陳述式來建立 [!INCLUDE[tsql](../../includes/tsql-md.md)] DML 觸發程序。  
  
##  <a name="Top"></a> 開始之前  
  
### <a name="limitations-and-restrictions"></a>限制事項  
 如需與建立 DML 觸發程序相關之限制事項的清單，請參閱 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)。  
  
###  <a name="Permissions"></a> Permissions  
 需要建立觸發程序之資料表或檢視的 ALTER 權限。  
  
##  <a name="Procedures"></a> 如何建立 DML 觸發程序  
 您可以使用下列其中一項：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 [資料庫]、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫、[資料表] 和 **Purchasing.PurchaseOrderHeader** 資料表。  
  
3.  以滑鼠右鍵按一下 [觸發程序]，然後選取 [新增觸發程序]。  
  
4.  在 **[查詢]** 功能表上，按一下 **[指定範本參數的值]**。 您也可以按 (Ctrl-Shift-M) 開啟 [指定範本參數的值] 對話方塊。  
  
5.  在 **[指定範本參數的值]** 對話方塊中，為顯示的參數輸入下列值。  
  
    |參數|值|  
    |---------------|-----------|  
    |作者|*您的名字*|  
    |建立日期|*今天的日期*|  
    |描述|先檢查供應商信用評等，再允許插入含有該供應商的新採購單。|  
    |Schema_Name|Purchasing|  
    |Trigger_Name|NewPODetail2|  
    |Table_Name|PurchaseOrderDetail|  
    |Data_Modification_Statement|從清單中移除 UPDATE 和 DELETE。|  
  
6.  按一下 **[確定]**。  
  
7.  在 [查詢編輯器] 中，將 `-- Insert statements for trigger here` 註解取代為下列陳述式：  
  
    ```tsql  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
8.  若要驗證語法是否有效，請在 [查詢] 功能表上按一下 [剖析]。 如果傳回錯誤訊息，請比較陳述式與上列資訊，並視需要進行更正，然後重複此步驟。  
  
9. 若要建立 DML 觸發程序，請在 [查詢] 功能表中按一下 [執行]。 DML 觸發程序會建立為資料庫中的物件。  
  
10. 若要查看物件總管中所列的 DML 觸發程序，請以滑鼠右鍵按一下 [觸發程序]，然後選取 [重新整理]。  
  
 [開始之前](#Top)  
  
###  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  在 **[檔案]** 功能表中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例會建立與上面相同的預存 DML 觸發程序。  
  
    ```  
    -- Trigger valid for multirow and single row inserts  
    -- and optimal for single row inserts.  
    USE AdventureWorks2012;  
    GO  
    CREATE TRIGGER NewPODetail3  
    ON Purchasing.PurchaseOrderDetail  
    FOR INSERT AS  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
##  <a name="PowerShellProcedure"></a> [開始之前](#Top)  
  
  
