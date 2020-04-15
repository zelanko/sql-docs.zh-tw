---
title: 直接執行敘述 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statement execution
ms.assetid: b690f9de-66e1-4ee5-ab6a-121346fb5f85
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a4516f25ee6d18ddb56bedab1e55a2924c03873
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294162"
---
# <a name="execute-a-statement-directly-odbc"></a>直接執行陳述式 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-execute-a-statement-directly-and-one-time-only"></a>直接並且僅一次執行陳述式  
  
1.  如果語句具有參數標記,請使用[SQLBind 參數](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)將每個參數綁定到程式變數。 使用資料值填入程式變數，然後設定任何資料執行中 (data-at-execution) 參數。  
  
2.  調用[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)以執行該語句。  
  
3.  如果使用執行時的數據輸入參數[,SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)將返回SQL_NEED_DATA。 使用[SQLParam 資料和](https://go.microsoft.com/fwlink/?LinkId=58405) [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md)以區塊發送數據。  

### <a name="to-execute-a-statement-multiple-times-by-using-column-wise-parameter-binding"></a>使用資料行取向的參數繫結多次執行陳述式  
  
1.  呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)來設定以下屬性:  
  
     將 SQL_ATTR_PARAMSET_SIZE 設定為參數集 (S) 的數目。  
  
     將 SQL_ATTR_PARAM_BIND_TYPE 設定為 SQL_PARAMETER_BIND_BY_COLUMN。  
  
     將 SQL_ATTR_PARAMS_PROCESSED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存已處理的參數數目。  
  
     將 SQL_ATTR_PARAMS_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[S]，以保存參數狀態指標。  
  
2.  針對每個參數標記：  
  
     配置 S 個參數緩衝區的陣列來儲存資料值。  
  
     配置 S 個參數緩衝區的陣列來儲存資料長度。  
  
     呼叫[SQLBind 參數](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)將參數資料值和資料長度陣列結合到語句參數。  
  
     設定任何資料執行中的 text 或 image 參數。  
  
     將 S 資料值和 S 資料長度放在繫結參數陣列中。  
  
3.  調用[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)以執行該語句。 驅動程式會有效率地執行陳述式 S 次，針對每個參數集執行一次。  
  
4.  如果使用執行時的數據輸入參數[,SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)將返回SQL_NEED_DATA。 使用[SQLParam 資料和](https://go.microsoft.com/fwlink/?LinkId=58405) [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md)以區塊發送數據。  
  
### <a name="to-execute-a-statement-multiple-times-by-using-row-wise-parameter-binding"></a>使用資料列取向的參數繫結多次執行陳述式  
  
1.  配置結構的陣列[S]，其中 S 是參數集的數目。 結構中每個參數都具有一個元素，而每個元素則具有兩部分：  
  
     第一個部分是適當資料類型的變數，可保存參數資料。  
  
     第二個部分是 SQLINTEGER 變數，可保存狀態指標。  
  
2.  呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)來設定以下屬性:  
  
     將 SQL_ATTR_PARAMSET_SIZE 設定為參數集 (S) 的數目。  
  
     將 SQL_ATTR_PARAM_BIND_TYPE 設定為步驟 1 中配置的結構大小。  
  
     將 SQL_ATTR_PARAMS_PROCESSED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存已處理的參數數目。  
  
     將 SQL_ATTR_PARAMS_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[S]，以保存參數狀態指標。  
  
3.  對於每個參數標記,調用[SQLBindparameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)以將參數的數據值和數據長度指標指向步驟 1 中分配的結構陣列的第一個元素中的變數。 如果參數是資料執行中參數，請設定此參數。  
  
4.  將資料值填入繫結參數緩衝區陣列。  
  
5.  調用[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)以執行該語句。 驅動程式會有效率地執行陳述式 S 次，針對每個參數集執行一次。  
  
6.  如果使用執行時的數據輸入參數[,SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)將返回SQL_NEED_DATA。 使用[SQLParam 資料和](https://go.microsoft.com/fwlink/?LinkId=58405) [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md)以區塊發送數據。  
  
 **注意**依列繫結與行綁定更通常與[SQLPrepare 函數](https://go.microsoft.com/fwlink/?LinkId=59360)與[SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400)結合使用,而不是[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)。  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢「如何」主題&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
