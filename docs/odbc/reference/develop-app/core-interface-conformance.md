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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 886ded1cd79b35488c0d47df3dbd8055dc6a8016
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302130"
---
# <a name="core-interface-conformance"></a>核心介面一致性
所有 ODBC 驅動程式都必須展現至少核心層級的介面一致性。 由於核心層級中的功能是大部分一般互通應用程式所需的功能，因此驅動程式可以使用這類應用程式。 核心層級中的功能也會對應至 ISO CLI 規格中定義的功能，以及「開啟群組 CLI」規格中所定義的 nonoptional 功能。 符合核心層級介面的 ODBC 驅動程式可讓應用程式執行下列所有動作：  
  
-   藉由呼叫**SQLAllocHandle**和**SQLFreeHandle**，配置並釋放所有類型的控制碼。  
  
-   使用**SQLFreeStmt**函數的所有形式。  
  
-   藉由呼叫**SQLBindCol**來系結結果集資料行。  
  
-   藉由呼叫**SQLBindParameter**和**SQLNumParams**，僅在輸入方向處理動態參數（包括參數陣列）。 （輸出方向的參數是[層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能203）。  
  
-   指定系結位移。  
  
-   使用 [資料執行中] 對話方塊，其中涉及對**SQLParamData**和**SQLPutData**的呼叫。  
  
-   藉由呼叫**SQLCloseCursor**、 **SQLGetCursorName**和**SQLSetCursorName**來管理資料指標和資料指標名稱。  
  
-   藉由呼叫**SQLColAttribute**、 **SQLDescribeCol**、 **SQLNumResultCols**和**SQLRowCount**，取得結果集的描述（中繼資料）存取權。 （在資料行編號0上使用這些函數，以取得[第2層介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能204。）  
  
-   藉由呼叫目錄函數**SQLColumns**、 **SQLGetTypeInfo**、 **SQLStatistics**和**SQLTables**來查詢資料字典。  
  
     驅動程式不需要支援資料庫資料表和 views 的多部分名稱。 （如需詳細資訊，請參閱[層級1介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)中的功能101和[層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能201）。不過，SQL-92 規格的某些功能（例如資料行限定性和索引名稱）在語法上相當於多部分命名。 ODBC 功能的目前清單並不是為了在 SQL-92 的這些層面引進新的選項。  
  
-   藉由呼叫**SQLConnect**、 **SQLDataSources**、 **SQLDisconnect**和**SQLDriverConnect**來管理資料來源和連接。 藉由呼叫**SQLDrivers**，取得驅動程式的相關資訊，不論它們支援哪個 ODBC 層級。  
  
-   藉由呼叫**SQLExecDirect**、 **SQLExecute**和**SQLPREPARE**來準備和執行 SQL 語句。  
  
-   藉由呼叫**SQLFetch**或呼叫**SQLFetchScroll**並將*FetchOrientation*引數設定為 SQL_FETCH_NEXT，只提取結果集的一個資料列或多個資料列。  
  
-   藉由呼叫**SQLGetData**，取得部分中未系結的資料行。  
  
-   藉由呼叫**SQLGetConnectAttr**、 **SQLGetEnvAttr**和**SQLGetStmtAttr**，取得所有屬性的目前值，並將所有屬性設為其預設值，並藉由呼叫**SQLSetConnectAttr**、 **SQLSetEnvAttr**和**SQLSetStmtAttr**，將某些屬性設定為非預設值。  
  
-   藉由呼叫**SQLCopyDesc**、 **SQLGetDescField**、 **SQLGetDescRec**、 **SQLSetDescField**和**SQLSetDescRec**來操作描述項的特定欄位。  
  
-   藉由呼叫**SQLGetDiagField**和**SQLGetDiagRec**來取得診斷資訊。  
  
-   藉由呼叫**SQLGetFunctions**和**SQLGetInfo**來偵測驅動程式功能。 此外，也會藉由呼叫**SQLNativeSql**，在將 SQL 語句傳送至資料來源之前，偵測任何文字替換的結果。  
  
-   使用**SQLEndTran**的語法來認可交易。 核心層級的驅動程式不需要支援真正的交易;因此，應用程式無法為 SQL_ATTR_AUTOCOMMIT 連接屬性指定 SQL_ROLLBACK 或 SQL_AUTOCOMMIT_OFF。 （如需詳細資訊，請參閱[層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能109）。  
  
-   呼叫**SQLCancel**以取消資料執行中的對話方塊，並在多執行緒環境中取消在另一個執行緒中執行的 ODBC 函數。 核心層級介面一致性不會強制支援非同步執行函式，也不會使用**SQLCancel**來取消以非同步方式執行的 ODBC 函數。 平臺或 ODBC 驅動程式都不需要多執行緒，驅動程式也可以同時執行獨立的活動。 不過，在多執行緒環境中，ODBC 驅動程式必須是安全線程。 來自應用程式的要求序列化是執行此規格的一致方式，即使它可能會造成嚴重的效能問題也一樣。  
  
-   藉由呼叫**SQLSpecialColumns**，取得資料表的 SQL_BEST_ROWID 資料列識別資料行。 （支援 SQL_ROWVER 是[層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能208）。  
  
    > [!IMPORTANT]  
    >  ODBC 驅動程式必須實作用於核心介面一致性層級中的函式。
