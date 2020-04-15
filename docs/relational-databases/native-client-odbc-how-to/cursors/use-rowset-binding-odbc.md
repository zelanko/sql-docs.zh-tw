---
title: 使用行集綁定 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowset binding [ODBC]
ms.assetid: a7be05f0-6b11-4b53-9fbc-501e591eef09
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 05277e548dab36b22c023fe674e404d8b9014c7c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284478"
---
# <a name="use-rowset-binding-odbc"></a>使用資料列集繫結 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-use-column-wise-binding"></a>使用資料行取向的繫結  
  
1.  針對每個繫結資料行，請執行下列動作：  
  
    -   配置 R (或更多) 個資料行緩衝區的陣列以儲存資料值，其中 R 是資料列集的資料列數目。  
  
    -   或者，配置 R (或更多) 個資料行緩衝區的陣列來儲存資料長度。  
  
    -   呼叫[SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md)將欄的資料值和資料長度陣列結合到行集的欄位。  
  
2.  呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)來設定以下屬性:  
  
    -   將 SQL_ATTR_ROW_ARRAY_SIZE 設定為資料列集的資料列數目 (R)。  
  
    -   將 SQL_ATTR_ROW_BIND_TYPE 設定為 SQL_BIND_BY_COLUMN。  
  
    -   將 SQL_ATTR_ROWS FETCHED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存提取的資料列數目。  
  
    -   將 SQL_ATTR_ROW_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[R]，以保存資料列狀態指標。  
  
3.  執行陳述式。  
  
4.  對[SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)的每個調用都會檢索 R 行並將數據傳輸到綁定列中。  

### <a name="to-use-row-wise-binding"></a>使用資料列取向的繫結  
  
1.  配置結構的陣列[R]，其中 R 是資料列集的資料列數目。 結構中每個資料行都具有一個元素，而每個元素則具有兩部分：  
  
    -   第一個部分是適當資料類型的變數，可保存資料行資料。  
  
    -   第二個部分是 SQLINTEGER 變數，可保存資料行狀態指標。  
  
2.  呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)來設定以下屬性:  
  
    -   將 SQL_ATTR_ROW_ARRAY_SIZE 設定為資料列集的資料列數目 (R)。  
  
    -   將 SQL_ATTR_ROW_BIND_TYPE 設定為步驟 1 中配置的結構大小。  
  
    -   將 SQL_ATTR_ROWS_FETCHED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存提取的資料列數目。  
  
    -   將 SQL_ATTR_PARAMS_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[R]，以保存資料列狀態指標。  
  
3.  對於結果集中的每個列,調用[SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md)將列的數據值和數據長度指標指向步驟 1 中分配的結構陣列的第一個元素中的變數。  
  
4.  執行陳述式。  
  
5.  對[SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)的每個調用都會檢索 R 行並將數據傳輸到綁定列中。  
  
## <a name="see-also"></a>另請參閱  
 [使用游標操作主題&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)   
 [游標的實作方式](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [使用游標&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/use-cursors-odbc.md)  
  
  
