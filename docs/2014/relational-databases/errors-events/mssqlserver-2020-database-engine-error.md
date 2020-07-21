---
title: MSSQLSERVER_2020 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2020 (Database Engine error)
ms.assetid: 4a8bf90f-a083-4c53-84f0-d23c711c8081
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9190ada39fbc2bae6805a0d4d2c2c611847869e3
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552193"
---
# <a name="mssqlserver_2020"></a>MSSQLSERVER_2020
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2020|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|針對實體 "%.*ls" 所報告的相依性不包含資料行的參考。 這是因為此實體參考了不存在的物件，或是此實體中的一個或多個陳述式發生錯誤。  在重新執行查詢以前，請確定此實體中沒有任何錯誤，而且此實體參考的所有物件都存在。|  
  
## <a name="explanation"></a>說明  
 **sys.dm_sql_referenced_entities** 系統函數會回報任何資料行層級相依性，以進行結構描述繫結參考。 例如，此函數將會報告索引檢視表的所有資料行層級相依性，因為索引檢視表需要結構描述繫結。 不過，如果受參考實體並未結構描述繫結，只有當參考資料行的所有陳述式都可以繫結時，才會報告資料行相依性。 只有當剖析陳述式時所有物件都存在時，陳述式才能成功繫結。 如果實體中定義的任何陳述式無法繫結，即不會回報資料行相依性，而且 **referenced_minor_id** 資料行會傳回 0。 無法解析資料行相依性時，就會引發錯誤 2020。 這個錯誤不會讓查詢無法傳回物件層級相依性。  
  
## <a name="user-action"></a>使用者動作  
 更正發生錯誤 2020 之前，在訊息中識別的任何錯誤。 例如，在下列程式碼範例中，`Production.ApprovedDocuments` 檢視表定義於 `Title` 資料表中的 `ChangeNumber`、`Status` 和 `Production.Document` 資料行上。 系統會針對 `ApprovedDocuments` 檢視表所相依的物件和資料行查詢 **sys.dm_sql_referenced_entities** 系統函數。 因為此檢視表並非使用 WITH SCHEMA_BINDING 子句建立，所以檢視表中參考的資料行可能會在參考的資料表中修改。 此範例會將 `ChangeNumber` 資料表中的 `Production.Document` 資料行重新命名為 `TrackingNumber`，藉以更改此資料行。 系統會再次針對 `ApprovedDocuments` 檢視表查詢目錄檢視。不過，它無法繫結至檢視表中定義的所有資料行。 然後，系統會傳回識別此問題的錯誤 207 和 2020。 若要解決此問題，您必須更改檢視表，以便反映資料行的新名稱。  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `CREATE VIEW Production.ApprovedDocuments`  
  
 `AS`  
  
 `SELECT Title, ChangeNumber, Status`  
  
 `FROM Production.Document`  
  
 `WHERE Status = 2;`  
  
 `GO`  
  
 `SELECT referenced_schema_name AS schema_name`  
  
 `,referenced_entity_name AS table_name`  
  
 `,referenced_minor_name AS referenced_column`  
  
 `FROM sys.dm_sql_referenced_entities ('Production.ApprovedDocuments', 'OBJECT');`  
  
 `GO`  
  
 `EXEC sp_rename 'Production.Document.ChangeNumber', 'TrackingNumber', 'COLUMN';`  
  
 `GO`  
  
 `SELECT referenced_schema_name AS schema_name`  
  
 `,referenced_entity_name AS table_name`  
  
 `,referenced_minor_name AS referenced_column`  
  
 `FROM sys.dm_sql_referenced_entities ('Production.ApprovedDocuments', 'OBJECT');`  
  
 `GO`  
  
 此查詢會傳回下列錯誤訊息。  
  
 `Msg 207, Level 16, State 1, Procedure ApprovedDocuments, Line 3`  
  
 `Invalid column name 'ChangeNumber'.`  
  
 `Msg 2020, Level 16, State 1, Line 1`  
  
 `The dependencies reported for entity`  
  
 `"Production.ApprovedDocuments" do not include references to`  
  
 `columns. This is either because the entity references an`  
  
 `object that does not exist or because of an error in one or`  
  
 `more statements in the entity. Before rerunning the query,`  
  
 `ensure that there are no errors in the entity and that all`  
  
 `objects referenced by the entity exist.`  
  
 下列範例會更正檢視表中的資料行名稱。  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `ALTER VIEW Production.ApprovedDocuments`  
  
 `AS`  
  
 `SELECT Title,TrackingNumber, Status`  
  
 `FROM Production.Document`  
  
 `WHERE Status = 2;`  
  
 `GO`  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
  
