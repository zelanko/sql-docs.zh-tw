---
title: SQL柱 |微軟文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: abce98b64da8de6039f81025201cce25269763a6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302604"
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLColumn**傳回SQL_SUCCESS*目錄名稱*、*表名*或*列名*參數是否存在值。 當在這些參數中使用無效值時 **,SQLFetch**將返回SQL_NO_DATA。  
  
> [!NOTE]  
>  若是大數值類型，將會傳回包含 SQL_SS_LENGTH_UNLIMITED 值的所有長度參數。  
  
 **SQLColumns**可以在靜態伺服器游標上執行。 嘗試在可上升(動態或鍵集)游標上執行**SQLColumns**將返回SQL_SUCCESS_WITH_INFO指示游標類型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式通過接受*目錄名稱*參數的兩部分名稱 *(Linked_Server_Name.Catalog_Name)* 支援報告連結伺服器上的表的資訊。  
  
 對於 ODBC 2。*x*應用程式不使用*表名*中的通配符 **,SQLColumns**傳回有關名稱與*表Name*匹配且歸目前用戶擁有的任何表的資訊。 如果目前使用者沒有名稱與*表Name*參數匹配的表 **,SQLColumns**將傳回有關表名稱與*表Name*參數匹配的其他用戶擁有的任何表的資訊。 對於 ODBC 2。*x*應用程式使用通配符 **,SQLColumns**傳回名稱與*表格名稱*匹配的所有表。 對於 ODBC 3。*x*應用程式**SQLColumns**傳回名稱與*表Name*符合的所有表,而不考慮擁有者或是否使用通配符。  
  
 下表列出結果集傳回的資料行：  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|DATA_TYPE|返回**varchar(最大)** 數據類型的SQL_VARCHAR、SQL_VARBINARY或SQL_WVARCHAR。|  
|TYPE_NAME|返回**varchar(最大值)、varbinary(max)** 和**nvarchar(max)** 數據類型的**varbinary(max)**「varchar」、」varbinary"或"nvarchar"。|  
|COLUMN_SIZE|返回**SQL_SS_LENGTH_UNLIMITED varchar(max)** 數據類型,指示列的大小不受限制。|  
|BUFFER_LENGTH|返回**varchar(max)** 數據類型的SQL_SS_LENGTH_UNLIMITED,指示緩衝區的大小不受限制。|  
|SQL_DATA_TYPE|返回**varchar(最大)** 數據類型的SQL_VARCHAR、SQL_VARBINARY或SQL_WVARCHAR。|  
|CHAR_OCTET_LENGTH|傳回 char 或 binary 資料行的最大長度。 傳回 0 表示大小不受限制。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|傳回定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|傳回定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_NAME|傳回 XML 結構描述集合的名稱。 如果找不到名稱，則此變數包含空字串。|  
|SS_UDT_CATALOG_NAME|包含 UDT (使用者定義型別) 之目錄的名稱。|  
|SS_UDT_SCHEMA_NAME|包含 UDT 之結構描述的名稱。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的組件完整名稱。|  
  
 對於 UDT,現有的TYPE_NAME列用於指示 UDT 的名稱;對於 UDT,則使用"已使用"列"來指示 UDT 的名稱。因此,不應將其附加列添加到**SQLColumn**或[SQLAColumn](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md)的結果集中。 適用於 UDT 資料行或參數的 DATA_TYPE 為 SQL_SS_UDT。  
  
 對於參數的 UDT，如果伺服器傳回或要求此資訊，您可以使用以上定義的新驅動程式專用描述項來取得或設定 UDT 的額外中繼資料屬性。  
  
 當用戶端連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQLColumns 並調用 SQLColumns 時,使用目錄輸入參數的 NULL 或通配符值將不會從其他目錄中返回資訊。 系統只會傳回目前目錄的相關資訊。 用戶端可以首先調用 SQLTables 以確定所需表所在的目錄中。 然後,用戶端可以在對 SQLColumns 的調用中使用目錄輸入參數的目錄值來檢索有關該表中列的資訊。  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns 和資料表值參數  
 SQLColumns 返回的結果集取決於SQL_SOPT_SS_NAME_SCOPE設置。 有關詳細資訊,請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。 系統已針對資料表值參數加入下列資料行：  
  
|資料行名稱|資料類型|內容|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|對於 TABLE_TYPE 中的資料行，如果資料行為計算資料行，這是 SQL_TRUE，否則為 SQL_FALSE。|  
|SS_IS_IDENTITY|Smallint|如果資料行是識別資料行，則為 SQL_TRUE，否則為 SQL_FALSE。|  
  
 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLColumns 支援  
 關於日期/時間類型傳回的值的資訊,請參考[目錄中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 有關詳細資訊,請參閱[&#40;ODBC&#41;的日期和時間改進](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLColumns 支援  
 **SQLColumns**支援大型 CLR 用戶定義類型 (UDT)。 有關詳細資訊,請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>疏鬆資料行的 SQLColumns 支援  
 已[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將兩個特定列新增到 SQLColumns 的結果集中:  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**斯莫爾因特**|如果資料行為疏鬆資料行，這是 SQL_TRUE，否則為 SQL_FALSE。|  
|SS_IS_COLUMN_SET|**斯莫爾因特**|如果列是**column_set**列,則SQL_TRUE;否則,SQL_FALSE。|  
  
 與 ODBC 規範一致,SS_IS_SPARSE和SS_IS_COLUMN_SET出現在所有驅動程式特定的列之前,這些列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]添加到[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]版本早於之前,並在 ODBC 本身要求的所有列之後。  
  
 SQLColumns 返回的結果集取決於SQL_SOPT_SS_NAME_SCOPE設置。 有關詳細資訊,請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 有關 ODBC 中的稀疏列的詳細資訊,請參閱[稀疏列支援&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLColumns 函數](https://go.microsoft.com/fwlink/?LinkId=59336)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
