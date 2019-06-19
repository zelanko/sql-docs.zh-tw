---
title: SQLDescribeParam | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d72636f31a41f2b1d8ca7019d1a7e32f1b95ad51
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63015150"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  若要描述的任何 SQL 陳述式中，參數[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會建置並執行[!INCLUDE[tsql](../../includes/tsql-md.md)]SQLDescribeParam 備妥的 ODBC 陳述式控制代碼上呼叫時，SELECT 陳述式。 結果集的中繼資料則會決定已備妥之陳述式中的參數特性。 SQLDescribeParam 可以傳回 SQLExecute 或 SQLExecDirect 可能會傳回任何錯誤程式碼。  
  
 在開始 database engine 的改進[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允許 SQLDescribeParam 以取得更精確的預期結果的描述。 這些更精確的結果可能不同於在舊版的 SQLDescribeParam 傳回的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
 新功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]， *ParameterSizePtr*現在傳回值，這個值會配合中所定義的大小，以字元為單位的資料行或運算式的對應參數標記定義[ODBC規格](https://go.microsoft.com/fwlink/?LinkId=207044)。 在舊版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端*ParameterSizePtr*可能的對應值**SQL_DESC_OCTET_LENGTH**類型，或已提供不相關的資料行大小值以 SQLBindParameter 類型，應該忽略其值 (**SQL_INTEGER**，例如)。  
  
 在下列情況下，驅動程式不支援呼叫 SQLDescribeParam:  
  
-   之後的任何 SQLExecDirect[!INCLUDE[tsql](../../includes/tsql-md.md)]包含 FROM 子句的 UPDATE 或 DELETE 陳述式。  
  
-   針對在 HAVING 子句中包含參數或與 SUM 函數的結果相比較的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   針對相依於包含參數之子查詢的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   針對在比較 (like) 或定量述詞的運算式中都包含參數標記的 ODBC SQL 陳述式。  
  
-   針對其中一個參數為函數參數的任何查詢。  
  
-   當有註解 (/ * \*/) 在[!INCLUDE[tsql](../../includes/tsql-md.md)]命令。  
  
 處理的批次時[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式，此驅動程式也不支援陳述式中的參數標記呼叫 SQLDescribeParam，批次中的第一個陳述式之後。  
  
 SQLDescribeParam 時描述參數的備妥預存程序，使用系統預存程序[sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md)來擷取參數特性。 sp_sproc_columns 可以報告在目前的使用者資料庫中的預存程序的資料。 準備完整的預存程序名稱，可讓 SQLDescribeParam 跨資料庫執行。 比方說，系統預存程序[sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)備妥並做為任何資料庫中執行：  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 執行 SQLDescribeParam 成功準備傳回空的資料列時連接到任何資料庫設定之後，但**主要**。 相同的呼叫，備妥，如下所示，會導致 SQLDescribeParam 才會成功，不論目前的使用者資料庫：  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 大數值資料類型，傳回的值在*DataTypePtr*為 SQL_VARCHAR、 SQL_VARBINARY 或 SQL_NVARCHAR。 若要表示大數值資料型別參數的大小是 「 無限制 」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式集*ParameterSizePtr*設為 0。 實際大小值會傳回標準**varchar**參數。  
  
> [!NOTE]  
>  如果參數已與 SQL_VARCHAR、SQL_VARBINARY 或 SQL_WVARCHAR 參數的最大大小繫結，則會傳回參數的繫結大小，而不是「無限制」。  
  
 若要繫結「無限制」大小輸入參數，則必須使用資料執行中 (data-at-execution)。 不可能繫結 「 無限制 」 大小輸出參數 (例如串流資料從一個 output 參數，沒有方法[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)對結果集)。  
  
 對輸出參數而言，必須繫結緩衝區，而且如果值過大，則緩衝區會填滿，並且傳回 SQL_SUCCESS_WITH_INFO 訊息及「字串資料；右側截斷」警告。 之後會捨棄截斷的資料。  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam 和資料表值參數  
 應用程式可以擷取 SQLDescribeParam 的已備妥之陳述式資料表值參數資訊。 如需詳細資訊，請參閱 <<c0> [ 備妥的陳述式資料表值參數中繼資料](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)。  
  
 如需有關資料表值參數在一般情況下，請參閱[Parameters &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>SQLDescribeParam 對增強日期和時間功能的支援  
 針對日期/時間類型所傳回的值如下：  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|日期|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 如需詳細資訊，請參閱 <<c0> [ 日期和時間改善&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。</c0>  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLDescribeParam 支援  
 **SQLDescribeParam**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱 < [Large CLR User-Defined 類型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLDescribeParam 函數](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
