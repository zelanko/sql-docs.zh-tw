---
title: "刪除使用者定義函數 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: udf
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: db1d668a-23b7-4757-a9c5-1bd848ba7f6d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e3db20508f239f3b57d3793a254526ff6eb2b68b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="delete-user-defined-functions"></a>刪除使用者定義函數
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
您可以透過使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或下列項目，刪除 (卸除) [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的使用者定義函數： [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目刪除使用者定義函數：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果資料庫中有 Transact-SQL 函數或檢視參考這個函數，並且是利用 SCHEMABINDING 加以建立；或者如果有計算資料行、CHECK 條件約束或 DEFAULT 條件約束參考這個函數，就無法刪除函數。  
  
-   如果有計算資料行參考這個函數，而且已經產生索引，就無法刪除函數。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要函數所屬結構描述的 ALTER 權限，或函數的 CONTROL 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-user-defined-function"></a>若要刪除使用者定義函數  
  
1.  按一下包含要修改之函數的資料庫旁邊的加號。  
  
2.  按一下 **[可程式性]** 資料夾旁的加號。  
  
3.  按一下包含要修改之函數的資料夾旁邊的加號：  
  
    -   資料表值函式  
  
    -   純量值函式  
  
    -   彙總函式  
  
4.  以滑鼠右鍵按一下您想刪除的函數，然後選取 [刪除]。  
  
5.  在 **[刪除物件]** 對話方塊中，按一下 **[確定]**。  
  
    > [!IMPORTANT]  
    >  在 [刪除物件] 對話方塊中按一下 [顯示相依性]，開啟 *function_name***Dependencies** 對話方塊。 這就會顯示相依於函數的所有物件以及函數所相依的所有物件。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-user-defined-function"></a>若要刪除使用者定義函數  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- creates function called “Sales.ufn_SalesByStore”  
    USE AdventureWorks2012;  
    GO  
    CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
    RETURNS TABLE  
    AS  
    RETURN   
    (  
        SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
        FROM Production.Product AS P   
        JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
        JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
        JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
        WHERE C.StoreID = @storeid  
        GROUP BY P.ProductID, P.Name  
    );  
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- determines if function exists in database  
    IF OBJECT_ID (N'Sales.fn_SalesByStore', N'IF') IS NOT NULL  
    -- deletes function  
        DROP FUNCTION Sales.fn_SalesByStore;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)。  
  
  
