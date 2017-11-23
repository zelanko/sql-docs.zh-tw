---
title: "存取清查結構描述 (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: "17"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b399910612848033ea927aa8c4d3adc86d048ae0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="access-inventory-schemas-accesstosql"></a>存取清查結構描述 (AccessToSQL)
下列章節將說明當您匯出要存取結構描述時所建立的 SSMA 資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
## <a name="databases"></a>資料庫  
資料庫中繼資料匯出至**SSMA_Access_InventoryDatabases**資料表。 此表格包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|可唯一識別每個資料庫的 GUID。 此資料行也是資料表的主索引鍵。|  
|**DatabaseName**|**nvarchar(4000)**|存取資料庫的名稱。|  
|**ExportTime**|**datetime**|日期和時間的 SSMA 建立此中繼資料。|  
|**檔案路徑**|**nvarchar(4000)**|存取資料庫的完整路徑和檔案名稱。|  
|**檔案大小**|**bigint**|存取資料庫，以 kb 為單位的大小。|  
|**FileOwner**|**nvarchar(4000)**|指定存取資料庫的擁有者為 Windows 帳戶。|  
|**DateCreated**|**datetime**|日期和時間所建立的 Access 資料庫中。|  
|**DateModified**|**datetime**|日期和時間，上次修改的 Access 資料庫中。|  
|**TablesCount**|**int**|Access 資料庫中的資料表數目。|  
|**QueriesCount**|**int**|Access 資料庫中的查詢數目。|  
|**FormsCount**|**int**|Access 資料庫中的表單數量。|  
|**ModulesCount**|**int**|Access 資料庫中的模組數目。|  
|**ReportsCount**|**int**|Access 資料庫中的報表數目。|  
|**MacrosCount**|**int**|Access 資料庫中的巨集數目。|  
|**AccessVersion**|**nvarchar(4000)**|存取資料庫的版本。|  
|**定序**|**nvarchar(4000)**|存取資料庫的定序。 定序可決定資料庫來排序和比較字串的方式。|  
|**JetVersion**|**nvarchar(4000)**|Jet 資料庫引擎版本。 Access 資料庫會使用基礎的 Jet 資料庫引擎。|  
|**IsUpdatable**|**bit**|表示是否可以更新資料庫。 如果值為 1，資料庫是可更新。 如果值為 0，資料庫處於唯讀狀態。|  
|**QueryTimeout**|**int**|設定的 ODBC 查詢逾時值的資料庫，以秒為單位。 預設值是 60 秒。|  
  
## <a name="tables"></a>資料表  
資料表中繼資料匯出至**SSMA_Access_InventoryTables**資料表。 此表格包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此資料表的資料庫。|  
|**TableId**|**uniqueidentifier**|唯一識別資料表的 GUID。 此資料行也是資料表的主索引鍵。|  
|**TableName**|**nvarchar(4000)**|資料表的名稱。|  
|**RowsCount**|**int**|資料表中的資料列數。|  
|**驗證規則**|**nvarchar(4000)**|定義資料表的有效輸入規則。 如果不有任何驗證規則，此欄位會包含空字串。|  
|**LinkedTable**|**nvarchar(4000)**|另一個資料表，如果有的話，與資料表相連結。 連結資料表可允許新增、 刪除及更新的其他資料表使用此資料表。|  
|**ExternalSource**|**nvarchar(4000)**|資料來源，如果有的話，會與資料表相關聯。 如果資料表有關聯，它會有此欄位中指定外部資料來源。|  
  
## <a name="columns"></a>資料行  
資料行中繼資料匯出至**SSMA_Access_InventoryColumns**資料表。 此表格包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此資料行的資料庫。|  
|**TableId**|**uniqueidentifier**|識別包含此資料行的資料表。|  
|**ColumnId**|**int**|識別資料行的遞增整數。 **ColumnId**資料表的主索引鍵。|  
|**ColumnName**|**nvarchar(4000)**|資料行的名稱。|  
|**IsNullable**|**bit**|指定是否資料行可以包含 null 值。 如果值為 1，資料行可以包含 null 值。 如果值為 0，資料行不能包含 null 值。 請注意，驗證規則也可用來避免 null 值。|  
|**DataType**|**nvarchar(4000)**|存取資料類型的資料行，例如**文字**或**長**。|  
|**IsAutoIncrement**|**bit**|指定是否資料行就會自動遞增的整數值。 如果值為 1，會自動遞增的整數。|  
|**Ordinal**|**smallint**|在資料表中，從零開始的資料行的順序。|  
|**預設值**|**nvarchar(4000)**|資料行的預設值。|  
|**驗證規則**|**nvarchar(4000)**|用來驗證資料的規則新增至或更新資料行中。|  
  
## <a name="indexes"></a>索引  
索引中繼資料匯出至**SSMA_Access_InventoryIndexes**資料表。 此表格包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此索引的資料庫。|  
|**TableId**|**uniqueidentifier**|識別包含此索引的資料表。|  
|**IndexId**|**int**|識別索引的遞增整數。 此資料行是資料表的主索引鍵。|  
|**IndexName**|**nvarchar(4000)**|索引的名稱。|  
|**ColumnsIncluded**|**nvarchar(4000)**|列出包含在索引資料行。 資料行名稱被以分號隔開。|  
|**IsUnique**|**bit**|指定是否在索引中的每個項目必須是唯一的。 多重資料行索引，值的組合必須是唯一的。 如果值為 1，則索引會強制執行唯一值。|  
|**IsPK**|**bit**|指定是否自動建立索引做為定義的主索引鍵的一部分。|  
|**IsClustered**|**bit**|指定索引是否已叢集化。 叢集的索引，重新排列資料的實體儲存體。 資料表可以有一個叢集的索引。|  
  
## <a name="foreign-keys"></a>外部索引鍵  
外部索引鍵的中繼資料匯出至**SSMA_Access_InventoryForeignKeys**資料表。 此表格包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此外部索引鍵的資料庫。|  
|**TableId**|**uniqueidentifier**|識別包含此外部索引鍵的資料表。|  
|**ForeignKeyId**|**int**|識別外部索引鍵的遞增整數。 此資料行是資料表的主索引鍵。|  
|**ForeignKeyName**|**nvarchar(4000)**|索引的名稱。|  
|**ReferencedTableId**|**uniqueidentifier**|識別包含來源資料行的資料表。|  
|**SourceColumns**|**nvarchar(4000)**|列出外部索引鍵資料行或資料行。|  
|**ReferencedColumns**|**nvarchar(4000)**|列出主索引鍵資料行或外部索引鍵所參考的資料行。|  
|**IsCascadeForUpdate**|**bit**|指定，是否更新主索引鍵值時，參考該索引鍵值的所有資料列也會更新。|  
|**IsCascadeForDelete**|**bit**|指定是否刪除主索引鍵值，參考該索引鍵值的所有資料列會一併刪除。|  
|**IsEnforced**|**bit**|指定的外部索引鍵條件約束會強制執行。|  
  
## <a name="queries"></a>查詢  
查詢中繼資料匯出至**SSMA_Access_InventoryQueries**資料表。 此表格包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此查詢的資料庫。|  
|**QueryId**|**int**|識別查詢的遞增整數。 此資料行是資料表的主索引鍵。|  
|**QueryName**|**nvarchar(4000)**|查詢的名稱。|  
|**QueryText**|**nvarchar(4000)**|SQL 查詢程式碼，例如 SELECT 陳述式。|  
|**IsUpdateable**|**bit**|指定是否可更新或唯讀查詢。|  
|**QueryType**|**nvarchar(4000)**|指定類型的查詢，例如**選取**或**SetOperation**。|  
|**ExternalSource**|**nvarchar(4000)**|如果查詢參考的外部資料來源，這是查詢所用的連接字串。|  
  
## <a name="forms"></a>表單  
表單的中繼資料匯出至**SSMA_Access_InventoryForms**資料表。 此表格包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此表單的資料庫。|  
|**FormId**|**int**|識別表單的遞增整數。 此資料行是資料表的主索引鍵。|  
|**FormName**|**nvarchar(4000)**|表格的名稱。|  
  
## <a name="macros"></a>巨集  
巨集的中繼資料匯出至**SSMA_Access_InventoryMacros**資料表。 此表格包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含巨集的資料庫。|  
|**MacroId**|**int**|識別巨集的遞增整數。 此資料行是資料表的主索引鍵。|  
|**巨集名稱**|**nvarchar(4000)**|巨集名稱。|  
  
## <a name="reports"></a>報表  
報表中繼資料匯出至**SSMA_Access_InventoryReports**資料表。 此表格包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含報表的資料庫。|  
|**ReportId**|**int**|識別報表的遞增整數。 此資料行是資料表的主索引鍵。|  
|**ReportName**|**nvarchar(4000)**|報表的名稱。|  
  
## <a name="modules"></a>模組  
模組中繼資料匯出至**SSMA_Access_InventoryModules**資料表。 此表格包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含模組的資料庫。|  
|**ModuleId**|**int**|遞增整數可識別模組。 此資料行是資料表的主索引鍵。|  
|**模組名稱**|**nvarchar(4000)**|模組的名稱。|  
  
## <a name="see-also"></a>請參閱＜  
[匯出 Access 清查](http://msdn.microsoft.com/en-us/7e1941fb-3d14-4265-aff6-c77a4026d0ed)  
  
