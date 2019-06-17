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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4aa145a3c42c5ed807a63dc551e67afe6af95cde
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711311"
---
# <a name="schemaenum"></a>SchemaEnum
指定的結構描述型別**Recordset**可[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法擷取。  
  
## <a name="remarks"></a>備註  
 函式和資料行的其他資訊傳回每一個 ADO 常數，請參閱中的主題[附錄 b:結構描述資料列集](https://msdn.microsoft.com/2b5fbf03-e50d-44ee-bc57-5a57666c55f1)的 OLE DB 程式設計人員參考。 下表的 [描述] 部分中的括號括住，會列出每個主題的名稱。  
  
 函式和資料行的其他資訊傳回每一個 ADO MD 常數，請參閱主題[OLE DB for OLAP 物件和結構描述資料列集](https://msdn.microsoft.com/d20bb2a6-68bd-423f-9ec8-eb930cd0c144)OLE DB 中的線上分析處理 (OLAP) 文件。 下表描述資料行中的括號括住，會列出每個主題的名稱。  
  
 您可以轉譯至 ADO 資料類型的 OLE DB 文件中的資料行的資料類型可藉由參考 ADO 的 Description 資料行[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)主題。 例如，OLE DB 資料類型**DBTYPE_WSTR**相當於 ADO 資料類型**adWChar**。  
  
 ADO 會產生常數，結構描述類似的結果**adSchemaDBInfoKeywords**並**adSchemaDBInfoLiterals**。 建立 ADO**資料錄集**，並使用分別傳回的值，然後填滿每個資料列**IDBInfo::GetKeywords**並**IDBInfo::GetLiteralInfo**方法。 這些方法的其他資訊可在[IDBInfo](https://msdn.microsoft.com/3f5ad97f-3fc6-4f21-b691-f6911e4007f3) OLE DB 程式設計人員參考一節。  
  
|常數|值|描述|條件約束資料行|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|傳回指定的使用者所擁有的判斷提示在目錄中定義。<br /><br /> （判斷提示資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|傳回資料庫目錄可從 DBMS 存取相關聯的實體屬性。<br /><br /> （目錄資料列集）|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|傳回目錄中定義的字元集會指定使用者可以存取。<br /><br /> （CHARACTER_SETS 資料列集）|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|傳回的檢查條件約束定義在目錄中給定使用者所擁有。<br /><br /> (CHECK_CONSTRAINTS)資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|傳回的字元定序定義在目錄中所指定的使用者進行存取。<br /><br /> （定序資料列集）|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|傳回可用，或授與的指定使用者在目錄中定義資料表的資料行的權限。<br /><br /> （COLUMN_PRIVILEGES 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|傳回資料表的資料行 （包括檢視表） 目錄中定義所指定的使用者進行存取。<br /><br /> （資料行資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|傳回相依於網域目錄中所定義且由指定使用者擁有的資料行目錄中定義。<br /><br /> (COLUMN_DOMAIN_USAGE Rowset)|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|傳回參考條件約束、 唯一條件約束、 check 條件約束和判斷提示所使用、 在目錄中定義及所指定的使用者擁有的資料行。<br /><br /> （CONSTRAINT_COLUMN_USAGE 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|傳回參考條件約束、 唯一條件約束、 check 條件約束和在目錄中定義且由指定使用者擁有的判斷提示所使用的資料表。<br /><br /> （CONSTRAINT_TABLE_USAGE 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|傳回結構描述 （或類別目錄，如果提供者不支援結構描述） 中的可用 cube 的相關資訊。<br /><br /> （CUBE 資料列集 *）|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|傳回提供者特定關鍵字的清單。<br /><br /> (IDBInfo::GetKeywords)|\<無 >|  
|**adSchemaDBInfoLiterals**|31|傳回文字命令中使用的提供者特定常值的清單。<br /><br /> (IDBInfo::GetLiteralInfo)|\<無 >|  
|**adSchemaDimensions**|33|傳回指定 cube 中維度相關的資訊。 它有一個資料列，每個維度。<br /><br /> （維度資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|傳回由指定使用者在目錄中定義的外部索引鍵資料行。<br /><br /> （FOREIGN_KEYS 資料列集）|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|傳回維度中，您可以使用階層的相關資訊。<br /><br /> （階層資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|傳回指定的使用者所擁有的索引定義在目錄中。<br /><br /> （索引資料列集）|TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TYPE TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|傳回由指定使用者條件約束為索引鍵的資料行目錄中定義。<br /><br /> (KEY_COLUMN_USAGE Rowset)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|傳回可用維度中的層級的相關資訊。<br /><br /> （層級資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|傳回可用的量值的相關資訊。<br /><br /> （量值資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|傳回可用成員的相關資訊。<br /><br /> （成員資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE 樹狀運算子。 如需詳細資訊，請參閱 OLE DB 的線上分析處理 (OLAP)。|  
|**adSchemaPrimaryKeys**|28|傳回由指定使用者在目錄中定義的主索引鍵資料行。<br /><br /> （PRIMARY_KEYS 資料列集）|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|會傳回由程序所傳回資料列集之資料行的相關資訊。<br /><br /> （PROCEDURE_COLUMNS 資料列集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|會傳回程序的參數和傳回碼的相關資訊。<br /><br /> （PROCEDURE_PARAMETERS 資料列集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|傳回指定的使用者所擁有的程序定義在目錄中。<br /><br /> （程序資料列集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|傳回維度的每個層級的可用屬性的相關資訊。<br /><br /> （屬性資料列集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|如果提供者會定義它自己的非標準的結構描述查詢，使用。|\<提供者專用 >|  
|**adSchemaProviderTypes**|22|傳回的資料提供者支援的 （基底） 的資料類型。<br /><br /> （PROVIDER_TYPES 資料列集）|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|傳回參考條件約束定義在目錄中指定的使用者所擁有。<br /><br /> （REFERENTIAL_CONSTRAINTS 資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|傳回指定的使用者所擁有的結構描述 (database objects)。<br /><br /> （結構描述資料列集）|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|傳回的一致性層級、 選項，以及定義在目錄中的 SQL 實作處理資料所支援的方言。<br /><br /> （SQL_LANGUAGES 資料列集）|\<無 >|  
|**adSchemaStatistics**|19|傳回指定的使用者所擁有的統計資料目錄中定義。<br /><br /> （統計資料資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|傳回資料表定義的條件約束在目錄中指定的使用者所擁有。<br /><br /> （TABLE_CONSTRAINTS 資料列集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|傳回資料庫目錄中定義的資料表可用，或授與的指定使用者的權限。<br /><br /> （TABLE_PRIVILEGES 資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|傳回定義的資料表 （包括檢視表） 在目錄中所指定的使用者進行存取。<br /><br /> （資料表資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|傳回指定的使用者可以存取的字元轉譯在目錄中定義。<br /><br /> （翻譯資料列集）|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|保留供日後使用。||  
|**adSchemaUsagePrivileges**|15|傳回目錄中所定義的物件，提供或由指定使用者授與的使用權限。<br /><br /> （USAGE_PRIVILEGES 資料列集）|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE 授與者授與者|  
|**adSchemaViewColumnUsage**|24|傳回在其上的資料行檢視資料表、 在目錄中定義和所指定的使用者，擁有是相依項目。<br /><br /> （VIEW_COLUMN_USAGE 資料列集）|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|傳回由指定使用者可存取的檢視表定義在目錄中。<br /><br /> （檢視資料列集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|傳回在其上的資料表檢視資料表、 目錄中定義和所指定的使用者，擁有是相依項目。<br /><br /> （VIEW_TABLE_USAGE 資料列集）|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
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
