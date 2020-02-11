---
title: 存取清查架構（AccessToSQL） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068949"
---
# <a name="access-inventory-schemas-accesstosql"></a>存取清查架構（AccessToSQL）
下列各節說明當您將存取架構匯出至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，SSMA 所建立的資料表。  
  
## <a name="databases"></a>資料庫  
資料庫中繼資料會匯出至**SSMA_Access_InventoryDatabases**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|唯一識別每個資料庫的 GUID。 此資料行也是資料表的主要索引鍵。|  
|**DatabaseName**|**nvarchar(4000)**|Access 資料庫的名稱。|  
|**ExportTime**|**datetime**|SSMA 建立此中繼資料的日期和時間。|  
|**FilePath**|**nvarchar(4000)**|Access 資料庫的完整路徑和檔案名。|  
|**FileSize**|**Bigint**|Access 資料庫的大小（以 KB 為單位）。|  
|**FileOwner**|**nvarchar(4000)**|指定為 Access 資料庫擁有者的 Windows 帳戶。|  
|**DateCreated**|**datetime**|建立 Access 資料庫的日期和時間。|  
|**DateModified**|**datetime**|上次修改 Access 資料庫的日期和時間。|  
|**TablesCount**|**int**|Access 資料庫中的資料表數目。|  
|**QueriesCount**|**int**|Access 資料庫中的查詢數目。|  
|**FormsCount**|**int**|Access 資料庫中的表單數目。|  
|**ModulesCount**|**int**|Access 資料庫中的模組數目。|  
|**ReportsCount**|**int**|Access 資料庫中的報表數目。|  
|**MacrosCount**|**int**|Access 資料庫中的宏數目。|  
|**AccessVersion**|**nvarchar(4000)**|資料庫的存取版本。|  
|**定序**|**nvarchar(4000)**|Access 資料庫的定序。 定序會決定資料庫排序和比較字串的方式。|  
|**JetVersion**|**nvarchar(4000)**|Jet 資料庫引擎版本。 Access 資料庫會使用基礎 Jet 資料庫引擎。|  
|**IsUpdatable**|**bit**|指出是否可更新資料庫。 如果值為1，則資料庫是可更新的。 如果值為0，則資料庫是唯讀的。|  
|**QueryTimeout**|**int**|資料庫的已設定 ODBC 查詢超時值（以秒為單位）。 預設值是 60 秒。|  
  
## <a name="tables"></a>資料表  
資料表中繼資料會匯出至**SSMA_Access_InventoryTables**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此資料表的資料庫。|  
|**TableId**|**uniqueidentifier**|可唯一識別資料表的 GUID。 此資料行也是資料表的主要索引鍵。|  
|**TableName**|**nvarchar(4000)**|資料表的名稱。|  
|**RowsCount**|**int**|資料表中的資料列數。|  
|**有效性**|**nvarchar(4000)**|定義資料表有效輸入的規則。 如果沒有驗證規則存在，此欄位將會包含空字串。|  
|**LinkedTable**|**nvarchar(4000)**|與資料表連結的另一個資料表（如果有的話）。 連結資料表可讓您使用此資料表來新增、刪除和更新其他資料表。|  
|**ExternalSource**|**nvarchar(4000)**|與資料表相關聯的資料來源（如果有的話）。 如果資料表已連結，它會在此欄位中指定外部資料源。|  
  
## <a name="columns"></a>資料行  
資料行中繼資料會匯出至**SSMA_Access_InventoryColumns**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此資料行的資料庫。|  
|**TableId**|**uniqueidentifier**|識別包含此資料行的資料表。|  
|**ColumnId**|**int**|用來識別資料行的遞增整數。 **ColumnId**是資料表的主要索引鍵。|  
|**ColumnName**|**nvarchar(4000)**|資料行的名稱。|  
|**IsNullable**|**bit**|指定資料行是否可以包含 null 值。 如果值為1，則資料行可以包含 null 值。 如果值為0，則資料行不能包含 null 值。 請注意，驗證規則也可以用來防止 null 值。|  
|**DataType**|**nvarchar(4000)**|資料行的存取資料類型，例如**Text**或**Long**。|  
|**IsAutoIncrement**|**bit**|指定資料行是否自動遞增整數值。 如果值為1，則整數會自動遞增。|  
|**Ordinal**|**smallint**|資料表中的資料行順序，從零開始。|  
|**DefaultValue**|**nvarchar(4000)**|資料行的預設值。|  
|**有效性**|**nvarchar(4000)**|用來驗證資料行中加入或更新之資料的規則。|  
  
## <a name="indexes"></a>索引  
索引中繼資料會匯出至**SSMA_Access_InventoryIndexes**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此索引的資料庫。|  
|**TableId**|**uniqueidentifier**|識別包含此索引的資料表。|  
|**IndexId**|**int**|用來識別索引的遞增整數。 此資料行是資料表的主要索引鍵。|  
|**IndexName**|**nvarchar(4000)**|索引的名稱。|  
|**ColumnsIncluded**|**nvarchar(4000)**|列出索引中包含的資料行。 資料行名稱是以分號分隔。|  
|**IsUnique**|**bit**|指定索引中的每個專案是否都必須是唯一的。 在多重資料行索引上，值的組合必須是唯一的。 如果值為1，則索引會強制執行唯一的值。|  
|**IsPK**|**bit**|指定索引是否自動建立為定義主鍵的一部分。|  
|**IsClustered**|**bit**|指定索引是否已叢集化。 叢集索引會重新排序資料的實體儲存體。 一個資料表只能有一個叢集索引。|  
  
## <a name="foreign-keys"></a>外鍵  
外鍵中繼資料會匯出至**SSMA_Access_InventoryForeignKeys**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此外鍵的資料庫。|  
|**TableId**|**uniqueidentifier**|識別包含此外鍵的資料表。|  
|**ForeignKeyId**|**int**|識別外鍵的遞增整數。 此資料行是資料表的主要索引鍵。|  
|**ForeignKeyName**|**nvarchar(4000)**|索引的名稱。|  
|**ReferencedTableId**|**uniqueidentifier**|識別包含來源資料行的資料表。|  
|**SourceColumns**|**nvarchar(4000)**|列出外鍵資料行或資料行。|  
|**ReferencedColumns**|**nvarchar(4000)**|列出外鍵所參考的主要索引鍵資料行。|  
|**IsCascadeForUpdate**|**bit**|指定如果更新主鍵值，則也會更新參考該索引鍵值的所有資料列。|  
|**IsCascadeForDelete**|**bit**|指定如果刪除主要索引鍵值，則也會一併刪除參考該索引鍵值的所有資料列。|  
|**IsEnforced**|**bit**|指定強制執行 foreign key 條件約束。|  
  
## <a name="queries"></a>查詢  
查詢中繼資料會匯出至**SSMA_Access_InventoryQueries**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此查詢的資料庫。|  
|**QueryId**|**int**|識別查詢的遞增整數。 此資料行是資料表的主要索引鍵。|  
|**QueryName**|**nvarchar(4000)**|查詢的名稱。|  
|**QueryText**|**nvarchar(4000)**|SQL 查詢程式碼，例如 SELECT 語句。|  
|**IsUpdateable**|**bit**|指定查詢是可更新或唯讀。|  
|**QueryType**|**nvarchar(4000)**|指定查詢的類型，例如**Select**或**SetOperation**。|  
|**ExternalSource**|**nvarchar(4000)**|如果查詢參考外部資料源，這就是查詢所使用的連接字串。|  
  
## <a name="forms"></a>表單  
表單中繼資料會匯出至**SSMA_Access_InventoryForms**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含此表單的資料庫。|  
|**FormId**|**int**|用來識別表單的遞增整數。 此資料行是資料表的主要索引鍵。|  
|**FormName**|**nvarchar(4000)**|表格的名稱。|  
  
## <a name="macros"></a>巨集  
宏中繼資料會匯出至**SSMA_Access_InventoryMacros**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含宏的資料庫。|  
|**MacroId**|**int**|識別宏的遞增整數。 此資料行是資料表的主要索引鍵。|  
|**MacroName**|**nvarchar(4000)**|宏的名稱。|  
  
## <a name="reports"></a>報表  
報表中繼資料會匯出至**SSMA_Access_InventoryReports**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含報表的資料庫。|  
|**ReportId**|**int**|識別報表的遞增整數。 此資料行是資料表的主要索引鍵。|  
|**ReportName**|**nvarchar(4000)**|報表的名稱。|  
  
## <a name="modules"></a>模組  
模組中繼資料會匯出至**SSMA_Access_InventoryModules**資料表。 此資料表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|識別包含模組的資料庫。|  
|**ModuleId**|**int**|識別模組的遞增整數。 此資料行是資料表的主要索引鍵。|  
|**ModuleName**|**nvarchar(4000)**|模組的名稱。|  
  
## <a name="see-also"></a>另請參閱  
[匯出 Access 清查](exporting-an-access-inventory-accesstosql.md)  
  
