---
title: SQLDescribeCol |微軟文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e0e9a03b2e8635618afbdc615a6f77dfe05c533e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302573"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  對於已執行的語句[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],本機用戶端 ODBC 驅動程式不需要查詢伺服器來描述結果集中的列。 在這種情況下 **,SQLDescribeCol**不會導致伺服器往返。 與[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)和[SQLNumResultCols 一](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)樣,在準備好但未執行語句時調用**SQLCol**會生成伺服器往返。  
  
 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或陳述式批次傳回多個結果資料列集時，按序數參考的資料行有可能源自於個別的資料表，或是參考結果集中完全不同的資料行。 應為每個集調用**SQLDescribeCol。** 當結果集變更時，應用程式應該在提取資料列結果以前先重新繫結資料值。 有關處理多個結果集傳回的詳細資訊,請參閱[SQLMore 結果](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 當已備妥的 SQL 陳述式批次產生多個結果集時，只有第一個結果集會報告資料行屬性。  
  
 對於較大的值數據類型 *,DataTypePtr*中返回的值SQL_VARCHAR、SQL_VARBINARY或SQL_NVARCHAR。 *列SizePtr*中的SQL_SS_LENGTH_UNLIMITED值表示大小為"無限制"。  
  
 資料庫引擎的改進從 SQLDescribeCol[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始 ,可以獲得對預期結果的更準確描述。 這些更準確的結果可能與 SQLDescribeCol 在 以前的版本中傳[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]回的值不同 。 如需詳細資訊，請參閱[中繼資料探索](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>SQLDescribeCol 對增強型日期和時間功能的支援  
 針對日期/時間類型所傳回的值如下：  
  
||*資料類型Ptr*|*欄大小器*|*十進位數字Ptr*|  
|-|-------------------|---------------------|------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 有關詳細資訊,請參閱[&#40;ODBC&#41;的日期和時間改進](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>SQLDescribeCol 對於大型 CLR UDT 的支援  
 **SQLDescribeCol**支援大型 CLR 用戶定義類型 (UDT)。 有關詳細資訊,請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL描述科爾函數](https://go.microsoft.com/fwlink/?LinkID=59338)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
