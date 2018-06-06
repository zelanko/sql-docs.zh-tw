---
title: 核心介面一致性 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c45fdfe2b01ddfd34e7db391b799b95ce696da8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="core-interface-conformance"></a>核心介面一致性
所有的 ODBC 驅動程式必須呈現出至少核心層級介面一致性。 因為核心層級中的功能所需的大部分的泛型互通的應用程式，此驅動程式可以使用這類應用程式。 核心層級中的功能也會對應至 ISO CLI 規格中定義的功能和 nonoptional 開啟群組 CLI 規格中定義的功能。 核心層級介面標準 ODBC 驅動程式可讓應用程式執行下列各項：  
  
-   配置和釋放所有類型的控制代碼，藉由呼叫**SQLAllocHandle**和**SQLFreeHandle**。  
  
-   使用所有形式的**SQLFreeStmt**函式。  
  
-   將結果集資料行，藉由呼叫繫結**SQLBindCol**。  
  
-   處理動態參數，包括中的參數，僅輸入方向的陣列，藉由呼叫**SQLBindParameter**和**SQLNumParams**。 (輸出方向中的參數是功能中的 203[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   指定的繫結的位移。  
  
-   使用資料執行在對話方塊中，包含呼叫**SQLParamData**和**SQLPutData**。  
  
-   管理資料指標和資料指標名稱，請呼叫**SQLCloseCursor**， **SQLGetCursorName**，和**SQLSetCursorName**。  
  
-   取得存取權的描述 （中繼資料） 的結果集，藉由呼叫**SQLColAttribute**， **SQLDescribeCol**， **SQLNumResultCols**，和**SQLRowCount**. (這些函數來擷取書籤中繼資料的資料行編號 0 上的使用是功能中的 204[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   呼叫目錄函數來查詢資料字典**SQLColumns**， **SQLGetTypeInfo**， **SQLStatistics**，和**SQLTables**。  
  
     驅動程式不需要支援多個資料庫資料表和檢視表的名稱。 (如需詳細資訊，請參閱中的功能 101[層級 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)功能中的 201[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)不過的多部分命名語法相當 sql-92 規格，例如限定資料行和名稱的索引，某些功能。 ODBC 功能的存在清單不是導入的 SQL 92 這些層面的新選項。  
  
-   管理資料來源和連接，請呼叫**SQLConnect**， **SQLDataSources**， **SQLDisconnect**，和**SQLDriverConnect**。 取得有關驅動程式，不論哪一個 ODBC 層級支援，藉由呼叫**SQLDrivers**。  
  
-   準備和執行 SQL 陳述式，呼叫**SQLExecDirect**， **SQLExecute**，和**SQLPrepare**。  
  
-   藉由呼叫擷取結果集的一個資料列或多個資料列，只有，正向方向**SQLFetch**或藉由呼叫**SQLFetchScroll**與*Sqlfetchscroll*引數設定為 SQL_FETCH_NEXT。  
  
-   取得組件中的未繫結資料行，藉由呼叫**SQLGetData**。  
  
-   取得目前的值之所有屬性，藉由呼叫**SQLGetConnectAttr**， **SQLGetEnvAttr**，和**SQLGetStmtAttr**，並將所有屬性都設定為其預設值和某些屬性設定為非預設值，藉由呼叫**SQLSetConnectAttr**， **SQLSetEnvAttr**，和**SQLSetStmtAttr**。  
  
-   管理特定欄位的描述項，藉由呼叫**SQLCopyDesc**， **SQLGetDescField**， **SQLGetDescRec**， **SQLSetDescField**，和**SQLSetDescRec**。  
  
-   取得診斷資訊，藉由呼叫**SQLGetDiagField**和**SQLGetDiagRec**。  
  
-   偵測驅動程式功能，藉由呼叫**SQLGetFunctions**和**SQLGetInfo**。 此外，偵測它傳送至資料來源，藉由呼叫之前的 SQL 陳述式所做的任何文字替換作業的結果**SQLNativeSql**。  
  
-   使用的語法**SQLEndTran**認可交易。 核心層級驅動程式不需要支援，則為 true 的交易。因此，應用程式無法指定 SQL_ROLLBACK 也 SQL_AUTOCOMMIT_OFF SQL_ATTR_AUTOCOMMIT 連接屬性。 (如需詳細資訊，請參閱中的功能 109[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
-   呼叫**SQLCancel**取消資料在執行對話方塊和在多執行緒環境中，若要取消 ODBC 函式必須執行另一個執行緒。 核心層級介面一致性不會要求的非同步執行的函式，也不是使用支援**SQLCancel**取消 ODBC 函數以非同步方式執行。 平台和 ODBC 驅動程式都不需要是多執行緒的驅動程式同時進行獨立的活動。 不過，在多執行緒環境中，ODBC 驅動程式必須是安全執行緒。 從應用程式要求的序列化是一致的方式來實作此規格中，即使它可能會產生嚴重的效能問題。  
  
-   取得 SQL_BEST_ROWID 資料列識別資料行的資料表，藉由呼叫**SQLSpecialColumns**。 (SQL_ROWVER 支援功能的中的 208[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)  
  
    > [!IMPORTANT]  
    >  ODBC 驅動程式必須實作函式中的核心介面一致性層級。
