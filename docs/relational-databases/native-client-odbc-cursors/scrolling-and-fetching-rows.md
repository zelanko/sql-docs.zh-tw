---
title: 捲動與擷取行 |微軟文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- SQLFetchScroll function
- ODBC applications, cursors
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- fetching [ODBC]
- ODBC cursors, scrolling rows
ms.assetid: 9109f10d-326b-4a6d-8c97-831f60da8c4c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ae9f1079f329951045d4b3f61b39c12efc153fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302484"
---
# <a name="scrolling-and-fetching-rows"></a>捲動與提取資料列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  若要使用可捲動的資料指標，ODBC 應用程式必須：  
  
-   使用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)設置游標功能。  
  
-   使用**SQLExecute**或**SQLExecDirect**打開游標。  
  
-   使用**SQLFetch**或[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)滾動和提取行。  
  
 **SQLFetch**和**SQLFetchSroll**可以一次獲取行塊。 返回的行數通過使用**SQLSetStmtAttr**設置SQL_ATTR_ROW_ARRAY_SIZE參數來指定。  
  
 ODBC 應用程式可以使用**SQLFetch**通過僅轉發游標進行獲取。  
  
 **SQLFetchScroll**用於滾動游標。 **SQLFetchScroll**支援提取下一個、先行、第一行和最後一個行集,除了相對提取(從當前行集的開頭提取行 *)* 和絕對提取(從行*n*開始提取行集)。 如果*n*在絕對提取中為負數,則行將從結果集的末尾計數。 資料列的絕對提取 -1 表示提取從結果集的最後一個資料列開始的資料列集。  
  
 僅對其塊游標功能(如報表)使用**SQLFetchScroll**的應用程式可能會通過結果集一次,僅使用該選項獲取下一個行集。 另一方面,基於螢幕的應用程式可以利用**SQLFetchScroll**的所有功能。 如果應用程式將行集大小設置為螢幕上顯示的行數,並將螢幕緩衝區綁定到結果集,則可以將滾動條操作直接轉換為對**SQLFetchScroll**的調用。  
  
|捲軸作業|SQLFetchScroll 捲動選項|  
|--------------------------|-------------------------------------|  
|向上捲動一頁|SQL_FETCH_PRIOR|  
|向下捲動一頁|SQL_FETCH_NEXT|  
|向上捲動一行|SQL_FETCH_RELATIVE提取偏移量等於 -1|  
|向下捲動一行|包含 FetchOffset 的 SQL_FETCH_RELATIVE 等於 1|  
|捲動方塊到頂端|SQL_FETCH_FIRST|  
|捲動方塊到底部|SQL_FETCH_LAST|  
|隨機捲動方塊位置|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>本節內容  
  
-   [在 ODBC 中的資料列上加上書籤](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用游標&#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
