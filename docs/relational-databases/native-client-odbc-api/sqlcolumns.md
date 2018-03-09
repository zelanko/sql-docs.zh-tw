---
title: SQLColumns | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
caps.latest.revision: "62"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 661c678e8d98d1b4d3f88c29d6d0b786b4e686d4
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLColumns**是否存在的值都會傳回 SQL_SUCCESS *CatalogName*， *TableName*，或*ColumnName*參數。 **SQLFetch**這些參數中使用無效值時，傳回 sql_no_data 為止。  
  
> [!NOTE]  
>  若是大數值類型，將會傳回包含 SQL_SS_LENGTH_UNLIMITED 值的所有長度參數。  
  
 **SQLColumns**可以在靜態伺服器資料指標上執行。 嘗試執行**SQLColumns**上可更新的 （動態或索引鍵集） 資料指標會傳回 SQL_SUCCESS_WITH_INFO，指出資料指標類型已變更。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援的報告資訊連結的伺服器上的資料表所接受的兩段式名稱*CatalogName*參數： *Linked_Server_Name.Catalog_Name*.  
  
 ODBC 2。*x*應用程式中不使用萬用字元*TableName*， **SQLColumns**傳回資料表的名稱相符的任何相關資訊*TableName*和目前使用者所擁有。 如果目前使用者擁有其名稱符合任何資料表*TableName*參數， **SQLColumns**傳回其他使用者所擁有的任何資料表的相關資訊，其中資料表名稱必須符合*TableName*參數。 ODBC 2。*x*應用程式使用萬用字元， **SQLColumns**傳回所有資料表其名稱符合*TableName*。 ODBC 3。*x*應用程式**SQLColumns**傳回所有資料表其名稱符合*TableName*不論擁有者或是否使用萬用字元。  
  
 下表列出結果集傳回的資料行：  
  
|資料行名稱|Description|  
|-----------------|-----------------|  
|DATA_TYPE|傳回 SQL_VARCHAR、 SQL_VARBINARY 或 SQL_WVARCHAR 如**varchar （max)**資料型別。|  
|TYPE_NAME|傳回"varchar"、"varbinary"或"nvarchar" **varchar （max)**， **varbinary （max)**，和**nvarchar （max)**資料型別。|  
|COLUMN_SIZE|傳回為 SQL_SS_LENGTH_UNLIMITED **varchar （max)**資料類型表示資料行的大小沒有限制。|  
|BUFFER_LENGTH|傳回為 SQL_SS_LENGTH_UNLIMITED **varchar （max)**資料類型表示的緩衝區大小沒有限制。|  
|SQL_DATA_TYPE|傳回 SQL_VARCHAR、 SQL_VARBINARY 或 SQL_WVARCHAR 如**varchar （max)**資料型別。|  
|CHAR_OCTET_LENGTH|傳回 char 或 binary 資料行的最大長度。 傳回 0 表示大小不受限制。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|傳回定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|傳回定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_NAME|傳回 XML 結構描述集合的名稱。 如果找不到名稱，則此變數包含空字串。|  
|SS_UDT_CATALOG_NAME|包含 UDT (使用者定義型別) 之目錄的名稱。|  
|SS_UDT_SCHEMA_NAME|包含 UDT 之結構描述的名稱。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|UDT 的組件完整名稱。|  
  
 對於 Udt，現有的 TYPE_NAME 資料行用於表示 UDT; 的名稱因此，沒有其他資料行應該加入的結果集**SQLColumns**或[SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md)。 適用於 UDT 資料行或參數的 DATA_TYPE 為 SQL_SS_UDT。  
  
 對於參數的 UDT，如果伺服器傳回或要求此資訊，您可以使用以上定義的新驅動程式專用描述項來取得或設定 UDT 的額外中繼資料屬性。  
  
 當用戶端連線至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]呼叫 SQLColumns、 為目錄輸入的參數不會從其他目錄傳回資訊，請使用 NULL 或萬用字元值。 系統只會傳回目前目錄的相關資訊。 用戶端第一次可以呼叫以判斷哪一個類別目錄中所需的資料表所在的 SQLTables。 用戶端可以然後使用該類別目錄值用於目錄輸入參數的呼叫 SQLColumns 中擷取該資料表中的資料行的相關資訊。  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns 和資料表值參數  
 SQLColumns 所傳回的結果集取決於 SQL_SOPT_SS_NAME_SCOPE 的設定。 如需詳細資訊，請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。 系統已針對資料表值參數加入下列資料行：  
  
|資料行名稱|資料類型|目錄|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|對於 TABLE_TYPE 中的資料行，如果資料行為計算資料行，這是 SQL_TRUE，否則為 SQL_FALSE。|  
|SS_IS_IDENTITY|Smallint|如果資料行是識別資料行，則為 SQL_TRUE，否則為 SQL_FALSE。|  
  
 如需有關資料表值參數的詳細資訊，請參閱[資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLColumns 支援  
 傳回日期/時間類型之值的相關資訊，請參閱[目錄中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 如需詳細資訊，請參閱[日期和時間增強功能 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLColumns 支援  
 **SQLColumns**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱[Large CLR User-Defined 類型 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>疏鬆資料行的 SQLColumns 支援  
 兩個[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]特定資料行已加入到結果集的 SQLColumns:  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**Smallint**|如果資料行為疏鬆資料行，這是 SQL_TRUE，否則為 SQL_FALSE。|  
|SS_IS_COLUMN_SET|**Smallint**|如果資料行是**column_set**資料行，這是 SQL_TRUE，否則 SQL_FALSE。|  
  
 依照 ODBC 規格，SS_IS_SPARSE 和 SS_IS_COLUMN_SET 會出現所有的驅動程式專用資料行已加入至之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本早於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，以及 ODBC 本身所託管的所有資料行之後。  
  
 SQLColumns 所傳回的結果集取決於 SQL_SOPT_SS_NAME_SCOPE 的設定。 如需詳細資訊，請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 如需有關 ODBC 中的疏鬆資料行的詳細資訊，請參閱[疏鬆資料行支援 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLColumns 函數](http://go.microsoft.com/fwlink/?LinkId=59336)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
