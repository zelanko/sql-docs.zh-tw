---
title: 修改預存程序 | Microsoft Docs
description: 了解如何使用 SQL Server Management Studio 或 Transact-SQL，在 SQL Server 2019 (15.x) 中修改預存程序。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- modifying stored procedures
- editing stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: 13396239-6100-48ce-aa34-461358d99c92
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f70272f01918af1d7cb91000e0ce15904b1e5518
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332609"
---
# <a name="modify-a-stored-procedure"></a>修改預存程序
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
    
##  <a name="this-topic-describes-how-to-modify-a-stored-procedure-in-sscurrent-by-using-ssmanstudiofull-or-tsql"></a><a name="Top"></a> 本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來修改 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的預存程序。  
  
-   **開始之前：** [限制事項](#Restrictions)、[安全性](#Security)  
  
-   **若要更改程序，請使用：** [SQL Server Management Studio](#SSMSProcedure)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序無法修改成 CLR 預存程序，反之亦然。  
  
 如果先前的程序定義是利用 WITH ENCRYPTION 或 WITH RECOMPILE 來建立的，只有在 ALTER PROCEDURE 陳述式包括這些選項時，才會啟用這些選項。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要程序的 ALTER PROCEDURE 權限。  
  
##  <a name="how-to-modify-a-stored-procedure"></a><a name="Procedures"></a> 如何修改預存程序  
 您可以使用下列其中一項：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要在 Management Studio 中修改程序**  
  
1.  在物件總管中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 **[資料庫]** 、程序所屬的資料庫，以及 **[可程式性]** 。  
  
3.  展開 [預存程序]，以滑鼠右鍵按一下要修改的程序，然後按一下 [修改]。  
  
4.  修改預存程序的文字。  
  
5.  若要測試語法，請在 **[查詢]** 功能表上按一下 **[剖析]** 。  
  
6.  若要將所做的修改儲存至程序定義，請在 **[查詢]** 功能表上按一下 **[執行]** 。  
  
7.  若要將更新的程序定義儲存為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼，請在 **[檔案]** 功能表上按一下 **[另存新檔]** 。 接受檔案名稱，或將它取代成新名稱，然後按一下 **[儲存]** 。  

> [!IMPORTANT]  
>  驗證所有使用者輸入。 在使用者輸入完成驗證前，請勿加以串連。 請勿執行由未經驗證之使用者輸入所建構的命令。  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要在查詢編輯器中修改程序**  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 **[資料庫]** ，展開程序所屬的資料庫。 或者，從工具列的可用資料庫清單中選取資料庫。 針對此範例，請選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
3.  按一下 **[檔案]** 功能表上的 **[新增查詢]** 。  
  
4.  將下列範例複製並貼入查詢編輯器中。 範例會建立 `uspVendorAllInfo` 程序，它會傳回 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 資料庫中的所有供應商名稱，以及他們提供的產品、他們的信用等級，以及是否能聯繫到他們。  
  
    ```  
  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
5.  按一下 **[檔案]** 功能表上的 **[新增查詢]** 。  
  
6.  將下列範例複製並貼入查詢編輯器中。 下列範例會修改 `uspVendorAllInfo` 程序。 它會移除 EXECUTE AS CALLER 子句，並修改程序主體，使其只傳回提供指定之產品的供應商。 `LEFT` 和 `CASE` 函數可自訂結果集的外觀。  
  
    ```  
    ALTER PROCEDURE Purchasing.uspVendorAllInfo  
        @Product varchar(25)   
    AS  
        SET NOCOUNT ON;  
        SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
        'Rating' = CASE v.CreditRating   
            WHEN 1 THEN 'Superior'  
            WHEN 2 THEN 'Excellent'  
            WHEN 3 THEN 'Above average'  
            WHEN 4 THEN 'Average'  
            WHEN 5 THEN 'Below average'  
            ELSE 'No rating'  
            END  
        , Availability = CASE v.ActiveFlag  
            WHEN 1 THEN 'Yes'  
            ELSE 'No'  
            END  
        FROM Purchasing.Vendor AS v   
        INNER JOIN Purchasing.ProductVendor AS pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product AS p   
          ON pv.ProductID = p.ProductID   
        WHERE p.Name LIKE @Product  
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
7.  若要將所做的修改儲存至程序定義，請在 **[查詢]** 功能表上按一下 **[執行]** 。  
  
8.  若要將更新的程序定義儲存為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼，請在 **[檔案]** 功能表上按一下 **[另存新檔]** 。 接受檔案名稱，或將它取代成新名稱，然後按一下 **[儲存]** 。  
  
9. 若要執行修改過的預存程序，請執行下列範例。  
  
    ```  
    EXEC Purchasing.uspVendorAllInfo N'LL Crankarm';  
    GO  
  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
  
