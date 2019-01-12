---
title: 建立檢視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], creating
ms.assetid: 0b7bd2a1-544c-42ba-8e7b-4822f34d7b64
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 27748ee6f4c70ebbcb4d1d28738130ddea07232b
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134398"
---
# <a name="create-views"></a>建立檢視表
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立檢視。 檢視可用於下列目的：  
  
-   對焦 (Focus)、簡化和自訂每位使用者查看資料庫的角度。  
  
-   做為安全機制，讓使用者能夠透過檢視存取資料，但不將直接存取基底資料表的權限授與使用者。  
  
-   提供回溯相容介面以模擬其結構描述已變更的資料表。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **使用下列方法建立檢視：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 檢視只能建立在目前資料庫中。  
  
 檢視最多可有 1,024 個資料行。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 至少必須有資料庫中的 CREATE VIEW 權限，以及正在建立之檢視表所在之結構描述的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-view-by-using-the-query-and-view-designer"></a>透過使用查詢和檢視表設計工具建立檢視  
  
1.  在 **[物件總管]** 中，展開您要建立新檢視表的資料庫。  
  
2.  以滑鼠右鍵按一下 [檢視] 資料夾，然後按一下 [新增檢視…]。  
  
3.  在 **加入資料表**對話方塊方塊中，選取項目或您想要包含在新的檢視，從下列索引標籤中的項目：資料表、 檢視、 函數和同義字。  
  
4.  按一下 **[加入]**，然後按一下 **[關閉]**。  
  
5.  在 **[圖表]** 窗格中，選取要包含在新檢視中的資料行或其他元素。  
  
6.  在 **[準則]** 窗格中，選擇資料行的其他排序或篩選準則。  
  
7.  在 [檔案]  功能表上，按一下 [儲存] _view name_。  
  
8.  在 **[選擇名稱]** 對話方塊中，輸入新檢視的名稱，並按一下 **[確定]**。  
  
     如需查詢和檢視表設計工具的詳細資訊，請參閱[查詢和檢視表設計工具 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-view"></a>建立檢視  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 [執行] 。  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    CREATE VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID ;   
    GO  
    -- Query the view  
    SELECT FirstName, LastName, HireDate  
    FROM HumanResources.EmployeeHireDate  
    ORDER BY LastName;  
  
    ```  
  
 如需詳細資訊，請參閱 [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)。  
  
  
