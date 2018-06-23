---
title: 準備及執行陳述式 (ODBC) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- statement execution
- statement preparation
ms.assetid: 0adecc63-4da5-486c-bc48-09a004a2fae6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a6d78ab8bbd48035795f8860cb02a20e83780289
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35701419"
---
# <a name="prepare-and-execute-a-statement-odbc"></a>準備和執行陳述式 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-prepare-a-statement-once-and-then-execute-it-multiple-times"></a>準備一次陳述式，然後執行多次  
  
1.  呼叫[SQLPrepare 函數](http://go.microsoft.com/fwlink/?LinkId=59360)準備陳述式。  
  
2.  （選擇性） 呼叫[SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404)來判斷已備妥的陳述式中的參數數目。  
  
3.  (選擇性) 針對準備陳述式中的每個參數：  
  
    -   呼叫[SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md)以便取得參數資訊。  
  
    -   將每個參數繫結至程式變數使用[SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md)。 設定任何資料執行中參數。  
  
4.  針對準備陳述式的每個執行：  
  
    -   如果陳述式具有參數標記，請將資料值放在繫結參數緩衝區中。  
  
    -   呼叫[SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400)執行備妥的陳述式。  
  
    -   如果資料在執行中輸入的參數使用， [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400)傳回 SQL_NEED_DATA。 按照區塊傳送資料，使用[SQLParamData](http://go.microsoft.com/fwlink/?LinkId=58405)和[SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md)。  
  
### <a name="to-prepare-a-statement-with-column-wise-parameter-binding"></a>準備含有資料行取向參數繫結的陳述式  
  
1.  呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)來設定下列屬性：  
  
    -   將 SQL_ATTR_PARAMSET_SIZE 設定為參數集 (S) 的數目。  
  
    -   將 SQL_ATTR_PARAM_BIND_TYPE 設定為 SQL_PARAMETER_BIND_BY_COLUMN。  
  
    -   將 SQL_ATTR_PARAMS_PROCESSED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存已處理的參數數目。  
  
    -   將 SQL_ATTR_PARAMS_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[S]，以保存參數狀態指標。  
  
2.  呼叫 SQLPrepare 準備陳述式。  
  
3.  （選擇性） 呼叫[SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404)來判斷已備妥的陳述式中的參數數目。  
  
4.  （選擇性） 如果已備妥的陳述式中每一個參數，呼叫 SQLDescribeParam 以便取得參數資訊。  
  
5.  針對每個參數標記：  
  
    -   配置 S 個參數緩衝區的陣列來儲存資料值。  
  
    -   配置 S 個參數緩衝區的陣列來儲存資料長度。  
  
    -   呼叫以將參數資料值和資料長度陣列繫結至陳述式參數的 SQLBindParameter。  
  
    -   如果參數是資料執行中的 text 或 image 參數，請設定此參數。  
  
    -   如果使用了任何資料執行中參數，請設定這些參數。  
  
6.  針對準備陳述式的每個執行：  
  
    -   將 S 資料值和 S 資料長度放在繫結參數陣列中。  
  
    -   呼叫 SQLExecute 執行備妥的陳述式。  
  
    -   如果資料在執行中輸入的參數使用，SQLExecute 會傳回 SQL_NEED_DATA。 使用 SQLParamData 和 SQLPutData 區塊傳送資料。  
  
### <a name="to-prepare-a-statement-with-row-wise-bound-parameters"></a>準備含有資料列取向繫結參數的陳述式  
  
1.  配置結構的陣列[S]，其中 S 是參數集的數目。 結構中每個參數都具有一個元素，而每個元素則具有兩部分：  
  
    -   第一個部分是適當資料類型的變數，可保存參數資料。  
  
    -   第二個部分是 SQLINTEGER 變數，可保存狀態指標。  
  
2.  呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)來設定下列屬性：  
  
    -   將 SQL_ATTR_PARAMSET_SIZE 設定為參數集 (S) 的數目。  
  
    -   將 SQL_ATTR_PARAM_BIND_TYPE 設定為步驟 1 中配置的結構大小。  
  
    -   將 SQL_ATTR_PARAMS_PROCESSED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存已處理的參數數目。  
  
    -   將 SQL_ATTR_PARAMS_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[S]，以保存參數狀態指標。  
  
3.  呼叫 SQLPrepare 準備陳述式。  
  
4.  針對每個參數標記呼叫 SQLBindParameter 參數資料值和資料長度指標指向它們在步驟 1 中所配置之結構陣列的第一個項目中的變數。 如果參數是資料執行中參數，請設定此參數。  
  
5.  針對準備陳述式的每個執行：  
  
    -   將資料值填入繫結參數緩衝區陣列。  
  
    -   呼叫 SQLExecute 執行備妥的陳述式。 驅動程式會有效率地執行 SQL 陳述式 S 次，針對每個參數集執行一次。  
  
    -   如果資料在執行中輸入的參數使用，SQLExecute 會傳回 SQL_NEED_DATA。 使用 SQLParamData 和 SQLPutData 區塊傳送資料。  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢的使用說明主題&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
