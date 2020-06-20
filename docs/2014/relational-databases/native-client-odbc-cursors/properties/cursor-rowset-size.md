---
title: 資料指標資料列集大小 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
author: rothja
ms.author: jroth
ms.openlocfilehash: 73c5d1dc337538869b75aa800ccdc5ab461d5bdc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020722"
---
# <a name="cursor-rowset-size"></a>資料指標資料列集大小
  ODBC 資料指標不限制為一次只能提取一個資料列。 他們可以在每次呼叫**SQLFetch**或[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)時，抓取多個資料列。 與 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之類的用戶端/伺服器資料庫搭配使用時，一次擷取數個資料列會更有效率。 提取所傳回的資料列數目稱為資料列集大小，並使用[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)的 SQL_ATTR_ROW_ARRAY_SIZE 來指定。  
  
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
  
 使用資料行取向或資料列取向的系結時，每次呼叫**SQLFetch**或**SQLFetchScroll**時，都會以所抓取之資料列集的資料來填入系結陣列。  
  
 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md)也可以用來從區塊資料指標取出資料行資料。 由於**SQLGetData**會一次處理一個資料列，因此在呼叫**SQLGetData**之前，必須先呼叫**SQLSetPos** ，將資料列集中的特定資料列設定為目前的資料列。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會使用資料列集來提供優化，以快速取得整個結果集。 若要使用此優化，請在呼叫**SQLExecDirect**或**SQLExecute**時，將資料指標屬性設定為其預設值（順向、唯讀、資料列集大小 = 1）。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會設定預設的結果集。 若要在不捲動的情況下將結果傳送到用戶端時，這種做法比伺服器資料指標有效率。 在執行陳述式之後，請增加資料列集大小，並使用資料行取向或資料列取向的繫結。 這可讓您 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用預設結果集，將結果資料列有效率地傳送給用戶端，而 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE client ODBC 驅動程式會從用戶端上的網路緩衝區持續提取資料列。  
  
## <a name="see-also"></a>另請參閱  
 [資料指標屬性](cursor-properties.md)  
  
  
