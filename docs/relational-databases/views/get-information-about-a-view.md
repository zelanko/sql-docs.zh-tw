---
title: 取得檢視的資訊 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.viewproperties.general.f1
helpviewer_keywords:
- views [SQL Server], status information
- metadata [SQL Server], views
- dependencies [SQL Server], views
- displaying view information
- views [SQL Server], metadata
- viewing view information
- status information [SQL Server], views
- view dependencies
ms.assetid: 05a73e33-8f85-4fb6-80c1-1b659e753403
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f5e660301620a98e7ea6b93b4242da1a0d852ce9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "72909886"
---
# <a name="get-information-about-a-view"></a>取得檢視的資訊
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]
  您可以透過使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，取得 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中檢視定義或屬性的相關資訊。 您可能需要查看檢視的定義才能了解如何從來源資料表衍生出資料；或是查看檢視所定義的資料。  
  
> [!IMPORTANT]  
>  如果變更檢視所參考的物件名稱，就必須修改檢視，使其文字反映新的名稱。 因此，在重新命名物件前，應先顯示物件的相依性，以判斷是否有任何檢視會受預期的變更所影響。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **使用下列方法取得檢視的相關資訊：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 使用 `sp_helptext` 傳回檢視的定義，需要 **Public** 角色的成員資格。 使用 `sys.sql_expression_dependencies` 尋找檢視的所有相依性，需要資料庫的 VIEW DEFINITION 權限和資料庫之 `sys.sql_expression_dependencies` 的 SELECT 權限。 系統物件定義是公開可見的，就像 SELECT OBJECT_DEFINITION 中傳回的定義一樣。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="get-view-properties-by-using-object-explorer"></a>透過使用物件總管取得檢視屬性  
  
1.  在 **[物件總管]** 中，按一下資料庫旁邊的加號，此資料庫包含您要查看其屬性的檢視，然後按一下加號展開 **[檢視]** 資料夾。  
  
2.  以滑鼠右鍵按一下要查看其屬性的檢視，然後選取 **[屬性]** 。  

     下列屬性會在 **[檢視屬性]** 對話方塊中顯示。  
  
     **Database**  
     包含此檢視之資料庫的名稱。  
  
     **Server**  
     目前伺服器執行個體的名稱。  
  
     **使用者**  
     這個連接之使用者的名稱。  
  
     **建立日期**  
     顯示建立檢視的日期。  
  
     **名稱**  
     目前檢視的名稱。  
  
     **結構描述**  
     顯示擁有檢視的結構描述。  
  
     **系統物件**  
     指出檢視是否為系統物件。 值為 True 與 False。  
  
     **ANSI NULLS**  
     指出物件是否使用 ANSI NULLS 選項建立。  
  
     **已加密**  
     指出檢視表是否已加密。 值為 True 與 False。  
  
     **引號識別碼**  
     指出物件是否使用引號識別碼選項建立。  
  
     **結構描述繫結**  
     指出檢視是否以結構描述繫結。 值為 True 與 False。 如需結構描述繫結檢視的相關資訊，請參閱 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md) 的 SCHEMABINDING 部分。  
  
#### <a name="getting-view-properties-by-using-the-view-designer-tool"></a>透過使用檢視設計工具取得檢視屬性  
  
1.  在 **[物件總管]** 中，展開資料庫，此資料庫包含您要查看其屬性的檢視，然後展開 **[檢視]** 資料夾。  
  
2.  以滑鼠右鍵按一下要查看其屬性的檢視，然後選取 **[設計]** 。  
  
3.  在 [圖表] 窗格的空白處按一下滑鼠右鍵，再按 [ **屬性**]。  
  
     下列屬性會在 **[屬性]** 窗格中顯示。  
  
     **(名稱)**  
     目前檢視的名稱。  
  
     **Database Name**  
     包含此檢視之資料庫的名稱。  
  
     **說明**  
     目前檢視的簡要描述。  
  
     **結構描述**  
     顯示擁有檢視的結構描述。  
  
     **伺服器名稱**  
     目前伺服器執行個體的名稱。  
  
     **繫結至結構描述**  
     防止使用者以任何可能會導致檢視定義失效的方式修改促成此檢視的基礎物件。  
  
     **具決定性**  
     顯示是否可以確定地決定選取之資料行的資料類型。  
  
     **重複資料僅顯示一筆**  
     指定查詢會篩選檢視中重複的資料。 如果只使用資料表中的一部分資料行，而這些資料行包含了重複的值；或者聯結兩個以上資料表的處理序，會在結果集中產生重複的資料列時，這個選項非常實用。 選擇此選項相當於在 [SQL] 窗格中的陳述式裡插入 DISTINCT 關鍵字。  
  
     **GROUP BY 擴充選項**  
     指定彙總查詢為基礎的檢視有其他可用的選項。  
  
     **輸出全部資料行**  
     顯示選定的檢視是否傳回所有資料行。 這是在建立檢視時設定的。  
  
     **SQL 註解**  
     顯示 SQL 陳述式的描述。 若要查看或編輯整個描述，請按一下 [描述]，然後按一下屬性右側的省略符號 **(...)** 。 您的註解中可能包含使用檢視的人及使用時間等這類資訊。  
  
     **Top 規格**  
     展開以顯示 **[Top]** 、 **[運算式]** 、 **[百分比]** 屬性，以及 **[WITH TIES]** 屬性。  
  
     **(Top)**  
     指定檢視將包含 TOP 子句，而這個子句只會傳回結果集內的前 n 個資料列，或前百分之 n 的資料列。 預設值是檢視會傳回結果集裡前 10 個資料列。 使用此選項變更傳回的資料列數目，或指定不同的百分比。  
  
     **運算式**  
     顯示檢視會傳回多少百分比 (如果 **[百分比]** 設定為 **[是]** ) 或何種記錄 (如果 **[百分比]** 設定為 **[否]** )。  
  
     **Percent**  
     指定查詢將包含 **TOP** 子句，只會傳回結果集內的前百分之 n 的資料列。  
  
     **With Ties**  
     指定檢視中會包含 **WITH TIES** 子句。 如果檢視中包含了**WITH TIES** 子句和以百分比為基礎的 **WITH TIES** 子句， **WITH TIES** 非常實用。 如果設定了此選項，而且百分比截止點落在 **ORDER BY** 子句裡一組相同值的資料列中間，將會擴充檢視以將這些資料列全部包含。  
  
     **更新規格**  
     展開以顯示 **[使用檢視規則更新]** 屬性和 **[檢查選項]** 屬性。  
  
     **(使用檢視規則更新)**  
     指示檢視的所有更新和插入都會由 Microsoft Data Access Components (MDAC) 轉譯為參考檢視的 SQL 陳述式，而不是轉譯為直接參考檢視之基底資料表的 SQL 陳述式。  
  
     在某些情況下，MDAC 會表示檢視更新和檢視插入作業是針對檢視之基礎基底資料表的更新和插入。 透過選取 **[使用檢視規則更新]** ，可以確保 MDAC 會針對檢視本身產生更新和插入作業。  
  
     **檢查選項**  
     指示當您開啟此檢視並修改 **[結果]** 窗格時，資料來源會檢查加入或修改的資料是否滿足檢視定義的 **WHERE** 子句。 如果您的修改無法滿足 **WHERE** 子句，您將看到錯誤附帶詳細資訊。  
  
#### <a name="to-get-dependencies-on-the-view"></a>取得檢視的相依性  
  
1.  在 **[物件總管]** 中，展開資料庫，此資料庫包含您要查看其屬性的檢視，然後展開 **[檢視]** 資料夾。  
  
2.  以滑鼠右鍵按一下要查看其屬性的檢視，然後選取 **[檢視相依性]** 。  
  
3.  選取 **[相依於 [檢視名稱] 的物件]** ，以顯示參考檢視的物件。  
  
4.  選取 **[[檢視表名稱] 所相依的物件]** ，以顯示檢視表所參考的物件。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-get-the-definition-and-properties-of-a-view"></a>取得檢視定義和屬性  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  將下列其中一個範例複製並貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT definition, uses_ansi_nulls, uses_quoted_identifier, is_schema_bound  
    FROM sys.sql_modules  
    WHERE object_id = OBJECT_ID('HumanResources.vEmployee');   
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID('HumanResources.vEmployee')) AS ObjectDefinition;   
    GO  
    ```  
  
    ```  
    EXEC sp_helptext 'HumanResources.vEmployee';  
    ```  
  
 如需詳細資訊，請參閱 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)、[OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md) 和 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)。  
  
#### <a name="to-get-the-dependencies-of-a-view"></a>取得檢視的相依性  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 和 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。  
  
  
