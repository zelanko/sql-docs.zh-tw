---
title: "建立巢狀觸發程序 | Microsoft Docs"
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
- recursive DML triggers [SQL Server]
- DML triggers, nested
- triggers [SQL Server], nested
- direct recursion [SQL Server]
- triggers [SQL Server], recursive
- DML triggers, recursive
- RECURSIVE_TRIGGERS option
- indirect recursion [SQL Server]
- nested DML triggers
ms.assetid: cd522dda-b4ab-41b8-82b0-02445bdba7af
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ed1505ace274659400d797ae5ba8b27dcdf80557
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="create-nested-triggers"></a>建立巢狀觸發程序
  觸發程序執行用來起始另一個觸發程序的動作時，DML 和 DDL 觸發程序就是巢狀觸發程序。 這些動作可以起始化其他觸發程序等等。 DML 與 DDL 觸發程序最多可以巢狀方式嵌套多達 32 層。 您可以透過 [巢狀觸發程序] 伺服器組態選項來控制 AFTER 觸發程序是否可為巢狀。 不論此設定為何，INSTEAD OF 觸發程序 (只有 DML 觸發程序可為 INSTEAD OF 觸發程序) 均可為巢狀。  
  
> [!NOTE]  
>  任何從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 觸發程序對 Managed 程式碼的參考，都會算成 32 層巢狀限制中的一層。 從 Managed 程式碼內叫用的方法，不列入這項限制。  
  
 如果允許巢狀觸發程序，但鏈結中的觸發程序形成一個無限迴圈時，則觸發程序會因為超過巢狀層級而終止執行。  
  
 您可利用巢狀觸發程序來執行實用的內部管理功能，如儲存被前一個觸發程序所影響的資料列備份。 例如，您可在 `PurchaseOrderDetail` 上建立觸發程序，其可儲存經 `PurchaseOrderDetail` 觸發程序所刪除的 `delcascadetrig` 資料列備份。 由於 `delcascadetrig` 觸發程序為作用中，刪除 `PurchaseOrderID` 的 `PurchaseOrderHeader` 1965，也會刪除 `PurchaseOrderDetail`對應的一或多個資料列。 若要儲存資料，您可在 `PurchaseOrderDetail` 上建立 DELETE 觸發程序，將刪除的資料儲存至另外建立的資料表 `del_save`。 例如：  
  
```  
CREATE TRIGGER Purchasing.savedel  
   ON Purchasing.PurchaseOrderDetail  
FOR DELETE  
AS  
   INSERT del_save;  
   SELECT * FROM deleted;  
```  
  
 我們不建議您在與順序有關的序列中使用巢狀觸發程序。 請使用個別的觸發程序來串聯修改的資料。  
  
> [!NOTE]  
>  因觸發程序是在交易內執行，所以在整組巢狀觸發程序中，只要有一層在執行時發生錯誤，即會取消整個交易，所有的修改資料均會回復原狀。 您可在觸發程序中加入 PRINT 陳述式，這樣便可知道錯誤發生在那一層級。  
  
## <a name="recursive-triggers"></a>遞迴觸發程序  
 除非設定 RECURSIVE_TRIGGERS 資料庫選項，否則 AFTER 觸發程序不會以遞迴方式自我呼叫。  
  
 而遞迴有以下兩種不同類型：  
  
-   直接遞迴  
  
     當觸發程序引發和執行使相同觸發程序再度引發的動作時，就會發生遞迴。 例如，應用程式會更新資料表 **T3**；這將使觸發程序 **Trig3** 引發。 **Trig3** 會再次更新 **T3** ；這將使觸發程序 **Trig3** 再度引發。  
  
     在呼叫不同類型的觸發程序 (AFTER 或 INSTEAD OF) 之後，再次呼叫相同的觸發程序時，也會發生直接遞迴。 換句話說，即使在第一次與第二次呼叫之間呼叫了一個或多個 AFTER 觸發程序，第二次呼叫相同 INSTEAD OF 觸發程序時，仍會發生 INSTEAD OF 觸發程序的直接遞迴。 同樣地，即使在第一次與第二次呼叫之間呼叫了一或多個 INSTEAD OF 觸發程序，第二次呼叫相同 AFTER 觸發程序時，仍會發生 AFTER 觸發程序的直接遞迴。 例如，應用程式會更新資料表 **T4**。 這項更新會引發 INSTEAD OF 觸發程序 **Trig4** 。 **Trig4** 會更新資料表 **T5**。 這項更新會引發 AFTER 觸發程序 **Trig5** 。 **Trig5** 會更新資料表 **T4**，而這項更新會再次引發 INSTEAD OF 觸發程序 **Trig4** 。 這個事件鏈結被視為 **Trig4**的直接遞迴。  
  
-   間接遞迴  
  
     觸發程序引發並執行會引發另一個相同類型之觸發程序 (AFTER 或 INSTEAD OF) 的動作時，會發生這類遞迴。 此第二個觸發程序執行使原始觸發程序再次引發的動作。 換句話說，如果第二次呼叫 INSTEAD OF 觸發程序，則會在第一次與第二次呼叫之間呼叫另一個 INSTEAD OF 觸發程序時，發生間接遞迴。 同樣地，如果第二次呼叫 AFTER 觸發程序，則會在第一次與第二次呼叫之間呼叫另一個 AFTER 觸發程序時，發生間接遞迴。 例如，應用程式會更新資料表 **T1**。 這項更新會引發 AFTER 觸發程序 **Trig1** 。 **Trig1** 會更新資料表 **T2**，而這項更新會引發 AFTER 觸發程序 **Trig2** 。 接著，**Trig2** 會更新資料表 **T1** ，而這會再次引發 AFTER 觸發程序 **Trig1** 。  
  
 RECURSIVE_TRIGGERS 資料庫選項設定為 OFF 時，只能防止 AFTER 觸發程序的直接遞迴。 若要停用 AFTER 觸發程序的間接遞迴，也請將 **巢狀觸發程序** 伺服器選項設定為 **0**。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何使用遞迴觸發程序來解決自我參考關聯 (又名為遞移封閉)。 例如， `emp_mgr` 資料表定義下列項目：  
  
-   公司中的員工 (`emp`)。  
  
-   每名員工的經理 (`mgr`)。  
  
-   在對每位員工報告的組織樹中員工的總數 (`NoOfReports`)。  
  
 當有新員工記錄插入時，遞迴 UPDATE 觸發程序可使 `NoOfReports` 資料行同時保持最新的資料。 INSERT 觸發程序則可在更新經理記錄的 `NoOfReports` 資料行時，遞迴更新在經理階層架構之上其他記錄的 `NoOfReports` 資料行。  
  
```  
USE AdventureWorks2012;  
GO  
-- Turn recursive triggers ON in the database.  
ALTER DATABASE AdventureWorks2012  
   SET RECURSIVE_TRIGGERS ON;  
GO  
CREATE TABLE dbo.emp_mgr (  
   emp char(30) PRIMARY KEY,  
    mgr char(30) NULL FOREIGN KEY REFERENCES emp_mgr(emp),  
    NoOfReports int DEFAULT 0  
);  
GO  
CREATE TRIGGER dbo.emp_mgrins ON dbo.emp_mgr  
FOR INSERT  
AS  
DECLARE @e char(30), @m char(30);  
DECLARE c1 CURSOR FOR  
   SELECT emp_mgr.emp  
   FROM   emp_mgr, inserted  
   WHERE emp_mgr.emp = inserted.mgr;  
  
OPEN c1;  
FETCH NEXT FROM c1 INTO @e;  
WHILE @@fetch_status = 0  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Add 1 for newly  
   WHERE emp_mgr.emp = @e ;                           -- added employee.  
  
   FETCH NEXT FROM c1 INTO @e;  
END  
CLOSE c1;  
DEALLOCATE c1;  
GO  
-- This recursive UPDATE trigger works assuming:  
--   1. Only singleton updates on emp_mgr.  
--   2. No inserts in the middle of the org tree.  
CREATE TRIGGER dbo.emp_mgrupd ON dbo.emp_mgr FOR UPDATE  
AS  
IF UPDATE (mgr)  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Increment mgr's  
   FROM inserted                            -- (no. of reports) by  
   WHERE emp_mgr.emp = inserted.mgr;         -- 1 for the new report.  
  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports - 1 -- Decrement mgr's  
   FROM deleted                             -- (no. of reports) by 1  
   WHERE emp_mgr.emp = deleted.mgr;          -- for the new report.  
END  
GO  
-- Insert some test data rows.  
INSERT dbo.emp_mgr(emp, mgr) VALUES  
    ('Harry', NULL)  
    ,('Alice', 'Harry')  
    ,('Paul', 'Alice')  
    ,('Joe', 'Alice')  
    ,('Dave', 'Joe');  
GO  
SELECT emp,mgr,NoOfReports  
FROM dbo.emp_mgr;  
GO  
-- Change Dave's manager from Joe to Harry  
UPDATE dbo.emp_mgr SET mgr = 'Harry'  
WHERE emp = 'Dave';  
GO  
SELECT emp,mgr,NoOfReports FROM emp_mgr;  
  
GO  
```  
  
 更新前的結果如下。  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Joe                            0  
Harry                          NULL                           1  
Joe                            Alice                          1  
Paul                           Alice                          0  
```  
  
 更新後的結果如下。  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Harry                          0  
Harry                          NULL                           2  
Joe                            Alice                          0  
Paul                           Alice                          0  
```  
  
 **若要設定巢狀觸發程序選項**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 **若要設定 RECURSIVE_TRIGGERS 資料庫選項**  
  
-   [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [設定 nested triggers 伺服器組態選項](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)  
  
  
