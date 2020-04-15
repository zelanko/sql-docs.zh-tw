---
title: SQL程式列 |微軟文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedureColumns function
ms.assetid: 6671e180-0072-4de5-90f5-314306d2ba9c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b942126a5ad73d5c41f28f60a63d22ef8584f24
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279991"
---
# <a name="sqlprocedurecolumns"></a>SQLProcedureColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLProcessColumns**傳回一行,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]報告所有儲存過程的返回值屬性。  
  
 **SQL程式列**傳回SQL_SUCCESS*目錄名稱*、*架構名稱**、ProcName*參數或*列名*參數是否存在值。 當在這些參數中使用無效值時 **,SQLFetch**將返回SQL_NO_DATA。  
  
 **SQL程式列**可以在靜態伺服器游標上執行。 嘗試在可上升(動態或鍵集)游標上執行**SQLARK**鍵將返回SQL_SUCCESS_WITH_INFO指示游標類型已更改。  
  
 下表列出了結果集傳回的欄,以及如何擴充它們,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以便透過 本機客戶端 ODBC 驅動程式處理**udt**和**xml**資料類型:  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|SS_UDT_CATALOG_NAME|傳回包含 UDT (使用者定義型別) 之目錄的名稱。|  
|SS_UDT_SCHEMA_NAME|傳回包含 UDT 之結構描述的名稱。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|傳回 UDT 的組件完整名稱。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|傳回定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|傳回定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，則此變數包含空字串。|  
|SS_XML_SCHEMACOLLECTION_NAME|傳回 XML 結構描述集合的名稱。 如果找不到名稱，則此變數包含空字串。|  
  
## <a name="sqlprocedurecolumns-and-table-valued-parameters"></a>SQLProcedureColumns 和資料表值參數  
 SQL程式列以類似於 CLR 使用者定義的類型的方式處理表值參數。 在針對資料表值參數傳回的資料列中，資料行包含下列值：  
  
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
  
 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlprocedurecolumns-support-for-enhanced-date-and-time-features"></a>SQLProcedureColumns 對增強日期和時間功能的支援  
 關於日期/時間類型傳回的值,請參考[目錄中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 有關更一般的資訊,請參閱[ODBC&#41;&#40;日期和時間改進](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlprocedurecolumns-support-for-large-clr-udts"></a>SQLProcedureColumns 對大型 CLR UDT 的支援  
 **SQL程式列**支援大型 CLR 使用者定義類型 (UDT)。 有關詳細資訊,請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 程式列函數](https://go.microsoft.com/fwlink/?LinkId=59363)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
