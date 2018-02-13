---
title: SchemaEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SchemaEnum
helpviewer_keywords:
- SchemaEnum enumeration [ADO]
ms.assetid: 21c97651-297f-469f-b5b5-c48af72b62a8
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc84741e1963b2c484e82eea7bc3de08cf12da13
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="schemaenum"></a>SchemaEnum
指定的結構描述類型**資料錄集**， [OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法擷取。  
  
## <a name="remarks"></a>備註  
 函式和資料行的其他資訊傳回的每個 ADO 常數可以在主題中找到有關[附錄 b： 結構描述資料列集](http://msdn.microsoft.com/en-us/2b5fbf03-e50d-44ee-bc57-5a57666c55f1)的 OLE DB 程式設計人員參考。 下表的 [描述] 部分中的括號中，會列出每個主題的名稱。  
  
 函式和資料行的其他資訊傳回的每個 ADO MD 常數可以在主題中找到有關[OLE DB for OLAP 物件和結構描述資料列集](http://msdn.microsoft.com/en-us/d20bb2a6-68bd-423f-9ec8-eb930cd0c144)OLE DB 中的線上分析處理 (OLAP) 文件。 下表描述資料行中的括號中，會列出每個主題的名稱。  
  
 您可以藉由參考物件的 [描述] 資料行轉譯至 ADO 資料類型的 OLE DB 文件中的資料行的資料型別[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)主題。 例如，OLE DB 資料類型的**DBTYPE_WSTR**相當於 ADO 資料型別**adWChar**。  
  
 ADO 會產生結構描述類似的結果為常數， **adSchemaDBInfoKeywords**和**adSchemaDBInfoLiterals**。 建立 ADO**資料錄集**，然後以分別傳回的值填入每個資料列**IDBInfo::GetKeywords**和**IDBInfo::GetLiteralInfo**方法。 這些方法的相關資訊，可以找到中[IDBInfo](http://msdn.microsoft.com/en-us/3f5ad97f-3fc6-4f21-b691-f6911e4007f3)的 OLE DB 程式設計人員參考 > 一節。  
  
|常數|Value|Description|條件約束資料行|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|傳回給定使用者所擁有的判斷提示在目錄中定義。<br /><br /> （判斷提示資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|傳回可從 DBMS 存取目錄相關聯的實體屬性。<br /><br /> （目錄資料列集）|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|傳回指定的使用者可以存取的字集目錄中定義。<br /><br /> （CHARACTER_SETS 資料列集）|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|傳回的檢查條件約束定義類別目錄中給定使用者所擁有。<br /><br /> (CHECK_CONSTRAINTS)資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|傳回字元的定序在目錄中定義可指定使用者存取。<br /><br /> （定序資料列集）|COLLATION_CATALOG COLLATION_SCHEMA SYS.DATABASES|  
|**adSchemaColumnPrivileges**|13|傳回可用，或授與的指定使用者在目錄中定義資料表的資料行的權限。<br /><br /> （COLUMN_PRIVILEGES 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|傳回之資料表 （包括檢視） 在目錄中定義的指定使用者存取的資料行。<br /><br /> （資料行資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|傳回相依於網域目錄中定義且由指定使用者所擁有的資料行目錄中定義。<br /><br /> (COLUMN_DOMAIN_USAGE Rowset)|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|傳回由參考條件約束、 唯一條件約束、 check 條件約束，以及判斷提示，在目錄中定義，而且給定使用者所擁有的資料行。<br /><br /> (CONSTRAINT_COLUMN_USAGE Rowset)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|傳回所使用的參考條件約束、 唯一條件約束、 check 條件約束，以及判斷提示目錄中定義且由指定使用者所擁有的資料表。<br /><br /> （CONSTRAINT_TABLE_USAGE 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|傳回結構描述 （或類別目錄，如果提供者不支援結構描述） 中的可用 cube 的相關資訊。<br /><br /> （CUBE 資料列集 *）|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|傳回提供者特定關鍵字的清單。<br /><br /> (IDBInfo::GetKeywords)|\<無 >|  
|**adSchemaDBInfoLiterals**|31|傳回在文字命令中使用的提供者專屬常值的清單。<br /><br /> (IDBInfo::GetLiteralInfo)|\<無 >|  
|**adSchemaDimensions**|33|傳回指定 cube 中之維度相關的資訊。 它有一個資料列，每個維度。<br /><br /> （維度資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|傳回由指定使用者在目錄中定義的外部索引鍵資料行。<br /><br /> （FOREIGN_KEYS 資料列集）|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|傳回維度中，您可以使用階層的相關資訊。<br /><br /> （階層資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|傳回定義類別目錄中給定使用者所擁有的索引。<br /><br /> （索引資料列集）|TABLE_CATALOG 排列 TABLE_SCHEMA INDEX_NAME 類型 TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|傳回由指定使用者條件約束為索引鍵的資料行目錄中定義。<br /><br /> (KEY_COLUMN_USAGE Rowset)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG 排列 TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|傳回可用維度中的層級的相關資訊。<br /><br /> （層級資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME L LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|傳回可用的量值的相關資訊。<br /><br /> （量值資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|傳回可用的成員相關資訊。<br /><br /> （成員資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE 樹狀運算子。 如需詳細資訊，請參閱 OLE DB 的線上分析處理 (OLAP)。|  
|**adSchemaPrimaryKeys**|28|傳回由指定使用者在目錄中定義的主索引鍵資料行。<br /><br /> （PRIMARY_KEYS 資料列集）|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|會傳回由程序所傳回資料列集之資料行的相關資訊。<br /><br /> （PROCEDURE_COLUMNS 資料列集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|會傳回程序的參數和傳回碼的相關資訊。<br /><br /> （PROCEDURE_PARAMETERS 資料列集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|傳回給定使用者所擁有的程序在目錄中定義。<br /><br /> （程序資料列集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|傳回維度的每個層級的可用屬性的相關資訊。<br /><br /> （屬性資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|如果提供者會定義它自己的非標準的結構描述查詢，使用。|\<提供者特定 >|  
|**adSchemaProviderTypes**|22|傳回的資料提供者所支援的 （基底） 資料類型。<br /><br /> （PROVIDER_TYPES 資料列集）|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|傳回的參考條件約束定義類別目錄中給定使用者所擁有。<br /><br /> （REFERENTIAL_CONSTRAINTS 資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|傳回給定使用者所擁有的結構描述 （資料庫物件）。<br /><br /> （結構描述資料列集）|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|傳回一致性層級、 選項和支援的目錄中定義的 SQL 實作處理資料的方言。<br /><br /> （SQL_LANGUAGES 資料列集）|\<無 >|  
|**adSchemaStatistics**|19|傳回給定使用者所擁有的統計資料在目錄中定義。<br /><br /> （統計資料資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|傳回資料表定義的條件約束目錄中某位使用者所擁有。<br /><br /> （TABLE_CONSTRAINTS 資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|傳回可用，或授與的指定使用者在目錄中定義資料表的權限。<br /><br /> （TABLE_PRIVILEGES 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|傳回的資料表 （包括檢視） 在目錄中定義可指定使用者存取。<br /><br /> （資料表資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|傳回指定的使用者可以存取的字元轉譯在目錄中定義。<br /><br /> （轉譯資料列集）|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|保留供日後使用。||  
|**adSchemaUsagePrivileges**|15|傳回可用，或授與的指定使用者在目錄中定義物件的使用量權限。<br /><br /> （USAGE_PRIVILEGES 資料列集）|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE 授與者授與者|  
|**adSchemaViewColumnUsage**|24|傳回用的資料行中檢視資料表、 在目錄中定義，擁有者指定的使用者，是相依。<br /><br /> (VIEW_COLUMN_USAGE Rowset)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|傳回定義類別目錄中給定的使用者可以存取的檢視。<br /><br /> （檢視資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|傳回所在的資料表中檢視資料表、 在目錄中定義，擁有者指定的使用者，是相依。<br /><br /> （VIEW_TABLE_USAGE 資料列集）|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 Package: **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.Schema.ASSERTS|  
|AdoEnums.Schema.CATALOGS|  
|AdoEnums.Schema.CHARACTERSETS|  
|AdoEnums.Schema.CHECKCONSTRAINTS|  
|AdoEnums.Schema.COLLATIONS|  
|AdoEnums.Schema.COLUMNPRIVILEGES|  
|AdoEnums.Schema.COLUMNS|  
|AdoEnums.Schema.COLUMNSDOMAINUSAGE|  
|AdoEnums.Schema.CONSTRAINTCOLUMNUSAGE|  
|AdoEnums.Schema.CONSTRAINTTABLEUSAGE|  
|AdoEnums.Schema.CUBES|  
|AdoEnums.Schema.DBINFOKEYWORDS|  
|AdoEnums.Schema.DBINFOLITERALS|  
|AdoEnums.Schema.DIMENSIONS|  
|AdoEnums.Schema.FOREIGNKEYS|  
|AdoEnums.Schema.HIERARCHIES|  
|AdoEnums.Schema.INDEXES|  
|AdoEnums.Schema.KEYCOLUMNUSAGE|  
|AdoEnums.Schema.LEVELS|  
|AdoEnums.Schema.MEASURES|  
|AdoEnums.Schema.MEMBERS|  
|AdoEnums.Schema.PRIMARYKEYS|  
|AdoEnums.Schema.PROCEDURECOLUMNS|  
|AdoEnums.Schema.PROCEDUREPARAMETERS|  
|AdoEnums.Schema.PROCEDURES|  
|AdoEnums.Schema.PROPERTIES|  
|AdoEnums.Schema.PROVIDERSPECIFIC|  
|AdoEnums.Schema.PROVIDERTYPES|  
|AdoEnums.Schema.REFERENTIALCONTRAINTS|  
|AdoEnums.Schema.SCHEMATA|  
|AdoEnums.Schema.SQLLANGUAGES|  
|AdoEnums.Schema.STATISTICS|  
|AdoEnums.Schema.TABLECONSTRAINTS|  
|AdoEnums.Schema.TABLEPRIVILEGES|  
|AdoEnums.Schema.TABLES|  
|AdoEnums.Schema.TRANSLATIONS|  
|AdoEnums.Schema.TRUSTEES|  
|AdoEnums.Schema.USAGEPRIVILEGES|  
|AdoEnums.Schema.VIEWCOLUMNUSAGE|  
|AdoEnums.Schema.VIEWS|  
|AdoEnums.Schema.VIEWTABLEUSAGE|  
  
## <a name="applies-to"></a>適用於  
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
