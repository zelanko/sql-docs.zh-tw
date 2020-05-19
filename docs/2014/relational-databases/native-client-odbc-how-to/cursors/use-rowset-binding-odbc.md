---
title: 使用資料列集系結（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowset binding [ODBC]
ms.assetid: a7be05f0-6b11-4b53-9fbc-501e591eef09
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a5939d97f518dd88f6eaa48fde259d6b4eab54ae
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705228"
---
# <a name="use-rowset-binding-odbc"></a>使用資料列集繫結 (ODBC)
    
### <a name="to-use-column-wise-binding"></a>使用資料行取向的繫結  
  
1.  針對每個繫結資料行，請執行下列動作：  
  
    -   配置 R (或更多) 個資料行緩衝區的陣列以儲存資料值，其中 R 是資料列集的資料列數目。  
  
    -   或者，配置 R (或更多) 個資料行緩衝區的陣列來儲存資料長度。  
  
    -   呼叫[SQLBindCol](../../native-client-odbc-api/sqlbindcol.md) ，將資料行的資料值和資料長度陣列系結至資料列集的資料行。  
  
2.  呼叫[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)以設定下列屬性：  
  
    -   將 SQL_ATTR_ROW_ARRAY_SIZE 設定為資料列集的資料列數目 (R)。  
  
    -   將 SQL_ATTR_ROW_BIND_TYPE 設定為 SQL_BIND_BY_COLUMN。  
  
    -   將 SQL_ATTR_ROWS FETCHED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存提取的資料列數目。  
  
    -   將 SQL_ATTR_ROW_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[R]，以保存資料列狀態指標。  
  
3.  執行陳述式。  
  
4.  [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)的每個呼叫都會抓取 R 資料列，並將資料傳輸至系結的資料行。  
  
### <a name="to-use-row-wise-binding"></a>使用資料列取向的繫結  
  
1.  配置結構的陣列[R]，其中 R 是資料列集的資料列數目。 結構中每個資料行都具有一個元素，而每個元素則具有兩部分：  
  
    -   第一個部分是適當資料類型的變數，可保存資料行資料。  
  
    -   第二個部分是 SQLINTEGER 變數，可保存資料行狀態指標。  
  
2.  呼叫[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)以設定下列屬性：  
  
    -   將 SQL_ATTR_ROW_ARRAY_SIZE 設定為資料列集的資料列數目 (R)。  
  
    -   將 SQL_ATTR_ROW_BIND_TYPE 設定為步驟 1 中配置的結構大小。  
  
    -   將 SQL_ATTR_ROWS_FETCHED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存提取的資料列數目。  
  
    -   將 SQL_ATTR_PARAMS_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[R]，以保存資料列狀態指標。  
  
3.  針對結果集中的每個資料行呼叫[SQLBindCol](../../native-client-odbc-api/sqlbindcol.md) ，以將資料行的資料值和資料長度指標指向其在步驟1所配置之結構陣列第一個元素中的變數。  
  
4.  執行陳述式。  
  
5.  [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)的每個呼叫都會抓取 R 資料列，並將資料傳輸至系結的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標的 how to 主題 &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)   
 [如何實作為資料指標](../../native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [&#40;ODBC&#41;使用資料指標](use-cursors-odbc.md)  
  
  
