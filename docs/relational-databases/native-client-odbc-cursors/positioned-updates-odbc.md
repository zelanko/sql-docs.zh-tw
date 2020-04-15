---
title: 定位更新 (ODBC) |微軟文件
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 52495f670986638cac02661240e349713424256e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305320"
---
# <a name="positioned-updates-odbc"></a>定位更新 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

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
  
 當語句句柄游標屬性設置為使用伺服器游標時 **,SQLSetPos**可與任何語句結果集一起使用。 結果集資料行必須繫結至程式變數。 一旦應用程序獲取了一行,它調用**SQLSetPos**(SQL_POSTION) 將游標定位在行上。 然後應用程式可以呼叫 SQLSetPos(SQL_DELETE) 來刪除目前的資料列，或者可以將新的資料值移到繫結的程式變數中，並呼叫 SQLSetPos(SQL_UPDATE) 來更新目前的資料列。  
  
 應用程式可以使用**SQLSetPos**更新或刪除行集中的任何行。 呼叫**SQLSetPos**是建構和執行 SQL 語句的便捷替代方法。 **SQLSetPos**在當前行集中運行,只能在調用[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)後使用。  
  
 行集大小由對[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)的調用設置,屬性參數為SQL_ATTR_ROW_ARRAY_SIZE。 **SQLSetPos**使用新的行集大小,但僅在調用**SQLFetch**或**SQLFetchScroll**後。 例如,如果更改了行集大小,則調用**SQLSetPos,** 然後調用**SQLFetch**或**SQLFetchScroll。** 對**SQLSetPos 的**呼叫使用舊的行集大小,但**SQLFetch**或**SQLFetchScroll**使用新的列集大小。  
  
 資料列集中的第一個資料列是資料列號碼 1。 **SQLSetPos**中的行編號參數必須標識行集中的行;因此,在行集中,必須標識行數。也就是說,其值必須介於 1 和最近提取的行數之間。 這可能會小於資料列集大小。 如果 RowNumber 是 0，此作業會套用到資料列集內的每一個資料列。  
  
 **SQLSetPos**的刪除操作使數據源刪除表的一個或多個選定行。 要刪除**SQLSetPos 的**行,應用程式呼叫**SQLSetPos,** 操作設定為 SQL_DELETE,行號設置為要刪除的行數。 如果 RowNumber 是 0，將會刪除資料列集內的所有資料列。  
  
 **SQLSetPos**傳回後,已刪除的行是當前行,其狀態為SQL_ROW_DELETED。 該行不能用於任何其他定位操作,例如對[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)或**SQLSetPos**的調用。  
  
 當您刪除行集的所有行(RowNumber 等於 0)時,應用程式可以阻止驅動程式使用行操作陣列刪除某些行,就像**SQLSetPos**的更新操作一樣。  
  
 刪除的每一個資料列都應該是存在於結果集內的資料列。 如果應用程式緩衝區已藉由提取來填滿，而且已經維護資料列狀態陣列，則它在每一個資料列位置的值都不應該是 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 定位更新也可以使用 UPDATE、DELETE 和 INSERT 陳述式上的 WHERE CURRENT OF 子句來執行。 WHERE CURRENT OF 需要一個游標名稱,在調用[SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)函數時將生成 ODBC,或者可以通過調用**SQLSetCursorName**來指定該名稱。 下列是用來在 ODBC 應用程式內執行 WHERE CURRENT OF 更新的一般步驟：  
  
-   呼叫**SQLSetCursorName**為敘述的句柄建立游標名稱。  
  
-   建立包含 FOR UPDATE OF 子句的 SELECT 陳述式，並加以執行。  
  
-   調用**SQLFetchScroll**以檢索行集或**SQLFetch**以檢索行。  
  
-   呼叫**SQLSetPos** (SQL_POSITION) 將游標放置在行上。  
  
-   使用帶有**SQLSetCursorName**的遊標名稱集生成並執行具有 WHERE CURRENT OF 子句的更新語句。  
  
 或者,您可以在執行 SELECT 語句後呼叫**SQLGetCursorName,** 而不是在執行 SELECT 語句之前呼叫**SQLSetCursorName。** 如果不使用**SQLSetCursorName**設定游標名稱 **,SQLGetCursorName**將傳回由 ODBC 分配的預設游標名稱。  
  
 當您使用伺服器游標時 **,SQLSetPos**優先於 WHERE。 如果您搭配 ODBC 資料指標程式庫使用可更新的靜態資料指標，此資料指標程式庫會實作 WHERE CURRENT OF 更新，其方式是針對基礎資料表加入具有索引鍵值的 WHERE 子句。 如果資料表內的索引鍵不是唯一的，這樣會造成非預期的更新。  
  
## <a name="see-also"></a>另請參閱  
 [使用游標&#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
