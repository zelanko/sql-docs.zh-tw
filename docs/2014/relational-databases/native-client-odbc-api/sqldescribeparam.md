---
title: SQLDescribeParam |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d52d68cc0cd31e9dbb3da25c46901e126252607
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067723"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
  為了描述任何 SQL 語句的參數， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會在備妥的[!INCLUDE[tsql](../../includes/tsql-md.md)] ODBC 語句控制碼上呼叫 SQLDescribeParam 時，建立並執行 SELECT 語句。 結果集的中繼資料則會決定已備妥之陳述式中的參數特性。 SQLDescribeParam 可能會傳回 SQLExecute 或 SQLExecDirect 可能傳回的任何錯誤碼。  
  
 從開始，database engine 的改進[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]可讓 SQLDescribeParam 取得預期結果的更精確描述。 這些更精確的結果可能與舊版的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQLDescribeParam 所傳回的值不同。 如需詳細資訊，請參閱[中繼資料探索](../native-client/features/metadata-discovery.md)。  
  
 此外[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]， *ParameterSizePtr*現在也會傳回一個值，以與[ODBC 規格](https://go.microsoft.com/fwlink/?LinkId=207044)中所定義之對應參數標記的資料行或運算式大小（以字元為單位）的定義對齊。 在舊版的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中， *ParameterSizePtr*可以是類型的對應值`SQL_DESC_OCTET_LENGTH` ，或是針對類型提供給 SQLBindParameter 的不相關資料行大小值，應該忽略的值（`SQL_INTEGER`例如）。  
  
 在下列情況下，驅動程式不支援呼叫 SQLDescribeParam：  
  
-   在 SQLExecDirect 包含 FROM [!INCLUDE[tsql](../../includes/tsql-md.md)]子句的任何 UPDATE 或 DELETE 子句之後。  
  
-   針對在 HAVING 子句中包含參數或與 SUM 函數的結果相比較的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   針對相依於包含參數之子查詢的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   針對在比較 (like) 或定量述詞的運算式中都包含參數標記的 ODBC SQL 陳述式。  
  
-   針對其中一個參數為函數參數的任何查詢。  
  
-   當[!INCLUDE[tsql](../../includes/tsql-md.md)]命令中有批註（/ \**/）時。  
  
 在處理[!INCLUDE[tsql](../../includes/tsql-md.md)]語句批次時，驅動程式也不支援在批次中的第一個語句之後，針對語句中的參數標記呼叫 SQLDescribeParam。  
  
 在描述已備妥預存程式的參數時，SQLDescribeParam 會使用系統預存程式[sp_sproc_columns](/sql/relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql)來取得參數特性。 sp_sproc_columns 可以報告目前使用者資料庫內預存程式的資料。 準備完整的預存程式名稱，可讓 SQLDescribeParam 跨資料庫執行。 例如，您可以在任何資料庫中準備和執行系統預存程式[sp_who](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) ，如下所示：  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 當成功準備之後執行 SQLDescribeParam 時，會在連接到任何資料庫時， `master`傳回空的資料列集，但是。 無論目前的使用者資料庫為何，相同的呼叫（依照下列方式準備）都會導致 SQLDescribeParam 成功：  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 對於大數值資料類型，在*DataTypePtr*中傳回的值是 SQL_VARCHAR、SQL_VARBINARY 或 SQL_NVARCHAR。 若要指出大數值資料類型參數的大小為「無限制」， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會將*ParameterSizePtr*設定為0。 實際大小值則會以標準 `varchar` 參數傳回。  
  
> [!NOTE]  
>  如果參數已與 SQL_VARCHAR、SQL_VARBINARY 或 SQL_WVARCHAR 參數的最大大小繫結，則會傳回參數的繫結大小，而不是「無限制」。  
  
 若要繫結「無限制」大小輸入參數，則必須使用資料執行中 (data-at-execution)。 您無法系結「無限制」大小的輸出參數（沒有任何方法可從輸出參數串流資料，例如[SQLGetData](sqlgetdata.md)適用于結果集）。  
  
 對輸出參數而言，必須繫結緩衝區，而且如果值過大，則緩衝區會填滿，並且傳回 SQL_SUCCESS_WITH_INFO 訊息及「字串資料；右側截斷」警告。 之後會捨棄截斷的資料。  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam 和資料表值參數  
 應用程式可以使用 SQLDescribeParam 來抓取備妥之語句的資料表值參數資訊。 如需詳細資訊，請參閱備妥之[語句的資料表值參數中繼資料](../native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)。  
  
 如需有關資料表值參數的一般詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>SQLDescribeParam 對增強日期和時間功能的支援  
 針對日期/時間類型所傳回的值如下：  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLDescribeParam 支援  
 
  `SQLDescribeParam` 支援大型 CLR 使用者定義型別 (UDT)。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLDescribeParam 函式](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
