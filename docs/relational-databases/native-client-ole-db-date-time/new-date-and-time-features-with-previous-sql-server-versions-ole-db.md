---
title: 新的日期和時間功能與舊版 SQL Server (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6757868bf492a08caec1b8062776d6634331f868
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666726"
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>舊版 SQL Server 的新日期和時間功能 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用增強型的日期和時間功能的用戶端應用程式進行通訊的版本時，本主題會說明預期的行為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，以及當編譯版本的用戶端[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端早於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]將命令傳送到伺服器支援增強型日期和時間功能。  
  
## <a name="down-level-client-behavior"></a>下層用戶端行為  
 使用新版的用戶端應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端之前[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]查看新的日期/時間類型為**nvarchar**資料行。 資料行內容是常值表示法。 如需詳細資訊，請參閱 「 資料格式： 字串和常值 」 一節[OLE DB 日期和時間改善的資料型別支援](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。 資料行大小是針對資料行指定之有效位數的最大常值長度。  
  
 資料庫目錄 Api 將會傳回中繼資料一致，以傳回至用戶端之下層資料型別程式碼 (例如**nvarchar**) 和相關聯的下層表示法 （例如，適當常值格式）。 不過，傳回的資料類型名稱將會是實際的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 類型名稱。  
  
 當下層用戶端應用程式會針對執行[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更新版本） 的結構描述變更，為日期/時間類型所做的伺服器，預期的行為如下所示：  
  
|OLE DB 用戶端類型|SQL Server 2005 類型|SQL Server 2008 (或更新版本) 類型|結果轉換 (伺服器到用戶端)|參數轉換 (用戶端到伺服器)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|DATETIME|date|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||時間欄位會設定為零。|如果時間欄位為非零，IRowsetChange 將會因為字串截斷而失敗。|  
|DBTYPE_DBTIME||Time(0)|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||日期欄位設定為目前的日期。|如果小數秒數為非零，IRowsetChange 會因為字串截斷而失敗。<br /><br /> 忽略日期。|  
|DBTYPE_DBTIME||Time(7)|失敗 – 無效的時間間隔。|[確定]|  
|DBTYPE_DBTIMESTAMP|||失敗 – 無效的時間間隔。|[確定]|  
|DBTYPE_DBTIMESTAMP||Datetime2(3)|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP||datetime2(7)|[確定]|[確定]|  
|DBTYPE_DBDATE|Smalldatetime|date|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||時間欄位會設定為零。|如果時間欄位為非零，IRowsetChange 將會因為字串截斷而失敗。|  
|DBTYPE_DBTIME||Time(0)|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||日期欄位設定為目前的日期。|如果小數秒數為非零，IRowsetChange 會因為字串截斷而失敗。<br /><br /> 忽略日期。|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|[確定]|[確定]|  
  
 OK 表示，如果它使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，則應該繼續使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本)。  
  
 只有下列最常見的結構描述變更已經列入考慮：  
  
-   在符合邏輯之處使用新的類型時，應用程式僅需要一個日期或時間值。 不過，若要使用會強迫應用程式**datetime**或是**smalldatetime**因為個別的日期和時間類型無法使用。  
  
-   使用新類型會得到額外的小數秒精確度或正確度。  
  
-   若要切換**datetime2**因為這是慣用的資料類型的日期和時間。  
  
 使用透過 icommandwithparameters:: Getparameterinfo 或結構描述資料列集取得的伺服器中繼資料來設定透過 icommandwithparameters:: Setparameterinfo 參數型別資訊的應用程式將會在用戶端轉換過程中失敗，字串來源類型表示法大於目的地類型的字串表示。 例如，如果用戶端繫結使用 DBTYPE_DBTIMESTAMP 而且伺服器資料行是日期，若[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端會將值轉換為"yyyy dd mm hh:mm:ss.fff 」，但是伺服器中繼資料將會以傳回**nvarchar(10**。 產生的溢位會造成 DBSTATUS_E_CATCONVERTVALUE。 類似的問題發生的資料轉換的 IRowsetChange，因為資料列集的中繼資料從結果集中繼資料設定。  
  
### <a name="parameter-and-rowset-metadata"></a>參數和資料列集中繼資料  
 本節說明中繼資料參數、 結果資料行，以及結構描述資料列集的版本所編譯的用戶端[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端之前[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 DBPARAMINFO 結構會傳回下列資訊，透過*prgParamInfo*參數：  
  
|參數類型|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|日期|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 請注意，部分值範圍不是連續的；例如，在 8,10..16 中缺少 9。 這是當小數有效位數大於零時增加的小數點所導致。  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 系統會傳回下列資料行：  
  
|資料行類型|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE、DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|日期|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 結構會傳回下列資訊：  
  
|參數類型|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|日期|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>結構描述資料列集  
 本節討論參數中繼資料、結果資料行，以及新資料類型的結構描述資料列集。 此資訊非常實用是您必須使用工具開發的用戶端提供者早於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端。  
  
#### <a name="columns-rowset"></a>COLUMNS 資料列集  
 系統會傳回日期/時間類型的下列資料行值：  
  
|資料行類型|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|日期|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedureparameters-rowset"></a>PROCEDURE_PARAMETERS 資料列集  
 系統會傳回日期/時間類型的下列資料行值：  
  
|資料行類型|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|日期|DBTYPE_WSTR|10|20|日期|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|DATETIME|DBTYPE_DBTIMESTAMP|NULL|NULL|DATETIME|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="providertypes-rowset"></a>PROVIDER_TYPES 資料列集  
 系統會傳回日期/時間類型的下列資料列：  
  
|類型 -><br /><br /> 「資料行」|日期|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|日期|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|日期|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>下層伺服器行為  
 當連接到伺服器的版本低於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，使用新的伺服器類型名稱 （例如，使用 icommandwithparameters:: Setparameterinfo 或 itabledefinition:: Createtable） 的任何嘗試都會導致 DB_E_BADTYPENAME。  
  
 如果針對參數或結果繫結新類型，而不使用類型名稱，並將新類型用於隱含地指定伺服器類型，或者從伺服器類型到用戶端類型沒有有效的轉換，則會傳回 DB_E_ERRORSOCCURRED，而且會將 DBBINDSTATUS_UNSUPPORTED_CONVERSION 設定為執行時所使用之存取子的繫結狀態。  
  
 如果在連接上有從緩衝區類型到伺服器版本之伺服器類型的支援用戶端轉換，則可以使用所有用戶端緩衝區類型。 在此情況下，*伺服器類型*表示 icommandwithparameters:: Setparameterinfo，所指定，或如果尚未呼叫 icommandwithparameters:: Setparameterinfo，緩衝區型別所隱含的類型。 也就是說，DBTYPE_DBTIME2 和 DBTYPE_DBTIMESTAMPOFFSET 可以搭配下層伺服器使用，或者當 DataTypeCompatibility=80 時，如果用戶端成功轉換到支援的伺服器類型，也可以這麼做。 當然，如果伺服器類型不正確，當伺服器無法隱含地轉換到實際的伺服器類型時，仍然可能會回報錯誤。  
  
## <a name="sspropinitdatatypecompatibility-behavior"></a>SSPROP_INIT_DATATYPECOMPATIBILITY 行為  
 當 SSPROP_INIT_DATATYPECOMPATIBILITY 設定為 SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000 時，新的日期/時間類型和相關聯的中繼資料會出現以用戶端濆婞剢下層用戶端中, 所述[大量複製變更增強型日期和時間型別&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
## <a name="comparability-for-irowsetfind"></a>IRowsetFind 的相容性  
 新的日期/時間類型允許使用所有比較運算子，因為它們會顯示為字串類型，而非日期/時間類型。  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
