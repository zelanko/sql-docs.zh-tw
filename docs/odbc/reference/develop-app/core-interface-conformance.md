---
title: 核心介面一致性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e41d71cd3651e1db5d1a533159012b645b8c7764
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043755"
---
# <a name="core-interface-conformance"></a>核心介面一致性
所有的 ODBC 驅動程式必須提供至少核心層級介面一致性。 中大部分的泛型具互通性的應用程式所需的核心層級的功能，因為驅動程式可以使用這類應用程式。 ISO CLI 規格中定義的功能，並開啟群組 CLI 規格中定義的 nonoptional 功能，也對應中的核心層級的功能。 核心層級介面符合標準的 ODBC 驅動程式可讓應用程式執行下列各項：  
  
-   配置和釋放所有類型的控制代碼，藉由呼叫**SQLAllocHandle**並**SQLFreeHandle**。  
  
-   使用所有形式的**SQLFreeStmt**函式。  
  
-   將結果集資料行，藉由呼叫繫結**SQLBindCol**。  
  
-   處理動態參數，包括藉由呼叫的參數，僅會以輸入方向，陣列**SQLBindParameter**並**SQLNumParams**。 (輸出方向中的參數是功能在 203[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   指定的繫結位移。  
  
-   使用資料執行對話方塊中，包含要呼叫**SQLParamData**並**SQLPutData**。  
  
-   管理資料指標和資料指標名稱，請呼叫**SQLCloseCursor**， **SQLGetCursorName**，並**SQLSetCursorName**。  
  
-   取得結果集的存取權的描述 （中繼資料），藉由呼叫**SQLColAttribute**， **SQLDescribeCol**， **SQLNumResultCols**，和**SQLRowCount**. (使用以擷取書籤中繼資料的資料行編號 0 上的這些函式是功能在 204[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   呼叫目錄函數來查詢資料字典**SQLColumns**， **SQLGetTypeInfo**， **SQLStatistics**，以及**SQLTables**。  
  
     驅動程式不需要支援的資料庫資料表和檢視表的多部分名稱。 (如需詳細資訊，請參閱中的功能 101[層級 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)功能中的 201[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)不過，某些功能的 SQL-92 規格，例如限定資料行和索引的名稱是多部分命名語法類似。 ODBC 功能的存在清單不是導入的 SQL-92 到這些層面的新選項。  
  
-   管理資料來源和連線，請呼叫**SQLConnect**， **SQLDataSources**， **SQLDisconnect**，以及**SQLDriverConnect**。 取得有關驅動程式，不論哪一個 ODBC 層級支援，藉由呼叫**SQLDrivers**。  
  
-   準備和執行 SQL 陳述式，呼叫**SQLExecDirect**， **SQLExecute**，並**SQLPrepare**。  
  
-   擷取結果集的一個資料列或多個資料列，僅會以正向方向，藉由呼叫**SQLFetch**或來電 800-659-3579 **SQLFetchScroll**具有*Sqlfetchscroll*引數設定為 SQL_FETCH_NEXT。  
  
-   取得繫結的資料行在部分，藉由呼叫**SQLGetData**。  
  
-   取得目前的值的所有屬性，藉由呼叫**SQLGetConnectAttr**， **SQLGetEnvAttr**，並**SQLGetStmtAttr**，並將所有屬性都設定為其預設值和某些屬性設定為非預設值，藉由呼叫**SQLSetConnectAttr**， **SQLSetEnvAttr**，並**SQLSetStmtAttr**。  
  
-   管理特定欄位的描述元，藉由呼叫**SQLCopyDesc**， **SQLGetDescField**， **SQLGetDescRec**， **SQLSetDescField**，並**SQLSetDescRec**。  
  
-   取得診斷資訊，請藉由呼叫**SQLGetDiagField**並**SQLGetDiagRec**。  
  
-   偵測驅動程式功能，藉由呼叫**SQLGetFunctions**並**SQLGetInfo**。 此外，偵測它傳送至資料來源，藉由呼叫之前的 SQL 陳述式所做的任何文字替換作業的結果**SQLNativeSql**。  
  
-   使用的語法**SQLEndTran**認可的交易。 核心層級驅動程式不需要支援，則為 true 的交易;因此，應用程式不能指定 SQL_ROLLBACK 也 SQL_AUTOCOMMIT_OFF SQL_ATTR_AUTOCOMMIT 連接屬性。 (如需詳細資訊，請參閱中的功能 109[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   呼叫**SQLCancel**取消資料在執行對話方塊並在多執行緒環境中，若要取消 ODBC 函式正在執行 」，另一個執行緒。 核心層級介面一致性不會要求的非同步執行的函式或使用支援**SQLCancel**取消非同步執行的 ODBC 函式。 平台和 ODBC 驅動程式都不需要是多執行緒的驅動程式同時執行獨立的活動。 不過，在多執行緒環境中，ODBC 驅動程式必須是安全執行緒。 從應用程式要求的序列化是符合標準方式來實作此規格中，即使它可能會產生嚴重的效能問題。  
  
-   取得 SQL_BEST_ROWID 資料列識別資料行的資料表，藉由呼叫**SQLSpecialColumns**。 (支援 SQL_ROWVER 是功能在 208[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
    > [!IMPORTANT]  
    >  ODBC 驅動程式必須實作的函式中的核心介面一致性層級。
