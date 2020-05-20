---
title: SchemaEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SchemaEnum
helpviewer_keywords:
- SchemaEnum enumeration [ADO]
ms.assetid: 21c97651-297f-469f-b5b5-c48af72b62a8
author: rothja
ms.author: jroth
ms.openlocfilehash: cb004c33ae413c93506bc1c90b331494b7e56adc
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765429"
---
# <a name="schemaenum"></a>SchemaEnum
指定[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法所抓取之架構**記錄集**的類型。  
  
## <a name="remarks"></a>備註  
 如需每個 ADO 常數所傳回之函式和資料行的其他資訊，請參閱[附錄 B：](https://msdn.microsoft.com/2b5fbf03-e50d-44ee-bc57-5a57666c55f1) OLE DB 程式設計人員參考的架構資料列集中的主題。 下表的 [描述] 部分中，每個主題的名稱都會列在括弧中。  
  
 如需有關每個 ADO MD 常數所傳回之函數和資料行的詳細資訊，請參閱線上分析處理（OLAP） OLE DB 中[OLAP 物件和架構資料列集 OLE DB](https://msdn.microsoft.com/d20bb2a6-68bd-423f-9ec8-eb930cd0c144)的主題。 下表的 [描述] 資料行中，每個主題的名稱都會列在括弧中。  
  
 您可以參考 ADO [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)主題的 [描述] 欄，將 OLE DB 檔中資料行的資料類型轉譯為 ado 資料類型。 例如， **DBTYPE_WSTR**的 OLE DB 資料類型等同于**adWChar**的 ADO 資料類型。  
  
 ADO 會針對常數（ **adSchemaDBInfoKeywords**和**adSchemaDBInfoLiterals**）產生類似架構的結果。 ADO 會建立**記錄集**，然後使用**IDBInfo：： GetKeywords**和**IDBInfo：： GetLiteralInfo**方法分別傳回的值，填滿每個資料列。 如需這些方法的其他資訊，請參閱 OLE DB 程式設計人員參考的[IDBInfo](https://msdn.microsoft.com/3f5ad97f-3fc6-4f21-b691-f6911e4007f3)一節。  
  
|持續性|值|描述|條件約束資料行|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|傳回指定使用者所擁有的目錄中定義的判斷提示。<br /><br /> （判斷提示資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|傳回與可從 DBMS 存取之目錄相關聯的實體屬性。<br /><br /> （目錄資料列集）|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|傳回在目錄中定義的字元集，可供指定的使用者存取。<br /><br /> （CHARACTER_SETS 資料列集）|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|傳回指定使用者所擁有的目錄中定義的檢查條件約束。<br /><br /> （CHECK_CONSTRAINTS）資料列集|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|傳回在目錄中定義的字元定序，指定的使用者可以存取該定序。<br /><br /> （定序資料列集）|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|傳回在目錄中所定義之資料表資料行的許可權，可供指定的使用者使用或授與。<br /><br /> （COLUMN_PRIVILEGES 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|傳回在目錄中所定義且可供指定使用者存取之資料表的資料行（包括 views）。<br /><br /> （資料行資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|會傳回在資料庫目錄中所定義的資料行，而資料行會相依於資料庫目錄中定義的領域，並且由指定使用者擁有。<br /><br /> （COLUMN_DOMAIN_USAGE 資料列集）|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|會傳回參考條件約束、唯一條件約束、檢查條件約束和判斷提示所使用的資料行 (定義在資料庫目錄中，並且由指定使用者所擁有)。<br /><br /> （CONSTRAINT_COLUMN_USAGE 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|會傳回參考條件約束、唯一條件約束、檢查條件約束和判斷提示所使用的資料行 (定義在資料庫目錄中，並且由指定使用者所擁有)。<br /><br /> （CONSTRAINT_TABLE_USAGE 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|傳回架構中可用 cube 的相關資訊（如果提供者不支援架構，則會傳回目錄）。<br /><br /> （CUBE 資料列集 *）|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|會傳回提供者特定之關鍵字的清單。<br /><br /> （IDBInfo：： GetKeywords）|\<無>|  
|**adSchemaDBInfoLiterals**|31|會傳回文字命令中所使用之提供者特定常值 (Literal) 的清單。<br /><br /> （IDBInfo：： GetLiteralInfo）|\<無>|  
|**adSchemaDimensions**|33|傳回給定 cube 中之維度的相關資訊。 每個維度都有一個資料列。<br /><br /> （維度資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|會傳回由指定使用者在資料庫目錄中定義的外部索引鍵資料行。<br /><br /> （FOREIGN_KEYS 資料列集）|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|傳回維度中可用階層的相關資訊。<br /><br /> （階層資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|傳回由指定使用者所擁有的目錄中定義的索引。<br /><br /> （索引資料列集）|TABLE_CATALOG TABLE_SCHEMA INDEX_NAME 類型 TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|傳回目錄中定義的資料行，其受限於指定使用者的索引鍵。<br /><br /> （KEY_COLUMN_USAGE 資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|傳回維度中可用層級的相關資訊。<br /><br /> （層級資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|傳回可用量值的相關資訊。<br /><br /> （量值資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|傳回可用成員的相關資訊。<br /><br /> （成員資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE Tree 運算子。 如需詳細資訊，請參閱線上分析處理（OLAP） OLE DB。|  
|**adSchemaPrimaryKeys**|28|會傳回由指定使用者在資料庫目錄中定義的主索引鍵資料行。<br /><br /> （PRIMARY_KEYS 資料列集）|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|會傳回由程序所傳回資料列集之資料行的相關資訊。<br /><br /> （PROCEDURE_COLUMNS 資料列集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|會傳回程序的參數和傳回碼的相關資訊。<br /><br /> （PROCEDURE_PARAMETERS 資料列集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|傳回由指定使用者所擁有的目錄中定義的程式。<br /><br /> （程式資料列集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|傳回維度之每個層級可用屬性的相關資訊。<br /><br /> （屬性資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|當提供者定義自己的非標準架構查詢時使用。|\<提供者特定>|  
|**adSchemaProviderTypes**|22|傳回資料提供者所支援的（基底）資料類型。<br /><br /> （PROVIDER_TYPES 資料列集）|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|傳回指定之使用者所擁有的目錄中定義的參考條件約束。<br /><br /> （REFERENTIAL_CONSTRAINTS 資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|傳回指定使用者所擁有的架構（資料庫物件）。<br /><br /> （架構資料列集）|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|會傳回由資料庫目錄中定義的 SQL 實作處理資料所支援的一致性層級、選項和用語。<br /><br /> （SQL_LANGUAGES 資料列集）|\<無>|  
|**adSchemaStatistics**|19|傳回指定使用者所擁有的目錄中定義的統計資料。<br /><br /> （STATISTICS 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|傳回指定使用者所擁有之目錄中定義的資料表條件約束。<br /><br /> （TABLE_CONSTRAINTS 資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|會傳回指定使用者可以取得或授與的資料表權限 (定義在資料庫目錄中)。<br /><br /> （TABLE_PRIVILEGES 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|會傳回指定使用者可以存取的資料庫目錄中所定義的資料表 (包括檢視表)。<br /><br /> （資料表資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|傳回在目錄中定義的字元翻譯，可供指定的使用者存取。<br /><br /> （翻譯資料列集）|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|保留供未來使用。||  
|**adSchemaUsagePrivileges**|15|傳回目錄中定義之物件的許可權，這些物件可由指定的使用者取得或授與。<br /><br /> （USAGE_PRIVILEGES 資料列集）|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE 授權者被授與者|  
|**adSchemaViewColumnUsage**|24|傳回在目錄中所定義且由指定使用者所擁有之已查看資料表的資料行相依。<br /><br /> （VIEW_COLUMN_USAGE 資料列集）|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|傳回在目錄中定義的視圖，可供指定的使用者存取。<br /><br /> （VIEWS 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|會傳回所檢視資料表 (定義在資料庫目錄中，並且由指定使用者所擁有) 是相依的資料表。<br /><br /> （VIEW_TABLE_USAGE 資料列集）|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums。判斷提示|  
|AdoEnums. Schema. 目錄|  
|AdoEnums. Schema. CHARACTERSETS|  
|AdoEnums. Schema. CHECKCONSTRAINTS|  
|AdoEnums。定序|  
|AdoEnums. Schema. COLUMNPRIVILEGES|  
|AdoEnums。資料行|  
|AdoEnums. Schema. COLUMNSDOMAINUSAGE|  
|AdoEnums. Schema. CONSTRAINTCOLUMNUSAGE|  
|AdoEnums. Schema. CONSTRAINTTABLEUSAGE|  
|AdoEnums。 CUBE|  
|AdoEnums. Schema. DBINFOKEYWORDS|  
|AdoEnums. Schema. DBINFOLITERALS|  
|AdoEnums 維度|  
|AdoEnums. Schema. FOREIGNKEYS|  
|AdoEnums。階層架構|  
|AdoEnums。|  
|AdoEnums. Schema. KEYCOLUMNUSAGE|  
|AdoEnums 層級|  
|AdoEnums。量值|  
|AdoEnums 成員|  
|AdoEnums. Schema. PRIMARYKEYS|  
|AdoEnums. Schema. PROCEDURECOLUMNS|  
|AdoEnums. Schema. PROCEDUREPARAMETERS|  
|AdoEnums 程式|  
|AdoEnums。 PROPERTIES|  
|AdoEnums. Schema. PROVIDERSPECIFIC|  
|AdoEnums. Schema. PROVIDERTYPES|  
|AdoEnums. Schema. REFERENTIALCONTRAINTS|  
|AdoEnums 架構|  
|AdoEnums. Schema. SQLLANGUAGES|  
|AdoEnums。統計資料|  
|AdoEnums. Schema. TABLECONSTRAINTS|  
|AdoEnums. Schema. TABLEPRIVILEGES|  
|AdoEnums。|  
|AdoEnums。|  
|AdoEnums。受信者|  
|AdoEnums. Schema. USAGEPRIVILEGES|  
|AdoEnums. Schema. VIEWCOLUMNUSAGE|  
|AdoEnums。 VIEWS|  
|AdoEnums. Schema. VIEWTABLEUSAGE|  
  
## <a name="applies-to"></a>套用至  
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
