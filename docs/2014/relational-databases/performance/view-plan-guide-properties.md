---
title: 檢視計畫指南屬性 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.planguideprop.general.f1
helpviewer_keywords:
- plan guides [SQL Server], view plan guide properties
- viewing plan guide properties
ms.assetid: 8c0d2f39-59c1-4168-a649-65473f6a771b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b49b24db5dfa3c9b522247024e0cbb8dbd1a81d2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63151268"
---
# <a name="view-plan-guide-properties"></a>檢視計畫指南屬性
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **使用下列方法來檢視計畫指南的屬性：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>檢視計畫指南的屬性  
  
1.  按一下加號，展開您要在其中檢視計畫指南屬性的資料庫，然後按一下加號展開 **[可程式性]** 資料夾。  
  
2.  按一下加號展開 **[計畫指南]** 資料夾。  
  
3.  以滑鼠右鍵按一下要檢視其屬性的計劃指南，然後選取 [屬性]  。  
  
     下列屬性會在 **[計畫指南屬性]** 對話方塊中顯示。  
  
     **提示**  
     顯示套用到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的查詢提示或查詢計畫。 當指定了某個查詢計畫做為提示時，會顯示該計畫的 XML 執行程序表輸出。  
  
     **為已停用**  
     顯示計畫指南的狀態。 可能的值為 **True** 和 **False**。  
  
     **名稱**  
     顯示計畫指南的名稱。  
  
     **參數**  
     當範圍類型為 SQL 或 TEMPLATE 時，顯示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中內嵌的所有參數的名稱與資料類型。  
  
     **範圍批次**  
     顯示在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中出現的批次文字。  
  
     **範圍物件名稱**  
     當範圍類型為 OBJECT 時，則顯示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序、使用者定義純量函數、多重陳述式資料表值函式或其中出現 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式之 DML 觸發程序的名稱。  
  
     **範圍結構描述名稱**  
     當範圍類型為 OBJECT 時，顯示包含了該物件的結構描述名稱。  
  
     **範圍類型**  
     顯示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳列式中出現的實體類型。 這會指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式要與計畫指南比對相符的內容。 可能的值是 **OBJECT**、 **SQL**，以及 **TEMPLATE**。  
  
     **陳述式**  
     顯示對照套用計畫指南的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
4.  按一下 [確定]  。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>檢視計畫指南的屬性  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- If a plan guide named "Guide1" already exists in the AdventureWorks2012 database, delete it.  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID(N'Guide1') IS NOT NULL  
       EXEC sp_control_plan_guide N'DROP', N'Guide1';  
    GO  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
    GO  
    -- Gets the name, created date, and all other relevant property information on the plan guide created above.   
    SELECT name AS plan_guide_name,  
       create_date,  
       query_text,  
       scope_type_desc,  
       OBJECT_NAME(scope_object_id) AS scope_object_name,  
       scope_batch,  
       parameters,  
       hints,  
       is_disabled  
    FROM sys.plan_guides  
    WHERE name = N'Guide1';  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sys.plan_guides &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-plan-guides-transact-sql)。  
  
  
