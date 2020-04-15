---
title: 具有早期 SQL 伺服器版本的 OLE DB 功能的日期和時間
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
author: markingmyname
ms.author: maghan
ms.custom: seo-dt-2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a90863fb061912dd0a6c44fe23ba2baa402662c3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301011"
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>舊版 SQL Server 的新日期和時間功能 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題介紹使用增強日期和時間功能的用戶端應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]早於的版本通信的預期行為,以及用戶端早[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]於將命令發送到支援增強日期和時間功能的伺服器之前使用本機用戶端版本編譯時的預期行為。  
  
## <a name="down-level-client-behavior"></a>下層用戶端行為  
 早於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]將新日期/時間[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類型 視為**nvarchar**列之前使用本機用戶端版本的用戶端應用程式。 資料行內容是常值表示法。 有關詳細資訊,請參閱[OLE DB 日期和時間改進的資料類型支援的](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)「資料格式:字串和文字」部分。 資料行大小是針對資料行指定之有效位數的最大常值長度。  
  
 目錄 API 將傳回與傳回到用戶端(例如**nvarchar)** 和相關下級表示形式(例如,適當的文本格式)的低級資料類型代碼一致的中繼資料。 不過，傳回的資料類型名稱將會是實際的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 類型名稱。  
  
 當低級用戶端應用程式針對[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]已對日期/時間類型的架構更改的(或更高版本)伺服器運行時,預期行為如下所示:  
  
|OLE DB 用戶端類型|SQL Server 2005 類型|SQL Server 2008 (或更新版本) 類型|結果轉換 (伺服器到用戶端)|參數轉換 (用戶端到伺服器)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|Datetime|Date|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||時間欄位會設定為零。|如果時間欄位為非零,則 IRowsetChange 將因字串截斷而失敗。|  
|DBTYPE_DBTIME||Time(0)|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||日期欄位設定為目前的日期。|如果分數秒為非零,IRowsetChange 將因字串截斷而失敗。<br /><br /> 忽略日期。|  
|DBTYPE_DBTIME||Time(7)|失敗 - 無效時間文字。|[確定]|  
|DBTYPE_DBTIMESTAMP|||失敗 - 無效時間文字。|[確定]|  
|DBTYPE_DBTIMESTAMP||日期時間2(3)|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP||日期時間2(7)|[確定]|[確定]|  
|DBTYPE_DBDATE|Smalldatetime|Date|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||時間欄位會設定為零。|如果時間欄位為非零,IRowsetChange 將因字串截斷而失敗。|  
|DBTYPE_DBTIME||Time(0)|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||日期欄位設定為目前的日期。|如果分數秒為非零,IRowsetChange 將因字串截斷而失敗。<br /><br /> 忽略日期。|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|[確定]|[確定]|  
  
 OK 表示，如果它使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，則應該繼續使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本)。  
  
 只有下列最常見的結構描述變更已經列入考慮：  
  
-   在符合邏輯之處使用新的類型時，應用程式僅需要一個日期或時間值。 但是,由於單獨的日期和時間類型不可用,應用程式被迫使用**日期時間**或**小日期時間**。  
  
-   使用新類型會得到額外的小數秒精確度或正確度。  
  
-   切換到**日期時間 2,** 因為這是日期和時間的首選數據類型。  
  
 使用透過 ICommandWith 參數獲取的伺服器中繼資料的應用程式:getparameterinfo 或架構列集透過 ICommand 與參數::Set 參數 Info 設定參數類型資訊,在用戶端轉換期間失敗,其中源類型的字串表示形式大於目標類型的字串表示形式。 例如,如果用戶端綁定使用DBTYPE_DBTIMESTAMP並且伺服器列是日期,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]則本機用戶端將該值轉換為"yyyy-dd-mm hh:mm:ss.fff",但伺服器元數據將返回為**nvarchar(10)。** 產生的溢位會造成 DBSTATUS_E_CATCONVERTVALUE。 IRowsetChange 的數據轉換也會產生類似的問題,因為行集元數據是從結果集元數據設置的。  
  
### <a name="parameter-and-rowset-metadata"></a>參數和資料列集中繼資料  
 本節介紹早於 使用本機用戶端版本編譯的用戶端的參數、結果列和架構行集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 元[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]數據。  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 DBPARAMINFO 結構透過*prgParamInfo*參數傳回以下資訊:  
  
|參數類型|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 請注意，部分值範圍不是連續的；例如，在 8,10..16 中缺少 9。 這是當小數有效位數大於零時增加的小數點所導致。  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 系統會傳回下列資料行：  
  
|資料行類型|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE、DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|date|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 結構會傳回下列資訊：  
  
|參數類型|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>結構描述資料列集  
 本節討論參數中繼資料、結果資料行，以及新資料類型的結構描述資料列集。 此資訊很有用,因為您使用比[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端更早的工具開發了用戶端提供程式。  
  
#### <a name="columns-rowset"></a>COLUMNS 資料列集  
 系統會傳回日期/時間類型的下列資料行值：  
  
|資料行類型|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|date|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|Datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedure_parameters-rowset"></a>PROCEDURE_PARAMETERS 資料列集  
 系統會傳回日期/時間類型的下列資料行值：  
  
|資料行類型|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|date|DBTYPE_WSTR|10|20|date|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|Datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|Datetime|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="provider_types-rowset"></a>PROVIDER_TYPES 資料列集  
 系統會傳回日期/時間類型的下列資料列：  
  
|類型 -><br /><br /> 資料行|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>下層伺服器行為  
 連接到早於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]版本的伺服器時,任何嘗試使用新伺服器類型名稱(例如,使用 ICommand 與參數::設置參數資訊或 ITable 定義:createTable)的嘗試都將導致DB_E_BADTYPENAME。  
  
 如果針對參數或結果繫結新類型，而不使用類型名稱，並將新類型用於隱含地指定伺服器類型，或者從伺服器類型到用戶端類型沒有有效的轉換，則會傳回 DB_E_ERRORSOCCURRED，而且會將 DBBINDSTATUS_UNSUPPORTED_CONVERSION 設定為執行時所使用之存取子的繫結狀態。  
  
 如果在連接上有從緩衝區類型到伺服器版本之伺服器類型的支援用戶端轉換，則可以使用所有用戶端緩衝區類型。 在此上下文中,*伺服器類型*是指 ICommand 與參數指定的類型::set 參數資訊,或者如果未調用 ICommand 與參數::set 參數 Info,則緩衝區類型隱含的類型。 也就是說，DBTYPE_DBTIME2 和 DBTYPE_DBTIMESTAMPOFFSET 可以搭配下層伺服器使用，或者當 DataTypeCompatibility=80 時，如果用戶端成功轉換到支援的伺服器類型，也可以這麼做。 當然，如果伺服器類型不正確，當伺服器無法隱含地轉換到實際的伺服器類型時，仍然可能會回報錯誤。  
  
## <a name="ssprop_init_datatypecompatibility-behavior"></a>SSPROP_INIT_DATATYPECOMPATIBILITY 行為  
 當SSPROP_INIT_DATATYPECOMPATIBILITY設置為SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000時,新的日期/時間類型和相關元數據將呈現在用戶端中,因為它們出現在低級用戶端上,如 OLE DB[和 ODBC&#41;&#40;增強日期和時間類型的批量複製更改](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)中所述。  
  
## <a name="comparability-for-irowsetfind"></a>IRowsetFind 的相容性  
 新的日期/時間類型允許使用所有比較運算子，因為它們會顯示為字串類型，而非日期/時間類型。  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
