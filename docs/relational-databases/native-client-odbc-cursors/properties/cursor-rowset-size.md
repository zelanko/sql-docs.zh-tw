---
title: "資料指標資料列集大小 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 028dfc5275a5c8a0aa9f7527cd500545dbe6ff81
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="cursor-rowset-size"></a>資料指標資料列集大小
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC 資料指標不限制為一次只能提取一個資料列。 他們可以擷取每個呼叫中的多個資料列**SQLFetch**或[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)。 與 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之類的用戶端/伺服器資料庫搭配使用時，一次擷取數個資料列會更有效率。 傳回在提取資料列數目稱為資料列集大小，使用 SQL_ATTR_ROW_ARRAY_SIZE 來指定[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
```  
SQLUINTEGER uwRowsize;  
SQLSetStmtAttr(m_hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)uwRowsetSize, SQL_IS_UINTEGER);  
```  
  
 資料列集大小大於 1 的資料指標稱為區塊資料指標。  
  
 有兩個選項可用來繫結區塊資料指標的結果集資料行：  
  
-   資料行取向的繫結  
  
     每個資料行都會繫結至變數的陣列。 每個陣列所擁有的元素數目則都與資料列集大小相當。  
  
-   資料列取向的繫結  
  
     陣列是使用保存資料列中所有資料行之資料和指標的結構而建立。 陣列所擁有的結構數目與資料列集大小相當。  
  
 使用資料行取向或資料列取向的繫結時，每次呼叫**SQLFetch**或**SQLFetchScroll**從擷取的資料列集的資料填入繫結的陣列。  
  
 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)也可用來從區塊資料指標擷取資料行的資料。 因為**SQLGetData**一次處理一個資料列**SQLSetPos**必須將特定的資料列中資料列集設定為目前的資料列會在呼叫之前呼叫**SQLGetData**。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式提供使用資料列集來擷取整個結果集，快速地最佳化。 若要使用此最佳化，將資料指標屬性設定為其預設值 (順向、 唯讀、 資料列集大小 = 1) 次**SQLExecDirect**或**SQLExecute**呼叫。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會設定預設結果集。 若要在不捲動的情況下將結果傳送到用戶端時，這種做法比伺服器資料指標有效率。 在執行陳述式之後，請增加資料列集大小，並使用資料行取向或資料列取向的繫結。 這可讓[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用預設結果集，以有效率地將結果資料列傳送到用戶端，而[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]持續從用戶端上的網路緩衝區提取資料列的 Native Client ODBC 驅動程式。  
  
## <a name="see-also"></a>請參閱  
 [資料指標屬性](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
