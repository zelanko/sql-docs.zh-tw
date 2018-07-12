---
title: 大型 CLR 使用者定義型別 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC, large user-defined types
- large user-defined types [ODBC]
ms.assetid: ddce337e-bb6e-4a30-b7cc-4969bb1520a9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 14dcac32a0e8e6af89cf3f9dc87b2458a986a2ef
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414417"
---
# <a name="large-clr-user-defined-types-odbc"></a>大型 CLR 使用者定義型別 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主題討論 SQL Server Native Client 中 ODBC 的變更，以支援大型 Common Language Runtime (CLR) 使用者定義型別 (UDT)。  
  
 如需示範 ODBC 對於大型 CLR Udt 支援範例，請參閱[支援大型 Udt](../../../relational-databases/native-client-odbc-how-to/support-for-large-udts.md)。  
  
 如需有關 SQL Server Native Client 中大型 CLR Udt 支援的詳細資訊，請參閱[Large CLR User-Defined 類型](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)。  
  
## <a name="data-format"></a>資料格式  
 SQL Server Native Client 會使用 SQL_SS_LENGTH_UNLIMITED 來表示大型物件 (LOB) 類型的資料行大小大於 8,000 個位元組。 從 SQL Server 2008 開始，當 CLR UDT 的值大於 8,000 個位元組時，將會針對 CLR UDT 使用相同的值。  
  
 UDT 值會表示為位元組陣列。 支援與十六進位字串之間的來回轉換。 常值會表示為具有 "0x" 前置詞的十六進位字串。  
  
 下表顯示參數和結果集內的資料類型對應：  
  
|SQL Server 資料類型|SQL 資料類型|值|  
|--------------------------|-------------------|-----------|  
|CLR UDT|SQL_SS_UDT|-151 (sqlncli.h)|  
  
 下表討論對應的結構和 ODBC C 類型。 基本上，是 CLR UDT **varbinary**具有額外的中繼資料型別。  
  
|SQL 資料類型|記憶體配置|C 資料類型|值 (sqlext.h)|  
|-------------------|-------------------|-----------------|------------------------|  
|SQL_SS_UDT|SQLCHAR * (unsigned char \*)|SQL_C_BINARY|SQL_BINARY (-2)|  
  
## <a name="descriptor-fields-for-parameters"></a>參數的描述項欄位  
 IPD 欄位中傳回的資訊如下所示：  
  
|描述項欄位|SQL_SS_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|SQL_SS_UDT<br /><br /> (長度大於 8,000 個位元組)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|包含 UDT 的目錄名稱。|包含 UDT 的目錄名稱。|  
|SQL_CA_SS_UDT_SCHEMA_NAME|包含 UDT 的結構描述名稱。|包含 UDT 的結構描述名稱。|  
|SQL_CA_SS_UDT_TYPE_NAME|UDT 的名稱。|UDT 的名稱。|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的完整名稱。|UDT 的完整名稱。|  
  
 UDT 參數，SQL_CA_SS_UDT_TYPE_NAME 一定要設定透過**SQLSetDescField**。 SQL_CA_SS_UDT_CATALOG_NAME 和 SQL_CA_SS_UDT_SCHEMA_NAME 是選擇性的。  
  
 如果在相同的資料庫中使用與資料表不同的結構描述來定義 UDT，必須要設定 SQL_CA_SS_UDT_SCHEMA_NAME。  
  
 如果在與資料表不同的資料庫中定義 UDT，則必須設定 SQL_CA_SS_UDT_CATALOG_NAME 和 SQL_CA_SS_UDT_SCHEMA_NAME。  
  
 如果 SQL_CA_SS_UDT_TYPE_NAME、SQL_CA_SS_UDT_CATALOG_NAME 或 SQL_CA_SS_UDT_SCHEMA_NAME 的設定有任何錯誤或省略，則會產生診斷記錄，其中包含 SQLSTATE HY000 和伺服器特有的訊息文字。  
  
## <a name="descriptor-fields-for-results"></a>結果的描述項欄位  
 IRD 欄位中傳回的資訊如下所示：  
  
|描述項欄位|SQL_SS_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|SQL_SS_UDT<br /><br /> (長度大於 8,000 個位元組)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_DISPLAY_SIZE|2*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LITERAL_PREFIX|"0x"|"0x"|  
|SQL_DESC_LITERAL_SUFFIX|""|""|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|SQL_PRED_NONE|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|包含 UDT 的目錄名稱。|包含 UDT 的目錄名稱。|  
|SQL_CA_SS_UDT_SCHEMA_NAME|包含 UDT 的結構描述名稱。|包含 UDT 的結構描述名稱。|  
|SQL_CA_SS_UDT_TYPE_NAME|UDT 的名稱。|UDT 的名稱。|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的完整名稱。|UDT 的完整名稱。|  
  
## <a name="column-metadata-returned-by-sqlcolumns-and-sqlprocedurecolumns-catalog-metadata"></a>SQLColumns 和 SQLProcedureColumns 傳回的資料行中繼資料 (目錄中繼資料)  
 下列資料行值是針對 UDT 所傳回：  
  
|資料行名稱|SQL_SS_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|SQL_SS_UDT<br /><br /> (長度大於 8,000 個位元組)|  
|-----------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|TYPE_NAME|UDT 的名稱。|UDT 的名稱。|  
|COLUMN_SIZE|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|BUFFER_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|DECIMAL_DIGITS|NULL|NULL|  
|SQL_DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DATETIME_SUB|NULL|NULL|  
|CHAR_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SS_UDT_CATALOG_NAME|包含 UDT 的目錄名稱。|包含 UDT 的目錄名稱。|  
|SS_UDT_SCHEMA_NAME|包含 UDT 的結構描述名稱。|包含 UDT 的結構描述名稱。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的完整名稱。|UDT 的完整名稱。|  
  
 最後三個資料行是驅動程式特有的資料行。 它們會加入任何 ODBC 定義的資料行之後, 但在任何現有的驅動程式專用資料行的 SQLColumns 或 SQLProcedureColumns 的結果集之前。  
  
 針對個別 Udt 或泛型類型"udt"SQLGetTypeInfo，會不傳回任何資料列。  
  
## <a name="bindings-and-conversions"></a>繫結和轉換  
 從 SQL 到 C 資料類型的支援轉換如下所示：  
  
|來回轉換：|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|支援 *|  
|SQL_C_BINARY|支援|  
|SQL_C_CHAR|支援 *|  
  
 \* 二進位資料會轉換成十六進位字串。  
  
 從 C 到 SQL 資料類型的支援轉換如下所示：  
  
|來回轉換：|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|支援 *|  
|SQL_C_BINARY|支援|  
|SQL_C_CHAR|支援 *|  
  
 \* 二進位資料轉換成十六進位字串，就會發生。  
  
## <a name="sqlvariant-support-for-udts"></a>UDT 的 SQL_VARIANT 支援  
 SQL_VARIANT 資料行中不支援 UDT。  
  
## <a name="bcp-support-for-udts"></a>UDT 的 BCP 支援  
 UDT 值只能當做字元或二進位值來匯入或匯出。  
  
## <a name="downlevel-client-behavior-for-udts"></a>UDT 的下層用戶端行為  
 UDT 受限於與下層用戶端對應的類型，如下所示：  
  
|伺服器版本|SQL_SS_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|SQL_SS_UDT<br /><br /> (長度大於 8,000 個位元組)|  
|--------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL Server 2005|**UDT**|**varbinary(max)**|  
|SQL Server 2008 及更新版本|**UDT**|**UDT**|  
  
## <a name="odbc-functions-supporting-large-clr-udts"></a>支援大型 CLR UDT 的 ODBC 函數  
 本章節討論 SQL Server Native Client ODBC 函數為了支援大型 CLR UDT 所做的變更。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 UDT 結果資料行值會從 SQL 轉換成 C 資料類型，如本主題稍早的「繫結和轉換」一節所述。  
  
### <a name="sqlbindparameter"></a>SQLBindParameter  
 UDT 所需的值如下所示：  
  
|SQL 資料類型|*Parametertype*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|---------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (長度大於 8,000 個位元組)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 針對 UDT 傳回的值如同本主題稍早的「結果的描述項欄位」一節所述。  
  
### <a name="sqlcolumns"></a>SQLColumns  
 針對 UDT 傳回的值如同本主題稍早的「SQLColumns 和 SQLProcedureColumns 傳回的資料行中繼資料 (目錄中繼資料)」一節所述。  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 針對 UDT 傳回的值如下所示：  
  
|SQL 資料類型|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (長度大於 8,000 個位元組)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqldescribeparam"></a>SQLDescribeParam  
 針對 UDT 傳回的值如下所示：  
  
|SQL 資料類型|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (長度大於 8,000 個位元組)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlfetch"></a>SQLFetch  
 UDT 結果資料行值會從 SQL 轉換成 C 資料類型，如本主題稍早的「繫結和轉換」一節所述。  
  
### <a name="sqlfetchscroll"></a>SQLFetchScroll  
 UDT 結果資料行值會從 SQL 轉換成 C 資料類型，如本主題稍早的「繫結和轉換」一節所述。  
  
### <a name="sqlgetdata"></a>SQLGetData  
 UDT 結果資料行值會從 SQL 轉換成 C 資料類型，如本主題稍早的「繫結和轉換」一節所述。  
  
### <a name="sqlgetdescfield"></a>SQLGetDescField  
 有提供新類型的描述項欄位在本主題稍早的「參數的描述項欄位」和「結果的描述項欄位」章節中有加以描述。  
  
### <a name="sqlgetdescrec"></a>SQLGetDescRec  
 針對 UDT 傳回的值如下所示：  
  
|SQL 資料類型|類型|子類型|長度|有效位數|小數位數|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|SQL_SS_UDT|0|*n*|n|0|  
|SQL_SS_UDT<br /><br /> (長度大於 8,000 個位元組)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 針對 UDT 傳回的值如同本主題稍早的「SQLColumns 和 SQLProcedureColumns 傳回的資料行中繼資料 (目錄中繼資料)」一節所述。  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 針對 UDT 傳回的值如同本主題稍早的「SQLColumns 和 SQLProcedureColumns 傳回的資料行中繼資料 (目錄中繼資料)」一節所述。  
  
### <a name="sqlputdata"></a>SQLPutData  
 UDT 參數值會從 C 轉換成 SQL 資料類型，如本主題稍早的「繫結和轉換」一節所述。  
  
### <a name="sqlsetdescfield"></a>SQLSetDescField  
 有提供新類型的描述項欄位在本主題稍早的「參數的描述項欄位」和「結果的描述項欄位」章節中有加以描述。  
  
### <a name="sqlsetdescrec"></a>SQLSetDescRec  
 UDT 允許的值如下所示：  
  
|SQL 資料類型|類型|子類型|長度|有效位數|小數位數|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|SQL_SS_UDT|0|*n*|*n*|0|  
|SQL_SS_UDT<br /><br /> (長度大於 8,000 個位元組)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlspecialcolumns"></a>SQLSpecialColumns  
 針對資料行 DATA_TYPE、TYPE_NAME、COLUMN_SIZE、BUFFER_LENGTH 和 DECIMAL_DIGTS UDT 傳回的值如同本主題稍早的「SQLColumns 和 SQLProcedureColumns 傳回的資料行中繼資料 (目錄中繼資料)」一節所述。  
  
## <a name="see-also"></a>另請參閱  
 [大型 CLR 使用者定義型別](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
  
  
