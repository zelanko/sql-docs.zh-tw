---
title: 存取清查結構描述 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- columns table
- databases table
- exported metadata
- exporting, schemas of exported metadata
- foreign keys table
- forms table
- indexes, table
- inventory schemas
- macros table
- modules table
- queries table
- reference, inventory schemas
- reports table
- schemas of exported metadata
- schemas, exported metadata
- SSMA_Access_InventoryColumns
- SSMA_Access_InventoryDatabases
- SSMA_Access_InventoryForeignKeys
- SSMA_Access_InventoryForms
- SSMA_Access_InventoryIndexes
- SSMA_Access_InventoryMacros
- SSMA_Access_InventoryModules
- SSMA_Access_InventoryQueries
- SSMA_Access_InventoryReports
- SSMA_Access_InventoryTables
- tables, inventory
ms.assetid: fdd3cff2-4d62-4395-8acf-71ea8f17f524
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c140489877be5f34bc6d7a5b20a4ce36fdb3820f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068949"
---
# <a name="access-inventory-schemas-accesstosql"></a>Access 清查結構描述 (AccessToSQL)
下列各節描述資料表所建立的 SSMA 中，當您匯出要存取結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="databases"></a>資料庫  
資料庫中繼資料匯出至**SSMA_Access_InventoryDatabases**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|可唯一識別每個資料庫的 GUID。 此資料行也是資料表的主索引鍵。|  
|**DatabaseName**|**nvarchar(4000)**|存取資料庫的名稱。|  
|**ExportTime**|**datetime**|日期和時間的 SSMA 建立此中繼資料。|  
|**FilePath**|**nvarchar(4000)**|存取資料庫的完整路徑和檔案名稱。|  
|**FileSize**|**bigint**|存取資料庫，以 kb 為單位的大小。|  
|**FileOwner**|**nvarchar(4000)**|Windows 帳戶指定為存取資料庫的擁有者。|  
|**DateCreated**|**datetime**|日期和時間所建立的 Access 資料庫中。|  
|**DateModified**|**datetime**|日期時間與上次修改的 Access 資料庫。|  
|**TablesCount**|**int**|Access 資料庫中的資料表數目。|  
|**QueriesCount**|**int**|Access 資料庫中的查詢數目。|  
|**FormsCount**|**int**|Access 資料庫中的表單數量。|  
|**ModulesCount**|**int**|Access 資料庫中的模組數目。|  
|**ReportsCount**|**int**|Access 資料庫中的報表數目。|  
|**MacrosCount**|**int**|Access 資料庫中的巨集數目。|  
|**AccessVersion**|**nvarchar(4000)**|存取資料庫的版本。|  
|**定序**|**nvarchar(4000)**|存取資料庫的定序。 定序可決定資料庫如何排序和比較字串。|  
|**JetVersion**|**nvarchar(4000)**|Jet 資料庫引擎版本。 Access 資料庫會使用基礎的 Jet 資料庫引擎。|  
|**IsUpdatable**|**bit**|指出資料庫是否可以更新。 如果值為 1，資料庫是可更新。 如果值為 0，資料庫是唯讀的。|  
|**QueryTimeout**|**int**|設定的 ODBC 查詢逾時值對於資料庫，以秒為單位。 預設值是 60 秒。|  
  
## <a name="tables"></a>資料表  
資料表中繼資料匯出至**SSMA_Access_InventoryTables**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此資料表的資料庫。|  
|**TableId**|**uniqueidentifier**|唯一識別資料表的 GUID。 此資料行也是資料表的主索引鍵。|  
|**TableName**|**nvarchar(4000)**|資料表的名稱。|  
|**RowsCount**|**int**|資料表中的資料列數。|  
|**ValidationRule**|**nvarchar(4000)**|定義有效的輸入資料表的規則。 如果不有任何驗證規則，該欄位將包含空字串。|  
|**LinkedTable**|**nvarchar(4000)**|另一個資料表，如果有的話，連結的資料表。 連結資料表可允許新增、 刪除及更新至另一個資料表使用此資料表。|  
|**ExternalSource**|**nvarchar(4000)**|資料來源，如果有的話，是與資料表相關聯。 如果連結資料表，它會有此欄位中指定的外部資料來源。|  
  
## <a name="columns"></a>[資料行]  
資料行中繼資料匯出至**SSMA_Access_InventoryColumns**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此資料行的資料庫。|  
|**TableId**|**uniqueidentifier**|識別包含此資料行的資料表。|  
|**ColumnId**|**int**|識別資料行的遞增整數。 **ColumnId**資料表的主索引鍵。|  
|**ColumnName**|**nvarchar(4000)**|資料行的名稱。|  
|**IsNullable**|**bit**|指定是否資料行可以包含 null 值。 如果值為 1，資料行可以包含 null 值。 如果值為 0，資料行不能包含 null 值。 請注意，驗證規則也可用來避免 null 值。|  
|**DataType**|**nvarchar(4000)**|存取資料類型的資料行，例如**文字**或是**長**。|  
|**IsAutoIncrement**|**bit**|指定是否資料行就會自動遞增的整數值。 如果值為 1，會自動遞增的整數。|  
|**Ordinal**|**smallint**|在資料表中，從零開始的資料行的順序。|  
|**DefaultValue**|**nvarchar(4000)**|資料行的預設值。|  
|**ValidationRule**|**nvarchar(4000)**|在資料行中更新或加入的規則，用來驗證資料。|  
  
## <a name="indexes"></a>索引  
索引中繼資料匯出至**SSMA_Access_InventoryIndexes**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此索引的資料庫。|  
|**TableId**|**uniqueidentifier**|識別包含此索引的資料表。|  
|**IndexId**|**int**|識別索引的遞增整數。 此資料行是資料表的主索引鍵。|  
|**IndexName**|**nvarchar(4000)**|索引的名稱。|  
|**ColumnsIncluded**|**nvarchar(4000)**|列出包含在索引資料行。 資料行名稱被以分號隔開。|  
|**IsUnique**|**bit**|指定是否在索引中的每個項目必須是唯一的。 多重資料行索引，值的組合必須是唯一的。 如果值為 1，則索引會強制執行唯一值。|  
|**IsPK**|**bit**|指定是否已自動建立索引定義的主索引鍵的一部分。|  
|**IsClustered**|**bit**|指定索引是否已叢集化。 叢集的索引重新排列資料的實體儲存體。 資料表可以有一個叢集的索引。|  
  
## <a name="foreign-keys"></a>外部索引鍵  
外部索引鍵的中繼資料匯出至**SSMA_Access_InventoryForeignKeys**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含這個外部索引鍵的資料庫。|  
|**TableId**|**uniqueidentifier**|識別包含這個外部索引鍵的資料表。|  
|**ForeignKeyId**|**int**|識別外部索引鍵的遞增整數。 此資料行是資料表的主索引鍵。|  
|**ForeignKeyName**|**nvarchar(4000)**|索引的名稱。|  
|**ReferencedTableId**|**uniqueidentifier**|識別包含來源資料行的資料表。|  
|**SourceColumns**|**nvarchar(4000)**|列出的外部索引鍵資料行或資料行。|  
|**ReferencedColumns**|**nvarchar(4000)**|列出的主要索引鍵資料行或外部索引鍵所參考的資料行。|  
|**IsCascadeForUpdate**|**bit**|指定，是否更新主索引鍵值，則參考該索引鍵值的所有資料列也會更新。|  
|**IsCascadeForDelete**|**bit**|指定是否刪除主索引鍵值，則參考該索引鍵值的所有資料列會一併刪除。|  
|**IsEnforced**|**bit**|指定外部索引鍵條件約束會強制執行。|  
  
## <a name="queries"></a>查詢  
查詢中繼資料匯出至**SSMA_Access_InventoryQueries**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此查詢的資料庫。|  
|**QueryId**|**int**|遞增整數，識別查詢。 此資料行是資料表的主索引鍵。|  
|**QueryName**|**nvarchar(4000)**|查詢的名稱。|  
|**QueryText**|**nvarchar(4000)**|SQL 查詢程式碼，例如 SELECT 陳述式。|  
|**IsUpdateable**|**bit**|指定查詢是否可更新或唯讀狀態。|  
|**QueryType**|**nvarchar(4000)**|指定查詢的類型，例如**選取** 或是 **SetOperation**。|  
|**ExternalSource**|**nvarchar(4000)**|如果查詢所參考的外部資料來源，這是查詢所用的連接字串。|  
  
## <a name="forms"></a>表單  
表單的中繼資料匯出至**SSMA_Access_InventoryForms**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此表單的資料庫。|  
|**FormId**|**int**|遞增整數，識別的表單。 此資料行是資料表的主索引鍵。|  
|**FormName**|**nvarchar(4000)**|表格的名稱。|  
  
## <a name="macros"></a>巨集  
巨集的中繼資料匯出至**SSMA_Access_InventoryMacros**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含巨集的資料庫。|  
|**MacroId**|**int**|遞增整數，識別巨集。 此資料行是資料表的主索引鍵。|  
|**MacroName**|**nvarchar(4000)**|巨集的名稱。|  
  
## <a name="reports"></a>報表  
報表中繼資料匯出至**SSMA_Access_InventoryReports**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含報表的資料庫。|  
|**ReportId**|**int**|識別報表的遞增整數。 此資料行是資料表的主索引鍵。|  
|**ReportName**|**nvarchar(4000)**|報表的名稱。|  
  
## <a name="modules"></a>模組  
模組中繼資料匯出至**SSMA_Access_InventoryModules**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此模組的資料庫。|  
|**ModuleId**|**int**|遞增整數，可識別的模組。 此資料行是資料表的主索引鍵。|  
|**ModuleName**|**nvarchar(4000)**|模組的名稱。|  
  
## <a name="see-also"></a>另請參閱  
[匯出 Access 清查](exporting-an-access-inventory-accesstosql.md)  
  
