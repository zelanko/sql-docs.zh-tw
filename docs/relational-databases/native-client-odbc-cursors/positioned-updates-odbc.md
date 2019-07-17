---
title: 定位更新 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a1d8b5df2b2b5255a685ae51b2a182746e9b9c17
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902448"
---
# <a name="positioned-updates-odbc"></a>定位更新 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 支援兩個方法於資料指標上執行定位更新：  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF 子句  
  
 更常見的方法是使用**SQLSetPos**。 它的選項如下。  
  
 SQL_POSITION  
 將資料指標置於目前資料列集的特定資料列中。  
  
 SQL_REFRESH  
 以資料指標目前所在位置之資料列中的值，重新整理繫結至結果集資料行的程式變數。  
  
 SQL_UPDATE  
 以繫結至結果集資料行之程式變數中儲存的值，更新資料指標中的目前資料列。  
  
 SQL_DELETE  
 刪除資料指標中的目前資料行。  
  
 **SQLSetPos**可以搭配任何陳述式的結果集的陳述式控制代碼資料指標屬性設定為使用伺服器資料指標時。 結果集資料行必須繫結至程式變數。 應用程式提取資料列，它會呼叫**SQLSetPos**(SQL_POSTION) 將游標放在資料列。 然後應用程式可以呼叫 SQLSetPos(SQL_DELETE) 來刪除目前的資料列，或者可以將新的資料值移到繫結的程式變數中，並呼叫 SQLSetPos(SQL_UPDATE) 來更新目前的資料列。  
  
 應用程式可更新或刪除任何資料列與資料列集中**SQLSetPos**。 呼叫**SQLSetPos**是方便的替代建構及執行 SQL 陳述式。 **SQLSetPos**目前的資料列集上運作，且可以呼叫之後，才能使用[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)。  
  
 資料列集大小設定藉由呼叫[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) SQL_ATTR_ROW_ARRAY_SIZE 屬性引數。 **SQLSetPos**使用新的資料列集大小，但只能在呼叫之後**SQLFetch**或是**SQLFetchScroll**。 比方說，如果資料列集大小變更時， **SQLSetPos**呼叫，然後**SQLFetch**或是**SQLFetchScroll**呼叫。 呼叫**SQLSetPos**會使用舊的資料列集大小，但**SQLFetch**或是**SQLFetchScroll**會使用新的資料列集大小。  
  
 資料列集中的第一個資料列是資料列號碼 1。 中的 RowNumber 引數**SQLSetPos**必須識別資料列中資料列集; 也就是說，其值必須介於 1 與最近提取的資料列數目。 這可能會小於資料列集大小。 如果 RowNumber 是 0，此作業會套用到資料列集內的每一個資料列。  
  
 刪除作業**SQLSetPos**刪除一或多個選取的資料列的資料表的資料來源。 若要刪除的資料列**SQLSetPos**，應用程式會呼叫**SQLSetPos**與 Operation 設定為 SQL_DELETE 並將 RowNumber 設定要刪除的資料列數目。 如果 RowNumber 是 0，將會刪除資料列集內的所有資料列。  
  
 在後**SQLSetPos**傳回刪除的資料列是目前的資料列，而且其狀態為 SQL_ROW_DELETED。 資料列不能在任何其他定位作業，例如呼叫[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)或是**SQLSetPos**。  
  
 當您刪除資料列集 （RowNumber 等於 0） 的所有資料列時，應用程式可以防止驅動程式刪除某些資料列的更新作業，如同使用資料列作業陣列**SQLSetPos**。  
  
 刪除的每一個資料列都應該是存在於結果集內的資料列。 如果應用程式緩衝區已藉由提取來填滿，而且已經維護資料列狀態陣列，則它在每一個資料列位置的值都不應該是 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 定位更新也可以使用 UPDATE、DELETE 和 INSERT 陳述式上的 WHERE CURRENT OF 子句來執行。 WHERE CURRENT OF 需要 資料指標名稱，ODBC 將會產生何時[SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)函式呼叫時，或您可以藉由呼叫指定**SQLSetCursorName**。 下列是用來在 ODBC 應用程式內執行 WHERE CURRENT OF 更新的一般步驟：  
  
-   呼叫**SQLSetCursorName**建立陳述式控制代碼的資料指標名稱。  
  
-   建立包含 FOR UPDATE OF 子句的 SELECT 陳述式，並加以執行。  
  
-   呼叫**SQLFetchScroll**擷取資料列集或**SQLFetch**擷取一個資料列。  
  
-   呼叫**SQLSetPos** (SQL_POSITION) 將游標放在資料列。  
  
-   建置及執行 UPDATE 陳述式搭配使用資料指標名稱設定使用 WHERE CURRENT OF 子句**SQLSetCursorName**。  
  
 或者，您可以呼叫**SQLGetCursorName**在您執行 SELECT 陳述式，而不是呼叫之後**SQLSetCursorName**之前執行 SELECT 陳述式。 **SQLGetCursorName**會傳回 ODBC 所指派，如果您未設定資料指標的名稱使用的預設資料指標名稱**SQLSetCursorName**。  
  
 **SQLSetPos**更為優先 WHERE CURRENT OF 當您使用伺服器資料指標。 如果您搭配 ODBC 資料指標程式庫使用可更新的靜態資料指標，此資料指標程式庫會實作 WHERE CURRENT OF 更新，其方式是針對基礎資料表加入具有索引鍵值的 WHERE 子句。 如果資料表內的索引鍵不是唯一的，這樣會造成非預期的更新。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標&#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
