---
title: 定點更新（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c9f21d5679e3bc926fc9a824ba11d8283dc9dad6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020749"
---
# <a name="positioned-updates-odbc"></a>定位更新 (ODBC)
  ODBC 支援兩個方法於資料指標上執行定位更新：  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF 子句  
  
 較常見的方法是使用**SQLSetPos**。 它的選項如下。  
  
 SQL_POSITION  
 將資料指標置於目前資料列集的特定資料列中。  
  
 SQL_REFRESH  
 以資料指標目前所在位置之資料列中的值，重新整理繫結至結果集資料行的程式變數。  
  
 SQL_UPDATE  
 以繫結至結果集資料行之程式變數中儲存的值，更新資料指標中的目前資料列。  
  
 SQL_DELETE  
 刪除資料指標中的目前資料行。  
  
 當語句控制碼資料指標屬性設定為使用伺服器資料指標時， **SQLSetPos**可以與任何語句結果集搭配使用。 結果集資料行必須繫結至程式變數。 一旦應用程式提取資料列，它就會呼叫**SQLSetPos**（SQL_POSTION），將資料指標放在資料列上。 然後應用程式可以呼叫 SQLSetPos(SQL_DELETE) 來刪除目前的資料列，或者可以將新的資料值移到繫結的程式變數中，並呼叫 SQLSetPos(SQL_UPDATE) 來更新目前的資料列。  
  
 應用程式可以使用**SQLSetPos**來更新或刪除資料列集中的任何資料列。 呼叫**SQLSetPos**是用來建立和執行 SQL 語句的方便替代方式。 **SQLSetPos**會在目前的資料列集上運作，而且只能在呼叫[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)之後使用。  
  
 資料列集大小是透過 SQL_ATTR_ROW_ARRAY_SIZE 的屬性引數呼叫[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)所設定。 **SQLSetPos**會使用新的資料列集大小，但只會在呼叫**SQLFetch**或**SQLFetchScroll**之後。 例如，如果資料列集大小已變更，則會呼叫**SQLSetPos** ，然後呼叫**SQLFetch**或**SQLFetchScroll** 。 對**SQLSetPos**的呼叫會使用舊的資料列集大小，但是**SQLFetch**或**SQLFetchScroll**會使用新的資料列集大小。  
  
 資料列集中的第一個資料列是資料列號碼 1。 **SQLSetPos**中的 RowNumber 引數必須識別資料列集中的資料列;也就是說，其值必須介於1到最近提取的資料列數目的範圍內。 這可能會小於資料列集大小。 如果 RowNumber 是 0，此作業會套用到資料列集內的每一個資料列。  
  
 **SQLSetPos**的 delete 作業會使資料來源刪除資料表的一個或多個選取資料列。 若要使用**SQLSetPos**刪除資料列，應用程式會呼叫**SQLSetPos** ，並將 Operation 設定為 SQL_DELETE 並將 RowNumber 設定為要刪除的資料列數目。 如果 RowNumber 是 0，將會刪除資料列集內的所有資料列。  
  
 **SQLSetPos**傳回之後，刪除的資料列就是目前的資料列，而且其狀態會是 SQL_ROW_DELETED。 資料列不能用於任何其他定位作業，例如呼叫[SQLGetData](../native-client-odbc-api/sqlgetdata.md)或**SQLSetPos**。  
  
 當您刪除資料列集的所有資料列（RowNumber 等於0）時，應用程式可以使用資料列作業陣列，讓驅動程式無法刪除某些資料列，就像**SQLSetPos**的更新作業一樣。  
  
 刪除的每一個資料列都應該是存在於結果集內的資料列。 如果應用程式緩衝區已藉由提取來填滿，而且已經維護資料列狀態陣列，則它在每一個資料列位置的值都不應該是 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 定位更新也可以使用 UPDATE、DELETE 和 INSERT 陳述式上的 WHERE CURRENT OF 子句來執行。 其中 CURRENT 的需要資料指標名稱，ODBC 將在呼叫[SQLGetCursorName](../native-client-odbc-api/sqlgetcursorname.md)函式時產生，或藉由呼叫**SQLSetCursorName**來指定。 下列是用來在 ODBC 應用程式內執行 WHERE CURRENT OF 更新的一般步驟：  
  
-   呼叫**SQLSetCursorName**以建立語句控制碼的資料指標名稱。  
  
-   建立包含 FOR UPDATE OF 子句的 SELECT 陳述式，並加以執行。  
  
-   呼叫**SQLFetchScroll**來抓取資料列集或**SQLFetch** ，以取得資料列。  
  
-   呼叫**SQLSetPos** （SQL_POSITION），將游標放在資料列上。  
  
-   使用以**SQLSetCursorName**設定的資料指標名稱，建立並執行含有 WHERE CURRENT of 子句的 UPDATE 語句。  
  
 或者，您可以在執行 SELECT 語句後呼叫**SQLGetCursorName** ，而不是在執行 select 語句之前呼叫**SQLSetCursorName** 。 如果您未使用**SQLSetCursorName**來設定資料指標名稱，則**SQLGETCURSORNAME**會傳回 ODBC 指派的預設資料指標名稱。  
  
 當您使用伺服器資料指標時， **SQLSetPos**會優先于目前的。 如果您搭配 ODBC 資料指標程式庫使用可更新的靜態資料指標，此資料指標程式庫會實作 WHERE CURRENT OF 更新，其方式是針對基礎資料表加入具有索引鍵值的 WHERE 子句。 如果資料表內的索引鍵不是唯一的，這樣會造成非預期的更新。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;使用資料指標](using-cursors-odbc.md)  
  
  
