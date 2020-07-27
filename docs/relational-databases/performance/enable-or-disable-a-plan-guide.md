---
title: 啟用或停用計畫指南 | Microsoft Docs
description: 了解如何使用 SQL Server Management Studio 或 Transact-SQL 來停用和啟用計畫指南。 停用或啟用資料庫中的一個或所有計畫指南。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], disabling
- enabling plan guides
- plan guides [SQL Server], enabling
- disabling plan guides
ms.assetid: b00ab550-5308-4cb8-8330-483cd1d25654
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 04180f951747b7517775ec7c222f679d043286c3
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457270"
---
# <a name="enable-or-disable-a-plan-guide"></a>啟用或停用計畫指南
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中停用和啟用計畫指南。 您可以啟用或停用資料庫中的單一計畫指南或所有計畫指南。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來停用和啟用計畫指南：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   試圖卸除或修改計畫指南所參考的函數、預存程序或 DML 觸發程序，不論是已啟用或已停用，都會造成錯誤。 請務必在卸除或修改上述任何物件之前，檢查是否存在相依性。  
  
-   停用已停用的計畫指南，或啟用已啟用的計畫指南，都沒有作用，執行時也不會發生錯誤。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 停用或啟用 OBJECT 計畫指南需要計畫指南所參考之物件 (例如：函數、預存程序) 的 ALTER 權限。 所有其他計畫指南都需要 ALTER DATABASE 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>若要停用或啟用計畫指南  
  
1.  按一下加號，展開您要在其中停用或啟用計畫指南的資料庫，然後按一下加號展開 **[可程式性]** 資料夾。  
  
2.  按一下加號展開 **[計畫指南]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想要停用或啟用的計畫指南，然後選取 [停用] 或 [啟用]。  
  
4.  在 **[停用計畫指南]** 或 **[啟用計畫指南]** 對話方塊中，確認選擇的動作已成功，然後按一下 **[關閉]** 。  

#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>若要停用或啟用資料庫中的所有計畫指南  
  
1.  按一下加號，展開您要在其中停用或啟用計畫指南的資料庫，然後按一下加號展開 **[可程式性]** 資料夾。  
  
2.  以滑鼠右鍵按一下 [計畫指南] 資料夾，然後選取 [全部啟用] 或 [全部停用]。  
  
3.  在 **[停用所有計畫指南]** 或 **[啟用所有計畫指南]** 對話方塊中，確認選擇的動作已成功，然後按一下 **[關閉]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>若要停用或啟用計畫指南  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    --Create a procedure on which to define the plan guide.  
    IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetSalesOrderByCountry;  
    GO  
    CREATE PROCEDURE Sales.GetSalesOrderByCountry   
        (@Country nvarchar(60))  
    AS  
    BEGIN  
        SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country;  
    END  
    GO  
    --Create the plan guide.  
    EXEC sp_create_plan_guide N'Guide3',  
        N'SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country',  
        N'OBJECT',  
        N'Sales.GetSalesOrderByCountry',  
        NULL,  
        N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
    --Disable the plan guide.  
    EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
    GO  
    --Enable the plan guide.  
    EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
    GO  
  
    ```  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>若要停用或啟用資料庫中的所有計畫指南  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    --Disable all plan guides in the database.  
    EXEC sp_control_plan_guide N'DISABLE ALL';  
    GO  
    --Enable all plan guides in the database.  
    EXEC sp_control_plan_guide N'ENABLE ALL';  
    GO  
  
    ```  
  
 如需詳細資訊，請參閱 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)。  
  
  
