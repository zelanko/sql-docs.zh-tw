---
title: SQLProcedureColumns |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedureColumns function
ms.assetid: 6671e180-0072-4de5-90f5-314306d2ba9c
caps.latest.revision: 50
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 75acfcf2d519db920b7fa7f9b4b3115ea4f8c981
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35700699"
---
# <a name="sqlprocedurecolumns"></a>SQLProcedureColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLProcedureColumns**傳回一個資料列，報告所有的傳回值屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預存程序。  
  
 **SQLProcedureColumns**是否存在的值都會傳回 SQL_SUCCESS *CatalogName*， *SchemaName*， *ProcName*，或*ColumnName*參數。 **SQLFetch**這些參數中使用無效值時，傳回 sql_no_data 為止。  
  
 **SQLProcedureColumns**可以在靜態伺服器資料指標上執行。 嘗試執行**SQLProcedureColumns**上可更新的 （動態或索引鍵集） 資料指標會傳回 SQL_SUCCESS_WITH_INFO，指出資料指標類型已變更。  
  
 下表列出結果集，以及如何擴充這些處理傳回的資料行**udt**和**xml**資料型別透過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式：  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|SS_UDT_CATALOG_NAME|傳回包含 UDT (使用者定義型別) 之目錄的名稱。|  
|SS_UDT_SCHEMA_NAME|傳回包含 UDT 之結構描述的名稱。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|傳回 UDT 的組件完整名稱。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|傳回定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|傳回定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_NAME|傳回 XML 結構描述集合的名稱。 如果找不到名稱，則此變數包含空字串。|  
  
## <a name="sqlprocedurecolumns-and-table-valued-parameters"></a>SQLProcedureColumns 和資料表值參數  
 SQLProcedureColumns 處理資料表值參數的方式，類似於 CLR 使用者定義型別。 在針對資料表值參數傳回的資料列中，資料行包含下列值：  
  
|資料行名稱|描述/值|  
|-----------------|------------------------|  
|DATA_TYPE|SQL_SS_TABLE|  
|TYPE_NAME|資料表值參數的資料表類型名稱。|  
|COLUMN_SIZE|NULL|  
|BUFFER_LENGTH|0|  
|DECIMAL_DIGITS|資料表值參數中，資料行的計數。|  
|NUM_PREC_RADIX|NULL|  
|NULLABLE|SQL_NULLABLE|  
|REMARKS|NULL|  
|COLUMN_DEF|NULL。 資料表類型可能沒有預設值。|  
|SQL_DATA_TYPE|SQL_SS_TABLE|  
|SQL_DATEIME_SUB|NULL|  
|CHAR_OCTET_LENGTH|NULL|  
|IS_NULLABLE|"YES"|  
|SS_TYPE_CATALOG_NAME|傳回包含資料表或 CLR 使用者定義型別之目錄的名稱。|  
|SS_TYPE_SCHEMA_NAME|傳回包含資料表或 CLR 使用者定義型別之結構描述的名稱。|  
  
 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 資料行會在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中提供，以便針對資料表值參數個別傳回目錄與結構描述。 這些資料行會針對資料表值參數及 CLR 使用者定義型別參數擴展  (CLR 使用者定義型別參數的現有結構描述與目錄不會受到這個額外功能的影響。 系統也會擴展它們來維護回溯相容性)。  
  
 依照 ODBC 規格規定，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 會出現在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所加入的所有驅動程式專用資料行之前，以及 ODBC 本身所託管的所有資料行之後。  
  
 如需有關資料表值參數的詳細資訊，請參閱[資料表值參數&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlprocedurecolumns-support-for-enhanced-date-and-time-features"></a>SQLProcedureColumns 對增強日期和時間功能的支援  
 針對日期/時間類型傳回的值，請參閱[目錄中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 如需詳細資訊，請參閱[日期和時間增強功能&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlprocedurecolumns-support-for-large-clr-udts"></a>SQLProcedureColumns 對大型 CLR UDT 的支援  
 **SQLProcedureColumns**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱[Large CLR User-Defined 類型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLProcedureColumns 函數](http://go.microsoft.com/fwlink/?LinkId=59363)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
