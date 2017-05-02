---
title: "重新命名資料行 (Database Engine) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [SQL Server], names
- renaming columns
- column names [SQL Server]
ms.assetid: 7c71ec9f-0180-4398-b32a-4bfb7592e75d
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e02a5d26a0a04d5afa1c4ddfcc9c06c503b6bd2c
ms.lasthandoff: 04/11/2017

---
# <a name="rename-columns-database-engine"></a>重新命名資料行 (Database Engine)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中重新命名資料表資料行。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來重新命名資料行：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 重新命名資料行不會自動重新命名該資料行的參考。 您必須手動修改任何參考重新命名之資料行的物件。 例如，如果您重新命名資料表資料行，且有觸發程序參考這個資料行，您必須修改觸發程序來反映新的資料行名稱。 在重新命名物件之前，請利用 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 來列出其相依性。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要物件的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-a-column-using-object-explorer"></a>若要使用物件總管來重新命名資料行  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在物件總管****中，以滑鼠右鍵按一下您想要重新命名資料行的資料表，然後選擇 [重新命名]****。  
  
3.  輸入新的資料行名稱。  
  
#### <a name="to-rename-a-column-using-table-designer"></a>若要使用資料表設計工具來重新命名資料行  
  
1.  在物件總管****中，以滑鼠右鍵按一下您想要重新命名資料行的資料表，然後選擇 [設計]****。  
  
2.  在 **[資料行名稱]**下，選取您要變更的名稱，並輸入新名稱。  
  
3.  在 [檔案] **** 功能表上，按一下 [儲存] *****table name*。  
  
> [!NOTE]  
>  您也可以在 **[資料行屬性]** 索引標籤中變更資料行的名稱。 請選取您要變更名稱的資料行，並輸入新的 **[名稱]**值。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要重新命名資料行**  
  
#### <a name="to-rename-a-column"></a>若要重新命名資料行  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  下列範例會將 `TerritoryID` 資料表中的 `Sales.SalesTerritory` 資料行重新命名為 `TerrID`。 將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)。  
  
  
