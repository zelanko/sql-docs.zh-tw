---
title: SQLDescribeParam |微軟文件
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
ms.openlocfilehash: efe1fdccbef4f5c4a393083f6eb81efee759be5c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302574"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  為了描述任何 SQL 語句的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]參數, 本機用戶端 ODBC 驅動程式在準備在 ODBC 語句句柄上調用 SQLDescribeParam 時產生並執行[!INCLUDE[tsql](../../includes/tsql-md.md)]SELECT 語句。 結果集的中繼資料則會決定已備妥之陳述式中的參數特性。 SQLDescribeParam 可以返回 SQLExecute 或 SQLExecDirect 可能返回的任何錯誤代碼。  
  
 資料庫引擎的改進從 SQLDescribeParam[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始 ,可以更精確地描述預期結果。 這些更準確的結果可能與 SQLDescribeParam 在 以前的版本中傳[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]回的值不同 。 如需詳細資訊，請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
 中[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]還新增了*參數SizePtr*現在返回一個值,該值與[ODBC 規範](https://go.microsoft.com/fwlink/?LinkId=207044)中定義的相應參數標記的列或表達式的大小(以字元)的定義一致。 在本機用戶端的早期版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中,*參數 SizePtr*可以是該類型的**SQL_DESC_OCTET_LENGTH**的相應值,也可以是提供給 SQLBindParameter 的類型的不相關的列大小值,該值應忽略該值(例如**SQL_INTEGER)。**  
  
 在以下情況下,驅動程式不支援呼叫 SQLDescribeParam:  
  
-   SQLExecDirect 後[!INCLUDE[tsql](../../includes/tsql-md.md)], 用於包含 FROM 子句的任何更新或刪除語句。  
  
-   針對在 HAVING 子句中包含參數或與 SUM 函數的結果相比較的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   針對相依於包含參數之子查詢的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   針對在比較 (like) 或定量述詞的運算式中都包含參數標記的 ODBC SQL 陳述式。  
  
-   針對其中一個參數為函數參數的任何查詢。  
  
-   當\*[!INCLUDE[tsql](../../includes/tsql-md.md)]命令中有註解 (/* /) 時。  
  
 處理一批[!INCLUDE[tsql](../../includes/tsql-md.md)]語句時,驅動程式也不支援在批處理中的第一個語句之後調用 SQLDescribeParam 作為語句中的參數標記。  
  
 在描述準備好的儲存過程的參數時,SQLDescribeParam 使用系統存儲過程[sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md)檢索參數特徵。 sp_sproc_columns可以報告當前用戶資料庫中存儲過程的數據。 準備完全限定的儲存過程名稱允許 SQLDescribeParam 跨資料庫執行。 例如,系統儲存過程[sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)可以在任何資料庫中準備和執行,如:  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 成功準備後執行 SQLDescribeParam 傳回空白列集,當連線到任何資料庫但**主**資料庫 。 相同的呼叫(如下)使 SQLDescribeParam 成功,而不考慮目前使用者資料庫:  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 對於較大的值數據類型 *,DataTypePtr*中返回的值SQL_VARCHAR、SQL_VARBINARY或SQL_NVARCHAR。 為了指示大值資料類型參數的大小為"無限制",[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式將*參數SizePtr*設置為 0。 為標準**varchar**參數返回實際大小值。  
  
> [!NOTE]  
>  如果參數已與 SQL_VARCHAR、SQL_VARBINARY 或 SQL_WVARCHAR 參數的最大大小繫結，則會傳回參數的繫結大小，而不是「無限制」。  
  
 若要繫結「無限制」大小輸入參數，則必須使用資料執行中 (data-at-execution)。 無法綁定「無限制」大小輸出參數(沒有從輸出參數流式傳輸數據的方法,就像[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)對結果集所做的那樣)。  
  
 對輸出參數而言，必須繫結緩衝區，而且如果值過大，則緩衝區會填滿，並且傳回 SQL_SUCCESS_WITH_INFO 訊息及「字串資料；右側截斷」警告。 之後會捨棄截斷的資料。  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam 和資料表值參數  
 應用程式可以使用 SQLDescribeParam 檢索已準備好語句的表值參數資訊。 有關詳細資訊,請參閱[已準備的語句的表值參數中繼資料](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)。  
  
 有關一般表值參數的詳細資訊,請參閱[&#40;ODBC &#40;的表值参数&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>SQLDescribeParam 對增強日期和時間功能的支援  
 針對日期/時間類型所傳回的值如下：  
  
||*資料類型Ptr*|*參數SizePtr*|*十進位數字Ptr*|  
|-|-------------------|------------------------|------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 有關詳細資訊,請參閱[&#40;ODBC&#41;的日期和時間改進](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLDescribeParam 支援  
 **SQLDescribeParam**支援大型 CLR 用戶定義類型 (UDT)。 有關詳細資訊,請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL描述參數函數](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
