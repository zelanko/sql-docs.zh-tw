---
title: 直接執行語句（ODBC） |Microsoft Docs
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
ms.openlocfilehash: 10ee03c1c127abae0d79cb1244f4991e68dd7ca1
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009469"
---
# <a name="execute-a-statement-directly-odbc"></a>直接執行陳述式 (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-execute-a-statement-directly-and-one-time-only"></a>直接並且僅一次執行陳述式  
  
1.  如果語句具有參數標記，請使用[SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)將每個參數系結至程式變數。 使用資料值填入程式變數，然後設定任何資料執行中 (data-at-execution) 參數。  
  
2.  呼叫[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)以執行語句。  
  
3.  如果使用了資料執行中輸入參數， [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)會傳回 SQL_NEED_DATA。 使用[SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405)和[SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md)以區區塊轉送資料。  

### <a name="to-execute-a-statement-multiple-times-by-using-column-wise-parameter-binding"></a>使用資料行取向的參數繫結多次執行陳述式  
  
1.  呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)以設定下列屬性：  
  
     將 SQL_ATTR_PARAMSET_SIZE 設定為參數集 (S) 的數目。  
  
     將 SQL_ATTR_PARAM_BIND_TYPE 設定為 SQL_PARAMETER_BIND_BY_COLUMN。  
  
     將 SQL_ATTR_PARAMS_PROCESSED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存已處理的參數數目。  
  
     將 SQL_ATTR_PARAMS_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[S]，以保存參數狀態指標。  
  
2.  針對每個參數標記：  
  
     配置 S 個參數緩衝區的陣列來儲存資料值。  
  
     配置 S 個參數緩衝區的陣列來儲存資料長度。  
  
     呼叫[SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) ，將參數資料值和資料長度陣列系結至語句參數。  
  
     設定任何資料執行中的 text 或 image 參數。  
  
     將 S 資料值和 S 資料長度放在繫結參數陣列中。  
  
3.  呼叫[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)以執行語句。 驅動程式會有效率地執行陳述式 S 次，針對每個參數集執行一次。  
  
4.  如果使用了資料執行中輸入參數， [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)會傳回 SQL_NEED_DATA。 使用[SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405)和[SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md)以區區塊轉送資料。  
  
### <a name="to-execute-a-statement-multiple-times-by-using-row-wise-parameter-binding"></a>使用資料列取向的參數繫結多次執行陳述式  
  
1.  配置結構的陣列[S]，其中 S 是參數集的數目。 結構中每個參數都具有一個元素，而每個元素則具有兩部分：  
  
     第一個部分是適當資料類型的變數，可保存參數資料。  
  
     第二個部分是 SQLINTEGER 變數，可保存狀態指標。  
  
2.  呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)以設定下列屬性：  
  
     將 SQL_ATTR_PARAMSET_SIZE 設定為參數集 (S) 的數目。  
  
     將 SQL_ATTR_PARAM_BIND_TYPE 設定為步驟 1 中配置的結構大小。  
  
     將 SQL_ATTR_PARAMS_PROCESSED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存已處理的參數數目。  
  
     將 SQL_ATTR_PARAMS_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[S]，以保存參數狀態指標。  
  
3.  針對每個參數標記，呼叫[SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) ，將參數的資料值和資料長度指標指向其在步驟1所配置之結構陣列第一個元素中的變數。 如果參數是資料執行中參數，請設定此參數。  
  
4.  將資料值填入繫結參數緩衝區陣列。  
  
5.  呼叫[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)以執行語句。 驅動程式會有效率地執行陳述式 S 次，針對每個參數集執行一次。  
  
6.  如果使用了資料執行中輸入參數， [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)會傳回 SQL_NEED_DATA。 使用[SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405)和[SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md)以區區塊轉送資料。  
  
 **注意**資料行取向和資料列取向的系結通常會與[SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360)函式和[SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400)搭配使用，而不是[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)。  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢 &#40;ODBC&#41;的使用說明主題](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
