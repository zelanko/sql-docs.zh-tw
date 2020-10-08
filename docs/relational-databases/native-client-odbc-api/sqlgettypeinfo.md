---
description: SQLGetTypeInfo
title: SQLGetTypeInfo |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 04647ba7d356b49b9967b5a84ebf15fb33072e0f
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810968"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會報告**SQLGetTypeInfo**結果集中的其他資料行 USERTYPE。 USERTYPE 會報告 DB-Library 資料類型定義，而且對於將現有 DB-Library 應用程式移植至 ODBC 的開發人員很有用。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將識別視為屬性，而 ODBC 則會將它視為資料類型。 若要解決這種不相符的情況， **SQLGetTypeInfo** 會傳回資料類型： **intidentity**、 **Smallintidentity**、 **Tinyintidentity**、 **decimalidentity**和 **numericidentity**。 **SQLGetTypeInfo**結果集資料行 AUTO_UNIQUE_VALUE 報告這些資料類型的值 TRUE。  
  
 若為 **Varchar**、 **Nvarchar** 和 **Varbinary**， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會繼續針對 COLUMN_SIZE 值分別報告8000、4000和8000，雖然它實際上是無限制的。 這為了確保回溯相容性。  
  
 若為 **xml** 資料類型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會報告 SQL_SS_LENGTH_UNLIMITED，COLUMN_SIZE 表示無限制的大小。  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo 和資料表值參數  
 資料表值參數的資料表類型實際上是中繼類型，也就是用來定義其他類型的類型。 因此，它不需要透過 SQLGetTypeInfo 來公開。 應用程式必須使用 SQLTables （而非 SQLGetTypeInfo）來取得與資料表值參數搭配使用之資料表類型的中繼資料。  
  
 如需有關為數據表值參數抓取中繼資料的詳細資訊，請參閱 [影響資料表值參數的語句屬性](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)。  
  
 如需資料表值參數的詳細資訊，請參閱 [&#40;ODBC&#41;的資料表值參數 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLGetTypeInfo 支援  
 如需日期/時間類型的傳回值，請參閱 [目錄中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 如需更多一般資訊，請參閱 [&#40;ODBC&#41;的日期和時間改進 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLGetTypeInfo 支援  
 **SQLGetTypeInfo** 支援)  (udt 的大型 CLR 使用者自訂類型。 如需詳細資訊，請參閱 [&#40;ODBC&#41;的大型 CLR 使用者自訂類型 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetTypeInfo 函式](../../odbc/reference/syntax/sqlgettypeinfo-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
