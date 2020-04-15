---
title: ODBC 中的書籤行 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- ODBC cursors, scrolling rows
- bookmarks [ODBC]
ms.assetid: 9cfcd243-c9d4-4c2a-abc4-399dbabe5f6b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0c1a4216d57d4f8178e55c54f7b0bcf61b8624c2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303996"
---
# <a name="scrolling-and-fetching-rows---bookmarking-rows-in-odbc"></a>捲動和擷取資料列 - ODBC 中的書籤資料列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  書籤是用來識別資料列的值。 書籤值的意義僅適用於驅動程式或資料來源。 例如，書籤可能跟資料列號碼一樣簡單，也可能跟磁碟位址一樣複雜。 在 ODBC 中，應用程式會要求特定資料列的書籤、將其儲存起來，然後將其傳回資料指標，即可傳回到資料列。  
  
 使用[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)提取行時,應用程式可以使用書籤作為選擇起始行的基礎。 這是一個絕對位址的形式，因為它不相依於目前的資料指標位置。 要滾動到書籤行,應用程式調用**SQLFetchScroll,** 獲取*方向*為 SQL_FETCH_BOOKMARK。 此作業使用 SQL_ATTR_FETCH_BOOKMARK_PTR 選項屬性所指向的書籤。 它會傳回資料列集，從該書籤識別的資料列開始。 應用程式可以在調用**SQLFetchScroll**的*FetchOffset*參數中指定此操作的偏移量。 指定位移時，所傳回之資料列集的第一個資料列會透過將 FetchOffset 引數中的數字加入到書籤所識別之資料列數目決定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式僅針對靜態和索引鍵集資料指標支援書籤。 如果設定書籤開啟時要求動態資料指標，就會改為開啟索引鍵集。  
  
 書籤還可以與**SQLBulk 操作**函數一起使用,對從書籤開始的一組行執行操作。  
  
## <a name="see-also"></a>另請參閱  
 [捲動與提取資料列](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
  
