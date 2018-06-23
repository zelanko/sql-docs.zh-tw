---
title: 設定資料指標選項 (ODBC) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], options
ms.assetid: 0e72b48a-fc5a-4656-8cf5-39f57d8c1565
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d4694337517f51c08273a988e105ae49fa9bb15a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034127"
---
# <a name="set-cursor-options-odbc"></a>設定資料指標選項 (ODBC)
  若要設定資料指標選項，請呼叫[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)設定或[SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md)來取得控制資料指標行為的陳述式選項。  
  
|*Attribute*|指定|  
|-----------------|---------------|  
|SQL_ATTR_CURSOR_TYPE|順向、靜態、動態或索引鍵集驅動的資料指標類型|  
|SQL_ATTR_CONCURRENCY|唯讀、鎖定、開放式 (使用時間戳記) 或開放式 (使用值) 的並行控制選項|  
|SQL_ATTR_ROW_ARRAY_SIZE|每次提取中擷取的資料列數目|  
|SQL_ATTR_CURSOR_SENSITIVITY|顯示或不顯示其他連接對資料指標資料列所做之更新的資料指標|  
|SQL_ATTR_CURSOR_SCROLLABLE|可以前後捲動的資料指標|  
  
 這些屬性 (順向、唯讀、資料列集大小為 1) 的預設值不會使用伺服器資料指標。 若要使用伺服器資料指標，至少其中一個屬性必須設定為預設值以外的值，而且所執行的陳述式必須為單一 SELECT 陳述式或包含單一 SELECT 陳述式的預存程序。 使用伺服器資料指標時，SELECT 陳述式無法使用伺服器資料指標不支援的子句：COMPUTE、COMPUTE BY、FOR BROWSE 和 INTO。  
  
 您可以透過設定 SQL_ATTR_CURSOR_TYPE 和 SQL_ATTR_CONCURRENCY，或是設定 SQL_ATTR_CURSOR_SENSITIVITY 和 SQL_ATTR_CURSOR_SCROLLABLE，控制所使用的資料指標類型。 您不應該混合使用這兩種指定資料指標行為的方法。  
  
## <a name="example"></a>範例  
 下列範例會配置陳述式控制代碼、使用資料列版本設定開放式並行存取來設定動態資料指標類型，然後執行 SELECT。  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_DYNAMIC, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CONCURRENCY, SQLPOINTER)SQL_CONCUR_ROWVER, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, SELECT au_lname FROM authors", SQL_NTS);  
```  
  
## <a name="example"></a>範例  
 下列範例會配置陳述式控制代碼、設定可捲動的感應式資料指標，然後執行 SELECT。  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
  
// Set the cursor options and execute the statement.  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SCROLLABLE, SQLPOINTER)SQL_SCROLLABLE, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SENSITIVITY, SQLPOINTER)SQL_INSENSITIVE, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, select au_lname from authors", SQL_NTS);  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢的使用說明主題&#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  