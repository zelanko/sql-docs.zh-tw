---
title: SQLProcedureColumns |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedureColumns function
ms.assetid: 6671e180-0072-4de5-90f5-314306d2ba9c
author: rothja
ms.author: jroth
ms.openlocfilehash: 078e391bd39fdc49cde539c4004ed51d25eef93f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021920"
---
# <a name="sqlprocedurecolumns"></a>SQLProcedureColumns
  `SQLProcedureColumns`傳回一個資料列，報告所有預存程式的傳回值屬性 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 `SQLProcedureColumns`傳回 SQL_SUCCESS *CatalogName*、 *SchemaName*、 *ProcName*或*ColumnName*參數值是否存在。 當這些參數中使用了不正確值時， **SQLFetch**會傳回 SQL_NO_DATA。  
  
 `SQLProcedureColumns` 可以在靜態伺服器資料指標上執行。 嘗試在可更新的 (動態或索引鍵集) 資料指標上執行 `SQLProcedureColumns` 時，將會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已變更。  
  
 下表列出結果集所傳回的資料行，以及如何透過 Native Client ODBC 驅動程式擴充以處理**udt**和**xml**資料類型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|SS_UDT_CATALOG_NAME|傳回包含 UDT (使用者定義型別) 之目錄的名稱。|  
|SS_UDT_SCHEMA_NAME|傳回包含 UDT 之結構描述的名稱。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|傳回 UDT 的組件完整名稱。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|傳回定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|傳回定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_NAME|傳回 XML 結構描述集合的名稱。 如果找不到名稱，則此變數包含空字串。|  
  
## <a name="sqlprocedurecolumns-and-table-valued-parameters"></a>SQLProcedureColumns 和資料表值參數  
 SQLProcedureColumns 會以類似 CLR 使用者自訂類型的方式來處理資料表值參數。 在針對資料表值參數傳回的資料列中，資料行包含下列值：  
  
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
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlprocedurecolumns-support-for-enhanced-date-and-time-features"></a>SQLProcedureColumns 對增強日期和時間功能的支援  
 如需日期/時間類型傳回的值，請參閱[目錄中繼資料](../native-client-odbc-date-time/metadata-catalog.md)。  
  
 如需更多一般資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlprocedurecolumns-support-for-large-clr-udts"></a>SQLProcedureColumns 對大型 CLR UDT 的支援  
 `SQLProcedureColumns` 支援大型 CLR 使用者定義型別 (UDT)。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLProcedureColumns 函式](https://go.microsoft.com/fwlink/?LinkId=59363)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
