---
title: 使用陳述式 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC]
ms.assetid: f7573f8f-6f21-4e03-8dd5-a5f2ea4878cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 195b38804045c26053771d263d650cfaa2efecde
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227008"
---
# <a name="use-a-statement-odbc"></a>使用陳述式 (ODBC)
    
### <a name="to-use-a-statement"></a>使用陳述式  
  
1.  利用 SQL_HANDLE_STMT 的 *HandleType* 來呼叫 [SQLAllocHandle](http://go.microsoft.com/fwlink/?LinkId=58396)，以配置陳述式控制代碼。  
  
2.  您可以選擇呼叫 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) 來設定陳述式選項，或是呼叫 [SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md) 來取得陳述式屬性。  
  
     若要使用伺服器資料指標，您必須將資料指標屬性設定為預設值以外的值。  
  
3.  如果此陳述式將會執行數次，您可以選擇預備此陳述式搭配 [SQLPrepare 函數](http://go.microsoft.com/fwlink/?LinkId=59360)一起執行。  
  
4.  如果此陳述式已經繫結參數標記，您可以選擇使用 [SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md) 將這些參數標記繫結至程式變數。 如果此陳述式已備妥，您可以呼叫 [SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404) 和 [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md) 來尋找參數的數目和參數的特性。  
  
5.  使用 SQLExecDirect 直接執行陳述式  
  
     \-或-  
  
     如果此陳述式已備妥，請使用 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) 將它執行多次。  
  
     \-或-  
  
     呼叫目錄函數，這樣會傳回結果。  
  
6.  若要處理結果，請將結果集資料行繫結至程式變數、使用 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 將資料從結果集資料行中移到程式變數，或是結合這兩個方法。  
  
     透過陳述式的結果集一次提取一個資料列。  
  
     \-或-  
  
     透過結果集，利用區塊資料指標一次提取數個資料列。  
  
     \-或-  
  
     呼叫 [SQLRowCount](../../native-client-odbc-api/sqlrowcount.md) 來判斷受到 INSERT、UPDATE 或 DELETE 陳述式影響的資料列數。  
  
     如果 SQL 陳述式可以有多個結果集，請在每一個結果集的結尾呼叫 [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md)，以查看是否有其他結果集要處理。  
  
7.  處理完結果之後，可能需要採取以下動作，以便提供陳述式控制代碼來執行新的陳述式：  
  
    -   如果您要等到它傳回 SQL_NO_DATA 之後才會呼叫 [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md)，請呼叫 [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) 來關閉此資料指標。  
  
    -   如果您將參數標記繫結至程式變數，請呼叫 [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) 並將 *Option* 設定為 SQL_RESET_PARAMS，以釋放繫結參數。  
  
    -   如果您將結果集資料行繫結至程式變數，請呼叫 [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) 並將 *Option* 設定為 SQL_UNBIND，以釋放繫結的資料行。  
  
    -   若要重複使用陳述式控制代碼，請移至步驟 2。  
  
8.  使用 SQL_HANDLE_STMT 的 *HandleType* 呼叫 [SQLFreeHandle](../../native-client-odbc-api/sqlfreehandle.md)，以釋放陳述式控制代碼。  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢使用說明主題&#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
