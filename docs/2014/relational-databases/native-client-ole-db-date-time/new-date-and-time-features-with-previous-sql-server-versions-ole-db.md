---
title: 先前 SQL Server 版本的新日期和時間功能（OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], enhanced behavior with earlier SQL Server versions
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc810ced25733ce77d80c7bec38b03e3aaf3753a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63233072"
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>舊版 SQL Server 的新日期和時間功能 (OLE DB)
  本主題描述當使用增強型日期和時間功能的用戶端應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的版本進行通訊時，以及使用早于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的 Native client 版本所編譯的用戶端將命令傳送到支援增強型日期和時間功能的伺服器時的預期行為。  
  
## <a name="down-level-client-behavior"></a>下層用戶端行為  
 使用早于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的 Native client 版本的用戶端應用程式，請將新的日期/ `nvarchar`時間類型視為資料行。 資料行內容是常值表示法。 如需詳細資訊，請參閱資料類型支援的「資料格式：字串和常值」一節，[以取得 OLE DB 的日期和時間改善](data-type-support-for-ole-db-date-and-time-improvements.md)。 資料行大小是針對資料行指定之有效位數的最大常值長度。  
  
 資料庫目錄 API 將會傳回與傳回到用戶端之下層資料類型程式碼一致的中繼資料 (例如，`nvarchar`)，以及相關聯的下層表示法 (例如，適當的常值格式)。 不過，傳回的資料類型名稱將會是實際的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 類型名稱。  
  
 當下層用戶端應用程式針對已建立日期[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] /時間類型的架構變更的（或更新版本）伺服器執行時，預期的行為如下所示：  
  
|OLE DB 用戶端類型|SQL Server 2005 類型|SQL Server 2008 (或更新版本) 類型|結果轉換 (伺服器到用戶端)|參數轉換 (用戶端到伺服器)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|Datetime|日期|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||時間欄位會設定為零。|如果時間欄位不是零，IRowsetChange 將會因為字串截斷而失敗。|  
|DBTYPE_DBTIME||Time(0)|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||日期欄位設定為目前的日期。|如果小數秒不是零，IRowsetChange 將會因為字串截斷而失敗。<br /><br /> 忽略日期。|  
|DBTYPE_DBTIME||Time(7)|失敗-不正確時間常值。|[確定]|  
|DBTYPE_DBTIMESTAMP|||失敗-不正確時間常值。|[確定]|  
|DBTYPE_DBTIMESTAMP||Datetime2 （3）|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP||Datetime2 （7）|[確定]|[確定]|  
|DBTYPE_DBDATE|Smalldatetime|日期|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||時間欄位會設定為零。|如果時間欄位不是零，IRowsetChange 將會因為字串截斷而失敗。|  
|DBTYPE_DBTIME||Time(0)|[確定]|[確定]|  
|DBTYPE_DBTIMESTAMP|||日期欄位設定為目前的日期。|如果小數秒不是零，IRowsetChange 將會因為字串截斷而失敗。<br /><br /> 忽略日期。|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|[確定]|[確定]|  
  
 OK 表示，如果它使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，則應該繼續使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本)。  
  
 只有下列最常見的結構描述變更已經列入考慮：  
  
-   在符合邏輯之處使用新的類型時，應用程式僅需要一個日期或時間值。 不過，系統會強迫應用程式使用 `datetime` 或 `smalldatetime`，因為無法使用個別的日期或時間類型。  
  
-   使用新類型會得到額外的小數秒精確度或正確度。  
  
-   切換到 `datetime2`，因為這是適用於日期和時間的慣用資料類型。  
  
 使用透過 ICommandWithParameters：： GetParameterInfo 或架構資料列集取得之伺服器中繼資料的應用程式，透過 ICommandWithParameters：： SetParameterInfo 來設定參數類型資訊時，將會在用戶端轉換期間失敗，而來源類型的字串表示會大於目的地類型的字串標記法。 例如，如果用戶端系結使用 DBTYPE_DBTIMESTAMP 而伺服器資料行是日期， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client 會將值轉換為 "yyyy-mm-dd hh： mm： ss. fff"，但是伺服器中繼資料將會當做傳回`nvarchar(10)`。 產生的溢位會造成 DBSTATUS_E_CATCONVERTVALUE。 IRowsetChange 的資料轉換會引發類似的問題，因為資料列集中繼資料是從結果集中繼資料設定而來。  
  
### <a name="parameter-and-rowset-metadata"></a>參數和資料列集中繼資料  
 本節針對以早于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的 Native Client 版本編譯的用戶端，描述參數、結果資料行和架構資料列集的中繼資料。  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 DBPARAMINFO 結構會透過*prgparaminfo 以*參數傳回下列資訊：  
  
|參數類型|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19，21. 27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26，28. 34|~0|~0|  
  
 請注意，部分值範圍不是連續的；例如，在 8,10..16 中缺少 9。 這是當小數有效位數大於零時增加的小數點所導致。  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 系統會傳回下列資料行：  
  
|資料行類型|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE、DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|date|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19，21. 27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26，28. 34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 結構會傳回下列資訊：  
  
|參數類型|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19，21. 27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26，28. 34|~0|~0|  
  
### <a name="schema-rowsets"></a>結構描述資料列集  
 本節討論參數中繼資料、結果資料行，以及新資料類型的結構描述資料列集。 如果您的用戶端提供者是使用早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client 的工具所開發，這種資訊就很有用。  
  
#### <a name="columns-rowset"></a>COLUMNS 資料列集  
 系統會傳回日期/時間類型的下列資料行值：  
  
|資料行類型|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|date|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16、20. 32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|Datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19，21. 27|38，42. 54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26，28. 34|52、56. 68|NULL|  
  
#### <a name="procedure_parameters-rowset"></a>PROCEDURE_PARAMETERS 資料列集  
 系統會傳回日期/時間類型的下列資料行值：  
  
|資料行類型|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|date|DBTYPE_WSTR|10|20|date|  
|time|DBTYPE_WSTR|8, 10..16|16、20. 32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|Datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|Datetime|  
|datetime2|DBTYPE_WSTR|19，21. 27|38，42. 54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26，28. 34|52、56. 68|datetimeoffset|  
  
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
 當連接到比[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]更早版本的伺服器時，任何嘗試使用新伺服器類型名稱的程式（例如，with ICommandWithParameters：： SetParameterInfo 或 ITableDefinition：： CreateTable）都會導致 DB_E_BADTYPENAME。  
  
 如果針對參數或結果繫結新類型，而不使用類型名稱，並將新類型用於隱含地指定伺服器類型，或者從伺服器類型到用戶端類型沒有有效的轉換，則會傳回 DB_E_ERRORSOCCURRED，而且會將 DBBINDSTATUS_UNSUPPORTED_CONVERSION 設定為執行時所使用之存取子的繫結狀態。  
  
 如果在連接上有從緩衝區類型到伺服器版本之伺服器類型的支援用戶端轉換，則可以使用所有用戶端緩衝區類型。 在此內容中，*伺服器類型*表示 ICommandWithParameters：： SetParameterInfo 所指定的類型，或如果尚未呼叫 ICommandWithParameters：： SetParameterInfo，則由緩衝區類型所隱含。 也就是說，DBTYPE_DBTIME2 和 DBTYPE_DBTIMESTAMPOFFSET 可以搭配下層伺服器使用，或者當 DataTypeCompatibility=80 時，如果用戶端成功轉換到支援的伺服器類型，也可以這麼做。 當然，如果伺服器類型不正確，當伺服器無法隱含地轉換到實際的伺服器類型時，仍然可能會回報錯誤。  
  
## <a name="ssprop_init_datatypecompatibility-behavior"></a>SSPROP_INIT_DATATYPECOMPATIBILITY 行為  
 當 SSPROP_INIT_DATATYPECOMPATIBILITY 設定為 SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000 時，新的日期/時間類型和相關聯的中繼資料會出現在用戶端，因為它們針對下層用戶端顯示，如針對[增強型日期和時間類型的大量複製變更 &#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)中所述。  
  
## <a name="comparability-for-irowsetfind"></a>IRowsetFind 的相容性  
 新的日期/時間類型允許使用所有比較運算子，因為它們會顯示為字串類型，而非日期/時間類型。  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善 &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
