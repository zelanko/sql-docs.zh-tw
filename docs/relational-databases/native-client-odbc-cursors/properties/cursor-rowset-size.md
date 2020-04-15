---
title: 游標列集大小 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7f799722bfae35a714e740691e2cdc53e3155063
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302863"
---
# <a name="cursor-rowset-size"></a>資料指標資料列集大小
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 資料指標不限制為一次只能提取一個資料列。 他們可以檢索 SQLFetch 或**SQLFetchScroll**[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)每次調用中的多行。 與 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之類的用戶端/伺服器資料庫搭配使用時，一次擷取數個資料列會更有效率。 在提取上返回的行數稱為行集大小,並使用[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)SQL_ATTR_ROW_ARRAY_SIZE指定。  
  
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
  
 當使用按列或行綁定時,對**SQLFetch**或**SQLFetchScroll**的每個調用都使用從檢索的行集中檢索的數據填充綁定陣列。  
  
 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)還可用於從塊游標檢索列數據。 由於**SQLGetData**一次工作一行,因此在調用**SQLGetData**之前,必須調用**SQLSetPos**將行集中的特定行設置為當前行。  
  
 本機[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式提供使用列集快速檢索整個結果集的優化。 要使用此優化,在調用**SQLExecDirect**或**SQLExecute**時,將游標屬性設置為其預設值(僅轉發、唯讀、行集大小 = 1)。 本機[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式設定預設結果集。 若要在不捲動的情況下將結果傳送到用戶端時，這種做法比伺服器資料指標有效率。 在執行陳述式之後，請增加資料列集大小，並使用資料行取向或資料列取向的繫結。 這允許[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用預設結果集有效地將結果行發送到用戶端,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]而本機用戶端ODBC驅動程式會不斷從用戶端上的網路緩衝區提取行。  
  
## <a name="see-also"></a>另請參閱  
 [資料指標屬性](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
