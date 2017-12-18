---
title: "檢視使用者定義函數 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: udf
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.udfproperties.general.f1
- sql13.swb.functionproperties.general.f1
helpviewer_keywords:
- displaying user-defined functions
- viewing user-defined functions
- user-defined functions [SQL Server], viewing
- status information [SQL Server], user-defined functions
ms.assetid: a45dfab5-6384-4311-b935-2e23a70c5c10
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6a71d45d8d304c52592b8ee693525950c3bfed28
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="view-user-defined-functions"></a>檢視使用者定義函數
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)] 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，取得 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中使用者定義函數之定義或屬性的相關資訊。 您可能需要查看函數的定義才能了解如何從來源資料表衍生出資料；或是查看函數所定義的資料。  
  
> [!IMPORTANT]  
>  如果變更函數所參考的物件名稱，就必須修改該函數，使其文字反映新的名稱。 因此，在改變物件名稱時，首先要檢視此物件的相依性以了解是否有相關的函數受到影響。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **使用下列方法取得函數的相關資訊：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 若要使用 **sys.sql_expression_dependencies** 尋找函數的所有相依性，需要資料庫的 VIEW DEFINITION 權限以及資料庫之 **sys.sql_expression_dependencies** 的 SELECT 權限。 系統物件定義是公開可見的，就像 OBJECT_DEFINITION 中傳回的定義一樣。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-show-a-user-defined-functions-properties"></a>若要顯示使用者定義函數的屬性  
  
1.  在 **[物件總管]**中，按一下資料庫旁邊的加號，此資料庫包含您要查看其屬性的函數，然後按一下加號展開 **[可程式性]** 資料夾。  
  
2.  按一下加號展開 **[函數]** 資料夾。  
  
3.  按一下加號展開包含您要檢視其屬性之函數的資料夾：  
  
    -   資料表值函式  
  
    -   純量值函式  
  
    -   彙總函式  
  
4.  以滑鼠右鍵按一下要查看其屬性的函數，然後選取 [屬性]。  
  
     下列屬性會出現在 [函數屬性 - *函數名稱*] 對話方塊中。  
  
     **資料庫**  
     包含此函數之資料庫的名稱。  
  
     **Server**  
     目前伺服器執行個體的名稱。  
  
     **使用者**  
     這個連接之使用者的名稱。  
  
     **建立日期**  
     顯示建立函數的日期。  
  
     **執行身分**  
     函數的執行內容。  
  
     **名稱**  
     目前函數的名稱。  
  
     **結構描述**  
     顯示擁有函數的結構描述。  
  
     **系統物件**  
     指出函數是否為系統物件。 值為 True 與 False。  
  
     **ANSI NULLS**  
     指出物件是否使用 ANSI NULLS 選項建立。  
  
     **已加密**  
     指出函數是否加密。 值為 True 與 False。  
  
     **函數類型**  
     使用者定義函數的類型。  
  
     **引號識別碼**  
     指出物件是否使用引號識別碼選項建立。  
  
     **結構描述繫結**  
     指出函數是否為結構描述繫結函數。 值為 True 與 False。 如需結構描述繫結函數的資訊，請參閱 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md) 的＜SCHEMABINDING＞一節。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-get-the-definition-and-properties-of-a-function"></a>若要取得函數定義和屬性  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列其中一個範例複製並貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the function name, definition, and relevant properties  
    SELECT sm.object_id,   
       OBJECT_NAME(sm.object_id) AS object_name,   
       o.type,   
       o.type_desc,   
       sm.definition,  
       sm.uses_ansi_nulls,  
       sm.uses_quoted_identifier,  
       sm.is_schema_bound,  
       sm.execute_as_principal_id  
    -- using the two system tables sys.sql_modules and sys.objects  
    FROM sys.sql_modules AS sm  
    JOIN sys.objects AS o ON sm.object_id = o.object_id  
    -- from the function 'dbo.ufnGetProductDealerPrice'  
    WHERE sm.object_id = OBJECT_ID('dbo.ufnGetProductDealerPrice')  
    ORDER BY o.type;  
    GO  
  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the definition of the function dbo.ufnGetProductDealerPrice  
    SELECT OBJECT_DEFINITION (OBJECT_ID('dbo.ufnGetProductDealerPrice')) AS ObjectDefinition;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 和 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)。  
  
#### <a name="to-get-the-dependencies-of-a-function"></a>若要取得函數的相依性  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get all of the dependency information  
    SELECT OBJECT_NAME(sed.referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(sed.referencing_id, sed.referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        sed.referencing_class_desc, sed.referenced_class_desc,  
        sed.referenced_server_name, sed.referenced_database_name, sed.referenced_schema_name,  
        sed.referenced_entity_name,   
        COALESCE(COL_NAME(sed.referenced_id, sed.referenced_minor_id), '(n/a)') AS referenced_column_name,  
        sed.is_caller_dependent, sed.is_ambiguous  
    -- from the two system tables sys.sql_expression_dependencies and sys.object  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    -- on the function dbo.ufnGetProductDealerPrice  
    WHERE sed.referencing_id = OBJECT_ID('dbo.ufnGetProductDealerPrice');  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 和 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。  
  
  
