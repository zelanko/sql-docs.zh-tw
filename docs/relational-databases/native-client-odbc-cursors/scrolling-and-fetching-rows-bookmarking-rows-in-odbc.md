---
title: 書籤在 ODBC 中的資料列 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d58ce5236a2d74e1749e88f0bffa9ca86f974733
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740048"
---
# <a name="scrolling-and-fetching-rows---bookmarking-rows-in-odbc"></a>捲動和擷取資料列 - ODBC 中的書籤資料列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  書籤是用來識別資料列的值。 書籤值的意義僅適用於驅動程式或資料來源。 例如，書籤可能跟資料列號碼一樣簡單，也可能跟磁碟位址一樣複雜。 在 ODBC 中，應用程式會要求特定資料列的書籤、將其儲存起來，然後將其傳回資料指標，即可傳回到資料列。  
  
 在提取資料列時， [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)，應用程式可以使用書籤做為基礎選取起始資料列。 這是一個絕對位址的形式，因為它不相依於目前的資料指標位置。 若要捲動到加上書籤的資料列，應用程式會呼叫**SQLFetchScroll**具有*Sqlfetchscroll*要使用 sql_fetch_bookmark。 此作業使用 SQL_ATTR_FETCH_BOOKMARK_PTR 選項屬性所指向的書籤。 它會傳回資料列集，從該書籤識別的資料列開始。 應用程式可以指定這項作業中的位移*FetchOffset*呼叫的引數**SQLFetchScroll**。 指定位移時，所傳回之資料列集的第一個資料列會透過將 FetchOffset 引數中的數字加入到書籤所識別之資料列數目決定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式僅針對靜態和索引鍵集資料指標支援書籤。 如果設定書籤開啟時要求動態資料指標，就會改為開啟索引鍵集。  
  
 書籤也可搭配**SQLBulkOperations**開始書籤的資料列集上執行作業的函式。  
  
## <a name="see-also"></a>另請參閱  
 [捲動與擷取資料列](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
  
