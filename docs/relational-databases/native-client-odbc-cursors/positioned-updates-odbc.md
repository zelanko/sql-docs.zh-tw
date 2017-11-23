---
title: "定位更新 (ODBC) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- SQLSetPos function
- SQLSetCursorName function
- ODBC applications, cursors
- cursors [ODBC], positioned updates
- positioned updates [ODBC]
- ODBC cursors, positioned updates
ms.assetid: ff404e02-630f-474d-b5d4-06442b756991
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a77f61ebd66cf6bda10d8c59c61e5364208a66e9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="positioned-updates-odbc"></a>定位更新 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 支援兩個方法於資料指標上執行定位更新：  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF 子句  
  
 更常用的方法是使用**SQLSetPos**。 它的選項如下。  
  
 SQL_POSITION  
 將資料指標置於目前資料列集的特定資料列中。  
  
 SQL_REFRESH  
 以資料指標目前所在位置之資料列中的值，重新整理繫結至結果集資料行的程式變數。  
  
 SQL_UPDATE  
 以繫結至結果集資料行之程式變數中儲存的值，更新資料指標中的目前資料列。  
  
 SQL_DELETE  
 刪除資料指標中的目前資料行。  
  
 **SQLSetPos**可以搭配任何陳述式時結果集的陳述式控制代碼資料指標屬性設定為使用伺服器資料指標。 結果集資料行必須繫結至程式變數。 應用程式提取資料列時，立即呼叫**SQLSetPos**(SQL_POSTION) 將游標放在資料列。 然後應用程式可以呼叫 SQLSetPos(SQL_DELETE) 來刪除目前的資料列，或者可以將新的資料值移到繫結的程式變數中，並呼叫 SQLSetPos(SQL_UPDATE) 來更新目前的資料列。  
  
 應用程式可以更新或刪除任何資料列與資料列集中**SQLSetPos**。 呼叫**SQLSetPos**是一個方便的替代方式建構及執行 SQL 陳述式。 **SQLSetPos**目前資料列集上運作，而且可用只有在呼叫之後[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)。  
  
 資料列集大小由呼叫所設定[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)使用 SQL_ATTR_ROW_ARRAY_SIZE 屬性引數。 **SQLSetPos**使用新的資料列集大小，但只有在呼叫之後**SQLFetch**或**SQLFetchScroll**。 例如，如果變更資料列集大小， **SQLSetPos**稱為然後**SQLFetch**或**SQLFetchScroll**呼叫。 若要呼叫**SQLSetPos**使用舊的資料列集大小，但**SQLFetch**或**SQLFetchScroll**會使用新的資料列集大小。  
  
 資料列集中的第一個資料列是資料列號碼 1。 中的 RowNumber 引數**SQLSetPos**必須識別資料列中資料列集; 也就是說，其值必須是介於 1 與最近提取的資料列數目。 這可能會小於資料列集大小。 如果 RowNumber 是 0，此作業會套用到資料列集內的每一個資料列。  
  
 刪除作業的**SQLSetPos** ，使得資料來源刪除一或多個選取的資料列的資料表。 若要刪除的資料列**SQLSetPos**，應用程式會呼叫**SQLSetPos**與 Operation 設定為 SQL_DELETE 並將 RowNumber 設定為的資料列數，若要刪除。 如果 RowNumber 是 0，將會刪除資料列集內的所有資料列。  
  
 之後**SQLSetPos**傳回時，將已刪除的資料列是目前的資料列，而且其狀態為 SQL_ROW_DELETED。 資料列不能在任何其他定位作業，例如呼叫[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)或**SQLSetPos**。  
  
 當您刪除資料列集 （RowNumber 等於 0） 的所有資料列時，應用程式可以避免驅動程式刪除某些資料列的 update 作業就像是使用資料列作業陣列**SQLSetPos**。  
  
 刪除的每一個資料列都應該是存在於結果集內的資料列。 如果應用程式緩衝區已藉由提取來填滿，而且已經維護資料列狀態陣列，則它在每一個資料列位置的值都不應該是 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 定位更新也可以使用 UPDATE、DELETE 和 INSERT 陳述式上的 WHERE CURRENT OF 子句來執行。 WHERE CURRENT OF 需要資料指標名稱，ODBC 將會產生時[SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)函式，或者您可以藉由呼叫指定**SQLSetCursorName**。 下列是用來在 ODBC 應用程式內執行 WHERE CURRENT OF 更新的一般步驟：  
  
-   呼叫**SQLSetCursorName**建立陳述式控制代碼的資料指標名稱。  
  
-   建立包含 FOR UPDATE OF 子句的 SELECT 陳述式，並加以執行。  
  
-   呼叫**SQLFetchScroll**擷取資料列集或**SQLFetch**擷取一個資料列。  
  
-   呼叫**SQLSetPos** (SQL_POSITION) 將游標放在資料列。  
  
-   建置並執行 UPDATE 陳述式搭配 WHERE CURRENT OF 子句使用設定的資料指標名稱**SQLSetCursorName**。  
  
 或者，您可以呼叫**SQLGetCursorName**執行 SELECT 陳述式，而不是呼叫之後**SQLSetCursorName**之前執行 SELECT 陳述式。 **SQLGetCursorName**傳回 ODBC 所指派，如果您未設定資料指標的名稱使用的預設資料指標名稱**SQLSetCursorName**。  
  
 **SQLSetPos**更為優先 WHERE CURRENT OF 當您使用伺服器資料指標。 如果您搭配 ODBC 資料指標程式庫使用可更新的靜態資料指標，此資料指標程式庫會實作 WHERE CURRENT OF 更新，其方式是針對基礎資料表加入具有索引鍵值的 WHERE 子句。 如果資料表內的索引鍵不是唯一的，這樣會造成非預期的更新。  
  
## <a name="see-also"></a>請參閱＜  
 [使用資料指標 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
