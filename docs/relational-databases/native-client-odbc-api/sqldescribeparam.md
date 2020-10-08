---
description: SQLDescribeParam
title: SQLDescribeParam |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 20463fcf61f5d9842f4e5a84814970c57d4712f3
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809266"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  若要描述任何 SQL 語句的參數， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 當在備妥的 odbc 語句控制碼上呼叫 SQLDescribeParam 時，NATIVE Client ODBC 驅動程式會建立並執行 SELECT 語句。 結果集的中繼資料則會決定已備妥之陳述式中的參數特性。 SQLDescribeParam 可以傳回 SQLExecute 或 SQLExecDirect 可能傳回的任何錯誤碼。  
  
 資料庫引擎的增強功能從 [ [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 允許 SQLDescribeParam] 取得預期結果更精確的描述。 這些更精確的結果可能與舊版的 SQLDescribeParam 所傳回的值不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
 此外 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ， *ParameterSizePtr* 現在也會傳回一個值，這個值會與對應參數標記的資料行或運算式的大小（以字元為單位）的定義對齊，如 [ODBC 規格](../../odbc/reference/appendixes/column-size.md)中所定義。 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中， *ParameterSizePtr* 可以是類型的 **SQL_DESC_OCTET_LENGTH** 對應值，或是針對某個類型提供給 SQLBindParameter 的不相關資料行大小值， (**SQL_INTEGER**中應忽略此值，例如) 。  
  
 驅動程式在下列情況下不支援呼叫 SQLDescribeParam：  
  
-   在 SQLExecDirect [!INCLUDE[tsql](../../includes/tsql-md.md)] 包含 FROM 子句的任何 UPDATE 或 DELETE 子句之後。  
  
-   針對在 HAVING 子句中包含參數或與 SUM 函數的結果相比較的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   針對相依於包含參數之子查詢的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   針對在比較 (like) 或定量述詞的運算式中都包含參數標記的 ODBC SQL 陳述式。  
  
-   針對其中一個參數為函數參數的任何查詢。  
  
-   當命令中有批註 (/* \* /) 時 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 處理語句批次時 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，驅動程式也不支援在批次中的第一個語句之後，對語句中的參數標記呼叫 SQLDescribeParam。  
  
 在描述已備妥預存程式的參數時，SQLDescribeParam 會使用系統預存程式 [sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md) 來取出參數特性。 sp_sproc_columns 可以在目前的使用者資料庫中報告預存程式的資料。 準備完整的預存程式名稱，可讓 SQLDescribeParam 跨資料庫執行。 例如，您可以在任何資料庫中備妥和執行系統預存程式 [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) ，如下所示：  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 成功完成後執行 SQLDescribeParam 會傳回空的資料列集（連接到任何資料庫，但 **master**）。 無論目前的使用者資料庫為何，相同的呼叫（以下列方式備妥）都會使 SQLDescribeParam 成功：  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 若為大數值資料類型， *DataTypePtr* 中傳回的值為 SQL_VARCHAR、SQL_VARBINARY 或 SQL_NVARCHAR。 若要指出大數值資料類型參數的大小為「無限制」， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會將 *ParameterSizePtr* 設定為0。 標準 **Varchar** 參數會傳回實際的大小值。  
  
> [!NOTE]  
>  如果參數已與 SQL_VARCHAR、SQL_VARBINARY 或 SQL_WVARCHAR 參數的最大大小繫結，則會傳回參數的繫結大小，而不是「無限制」。  
  
 若要繫結「無限制」大小輸入參數，則必須使用資料執行中 (data-at-execution)。 您無法系結「無限制」大小的輸出參數， (沒有任何方法可從輸出參數串流資料，例如 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 對結果集) 。  
  
 對輸出參數而言，必須繫結緩衝區，而且如果值過大，則緩衝區會填滿，並且傳回 SQL_SUCCESS_WITH_INFO 訊息及「字串資料；右側截斷」警告。 之後會捨棄截斷的資料。  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam 和資料表值參數  
 應用程式可以使用 SQLDescribeParam 來取得備妥語句的資料表值參數資訊。 如需詳細資訊，請參閱備妥之 [語句的資料表值參數中繼資料](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)。  
  
 如需有關資料表值參數的一般詳細資訊，請參閱 [&#40;ODBC&#41;的資料表值參數 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>SQLDescribeParam 對增強日期和時間功能的支援  
 針對日期/時間類型所傳回的值如下：  
  
| 屬性 | *DataTypePtr* | *ParameterSizePtr* | *DecimalDigitsPtr* |  
| --------- | ------------- | ------------------ | ------------------ |  
|Datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 如需詳細資訊，請參閱 [&#40;ODBC&#41;的日期和時間改進 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLDescribeParam 支援  
 **SQLDescribeParam** 支援)  (udt 的大型 CLR 使用者自訂類型。 如需詳細資訊，請參閱 [&#40;ODBC&#41;的大型 CLR 使用者自訂類型 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLDescribeParam 函式](../../odbc/reference/syntax/sqldescribeparam-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
