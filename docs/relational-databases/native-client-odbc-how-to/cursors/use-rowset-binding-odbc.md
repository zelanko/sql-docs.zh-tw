---
title: 使用資料列集繫結 (ODBC) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1277b565ccb60aaa7972f98ec731675b5a9bb7cd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813476"
---
# <a name="use-rowset-binding-odbc"></a>使用資料列集繫結 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-use-column-wise-binding"></a>使用資料行取向的繫結  
  
1.  針對每個繫結資料行，請執行下列動作：  
  
    -   配置 R (或更多) 個資料行緩衝區的陣列以儲存資料值，其中 R 是資料列集的資料列數目。  
  
    -   或者，配置 R (或更多) 個資料行緩衝區的陣列來儲存資料長度。  
  
    -   呼叫[SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md)到資料行的資料值和資料長度陣列繫結至資料列集資料行。  
  
2.  呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)設定下列屬性：  
  
    -   將 SQL_ATTR_ROW_ARRAY_SIZE 設定為資料列集的資料列數目 (R)。  
  
    -   將 SQL_ATTR_ROW_BIND_TYPE 設定為 SQL_BIND_BY_COLUMN。  
  
    -   將 SQL_ATTR_ROWS FETCHED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存提取的資料列數目。  
  
    -   將 SQL_ATTR_ROW_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[R]，以保存資料列狀態指標。  
  
3.  執行陳述式。  
  
4.  每次呼叫[SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)或是[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)擷取 R 個資料列，並將資料傳送到繫結的資料行。  
  
### <a name="to-use-row-wise-binding"></a>使用資料列取向的繫結  
  
1.  配置結構的陣列[R]，其中 R 是資料列集的資料列數目。 結構中每個資料行都具有一個元素，而每個元素則具有兩部分：  
  
    -   第一個部分是適當資料類型的變數，可保存資料行資料。  
  
    -   第二個部分是 SQLINTEGER 變數，可保存資料行狀態指標。  
  
2.  呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)設定下列屬性：  
  
    -   將 SQL_ATTR_ROW_ARRAY_SIZE 設定為資料列集的資料列數目 (R)。  
  
    -   將 SQL_ATTR_ROW_BIND_TYPE 設定為步驟 1 中配置的結構大小。  
  
    -   將 SQL_ATTR_ROWS_FETCHED_PTR 屬性設定為指向 SQLUINTEGER 變數，以保存提取的資料列數目。  
  
    -   將 SQL_ATTR_PARAMS_STATUS_PTR 設定為指向 SQLUSSMALLINT 變數的陣列[R]，以保存資料列狀態指標。  
  
3.  在結果集中的每一個資料行，呼叫[SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md)以指向它們在步驟 1 中所配置之結構陣列的第一個項目中變數的資料值和資料行的資料長度指標。  
  
4.  執行陳述式。  
  
5.  每次呼叫[SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)或是[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)擷取 R 個資料列，並將資料傳送到繫結的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標使用說明主題&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)   
 [如何實作資料指標](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [使用資料指標&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/use-cursors-odbc.md)  
  
  
