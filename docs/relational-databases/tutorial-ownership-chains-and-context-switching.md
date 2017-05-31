---
title: "教學課程：擁有權鏈結和內容切換 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- context switching [SQL Server], tutorials
- ownership chains [SQL Server]
ms.assetid: db5d4cc3-5fc5-4cf5-afc1-8d4edc1d512b
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 858ca3c26c6d5297de86e5b0710a3b464ed4ce18
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="tutorial-ownership-chains-and-context-switching"></a>Tutorial: Ownership Chains and Context Switching
這個教學課程利用案例來說明涉及擁有權鏈結和使用者內容切換的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安全性概念。  
  
> [!NOTE]  
> 若要執行本教學課程中的程式碼，您必須設定使用混合模式安全性，並已安裝 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫。 如需混合模式安全性的詳細資訊，請參閱 [選擇驗證模式](../relational-databases/security/choose-an-authentication-mode.md)。  
  
## <a name="scenario"></a>狀況  
在此狀況中，有兩位使用者需要使用其帳戶來存取 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫內儲存的採購訂單資料。 需求如下：  
  
-   第一個帳戶 (TestManagerUser) 必須能夠看見每筆訂單的所有詳細資料。  
  
-   第二個帳戶 (TestEmployeeUser) 必須能夠看見訂單號碼、訂貨日期、送貨日期、產品識別碼，以及已部分送達的每筆訂單所採購和收到的貨品數量。  
  
-   其餘所有帳戶必須保有各自現行的權限。  
  
為了滿足此案例的需求，範例將拆成四部分示範擁有權鏈結和內容切換的概念：  
  
1.  設定環境。  
  
2.  建立預存程序用於存取訂單資料。  
  
3.  透過預存程序存取資料。  
  
4.  重設環境。  
  
此範例會在每個程式碼區塊中各行附上說明。 若要複製整個範例，請參閱本教學課程結尾處的＜ [完整範例](#CompleteExample) ＞一節。  
  
## <a name="1-configure-the-environment"></a>1.設定環境  
使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 與下列程式碼開啟 `AdventureWorks2012` 資料庫，然後使用 `CURRENT_USER` [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式檢查 dbo 使用者是否顯示為內容。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
```  
  
如需 CURRENT_USER 陳述式的詳細資訊，請參閱 [CURRENT_USER &#40;Transact-SQL&#41;](../t-sql/functions/current-user-transact-sql.md)。  
  
使用下列程式碼，以 dbo 使用者身分在伺服器和 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫中建立兩位使用者。  
  
```  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
GO  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
```  
  
如需 CREATE USER 陳述式的詳細資訊，請參閱 [CREATE USER &#40;Transact-SQL&#41;](../t-sql/statements/create-user-transact-sql.md)。 如需 CREATE LOGIN 陳述式的詳細資訊，請參閱 [CREATE LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/create-login-transact-sql.md)。  
  
使用下列陳述式，將 `Purchasing` 結構描述的擁有權變更為 `TestManagerUser` 帳戶。 這樣一來，該帳戶對結構描述內含物件就具備了所有的資料操作語言 (DML) 陳述式存取權 (例如 `SELECT` 和 `INSERT` 權限)。 `TestManagerUser` 也已獲授與建立預存程序的能力。  
  
```  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
```  
  
如需 GRANT 陳述式的詳細資訊，請參閱 [GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md)。 如需預存程序的詳細資訊，請參閱[預存程序 &#40;Database Engine&#41;](../relational-databases/stored-procedures/stored-procedures-database-engine.md)。 如需所有 [!INCLUDE[ssDE](../includes/ssde-md.md)] 權限的海報，請參閱 [http://go.microsoft.com/fwlink/?LinkId=229142](http://go.microsoft.com/fwlink/?LinkId=229142)。  
  
## <a name="2-create-a-stored-procedure-to-access-data"></a>2.建立預存程序來存取資料  
若要在資料庫內切換內容，請使用 EXECUTE AS 陳述式。 EXECUTE AS 則需要 IMPERSONATE 權限。  
  
下列程式碼使用 `EXECUTE AS` 陳述式將內容變更為 `TestManagerUser` ，並建立預存程序單僅顯示 `TestEmployeeUser`所需的資料。 為了滿足需求，預存程序接受訂單號碼做為變數且並未顯示財務資訊，而 WHERE 子句則將結果限制在已部分送達的貨品。  
  
```  
EXECUTE AS LOGIN = 'TestManagerUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader a  
      INNER JOIN Purchasing.PurchaseOrderDetail b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END  
GO  
```  
  
目前 `TestEmployeeUser` 尚無權存取任何資料庫物件。 下列程式碼 (內容仍是 `TestManagerUser` ) 將授與該使用者帳戶透過預存程序查詢基底資料表資訊的能力。  
  
```  
GRANT EXECUTE  
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO  
```  
  
儘管並未明確指定結構描述，此預存程序係屬 `Purchasing` 結構描述的一部分，因為 `TestManagerUser` 預設即指派到 `Purchasing` 結構描述。 您可以利用系統目錄資訊找出物件，如下列程式碼所示。  
  
```  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas a  
   INNER JOIN sys.objects b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
```  
  
範例的這個部分既已完成，程式碼隨即使用 `REVERT` 陳述式將內容切換回 dbo。  
  
```  
REVERT;  
GO  
```  
  
如需 REVERT 陳述式的詳細資訊，請參閱 [REVERT &#40;Transact-SQL&#41;](../t-sql/statements/revert-transact-sql.md)。  
  
## <a name="3-access-data-through-the-stored-procedure"></a>3.透過預存程序存取資料  
`TestEmployeeUser` 除了在 public 資料庫角色中具備登入身分及受指派的權限外，對 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫物件毫無任何權限。 下列程式碼將因 `TestEmployeeUser` 試圖存取基底資料表而傳回錯誤。  
  
```  
EXECUTE AS LOGIN = 'TestEmployeeUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* This won't work */  
SELECT *  
FROM Purchasing.PurchaseOrderHeader;  
GO  
SELECT *  
FROM Purchasing.PurchaseOrderDetail;  
GO  
```  
  
由於 `TestManagerUser` 憑藉其 `Purchasing` 結構描述擁有權而成為上一節所建立預存程序中參考之物件的擁有者， `TestEmployeeUser` 可透過預存程序存取基底資料表。 下列程式碼仍舊使用 `TestEmployeeUser` 內容，傳遞訂單號碼 952 做為參數。  
  
```  
EXEC Purchasing.usp_ShowWaitingItems 952  
GO  
```  
  
## <a name="4-reset-the-environment"></a>4.重設環境  
下列程式碼使用 `REVERT` 命令，將目前帳戶的內容切換回 `dbo`然後重設環境。  
  
```  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="CompleteExample"></a>完整範例  
本節顯示完整的範例程式碼。  
  
> [!NOTE]  
> 下列程式碼剔除了用以示範 `TestEmployeeUser` 無法從基底資料表選取以致發生兩項預期錯誤的部分。  
  
```  
/*   
Script:       UserContextTutorial.sql  
Author:       Microsoft  
Last Updated: Books Online  
Conditions:   Execute as DBO or sysadmin in the AdventureWorks database  
Section 1:    Configure the Environment   
*/  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* Create server and database users */  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
  
GO  
  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
  
/*   
Section 2: Switch Context and Create Objects  
*/  
EXECUTE AS LOGIN = 'TestManagerUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader AS a  
      INNER JOIN Purchasing.PurchaseOrderDetail AS b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END;  
GO  
  
/* Give the employee the ability to run the procedure */  
GRANT EXECUTE   
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO   
  
/* Notice that the stored procedure is located in the Purchasing   
schema. This also demonstrates system catalogs */  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas AS a  
   INNER JOIN sys.objects AS b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
  
/* Go back to being the dbo user */  
REVERT;  
GO  
  
/*  
Section 3: Switch Context and Observe Security   
*/  
EXECUTE AS LOGIN = 'TestEmployeeUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
EXEC Purchasing.usp_ShowWaitingItems 952;  
GO  
  
/*   
Section 4: Clean Up Example  
*/  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
  

