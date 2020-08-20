---
description: 核心介面一致性
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
ms.openlocfilehash: 1ca38e2b616c39839cfe813dad984f7eba3796a6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465840"
---
# <a name="core-interface-conformance"></a>核心介面一致性
所有 ODBC 驅動程式都必須展示至少核心層級的介面一致性。 由於核心層級中的功能是大部分泛型互通應用程式所需的功能，因此驅動程式可以與這類應用程式搭配使用。 核心層級中的功能也會與 ISO CLI 規格中定義的功能以及 Open Group CLI 規格中定義的 nonoptional 功能相對應。 核心層級的介面一致 ODBC 驅動程式可讓應用程式執行下列作業：  
  
-   藉由呼叫 **SQLAllocHandle** 和 **SQLFreeHandle**，配置並釋放所有類型的控制碼。  
  
-   使用 **SQLFreeStmt** 函數的所有形式。  
  
-   藉由呼叫 **SQLBindCol**來系結結果集資料行。  
  
-   藉由呼叫 **SQLBindParameter** 和 **SQLNumParams**，只處理輸入方向的動態參數，包括參數陣列。 輸出方向的 (參數是 [層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能203。 )   
  
-   指定系結位移。  
  
-   使用「資料執行中」對話方塊，其中涉及 **SQLParamData** 和 **SQLPutData**的呼叫。  
  
-   藉由呼叫 **SQLCloseCursor**、 **SQLGetCursorName**和 **SQLSetCursorName**來管理資料指標和資料指標名稱。  
  
-   藉由呼叫 **SQLColAttribute**、 **SQLDescribeCol**、 **SQLNumResultCols**和 **SQLRowCount**，取得結果集 (中繼資料) 的存取權。  (在資料行編號0上使用這些函數來取得書簽中繼資料，則為 [層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能204。 )   
  
-   藉由呼叫目錄函數 **SQLColumns**、 **SQLGetTypeInfo**、 **SQLStatistics**和 **SQLTables**來查詢資料字典。  
  
     不需要驅動程式，就能支援資料庫資料表和 views 的多部分名稱。  (如需詳細資訊，請參閱層級 [1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md) 中的功能101和 [層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的特徵201。 ) 不過，SQL-92 規格的某些功能（例如資料行限定性和索引名稱）在語法上與多部分命名相同。 ODBC 功能的目前清單不是為了在 SQL-92 的這些方面引進新選項。  
  
-   藉由呼叫 **SQLConnect**、 **SQLDataSources**、 **SQLDisconnect**和 **SQLDriverConnect**，來管理資料來源和連接。 藉由呼叫 **SQLDrivers**，取得驅動程式的相關資訊，不論它們支援哪個 ODBC 層級。  
  
-   藉由呼叫 **SQLExecDirect**、 **SQLExecute**和 **SQLPrepare**，來準備和執行 SQL 語句。  
  
-   藉由呼叫 **SQLFetch** 或呼叫 **SQLFetchScroll** 並將 *FetchOrientation* 引數設定為 SQL_FETCH_NEXT，來提取結果集的一個資料列或多個資料列（以正向方向）。  
  
-   藉由呼叫 **SQLGetData**，在元件中取得未系結的資料行。  
  
-   藉由呼叫 **SQLGetConnectAttr**、 **SQLGetEnvAttr**和 **SQLGetStmtAttr**來取得所有屬性的目前值，並將所有屬性設為其預設值，然後藉由呼叫 **SQLSetConnectAttr**、 **SQLSetEnvAttr**和 **SQLSetStmtAttr**，將某些屬性設定為非預設值。  
  
-   藉由呼叫 **SQLCopyDesc**、 **SQLGetDescField**、 **SQLGetDescRec**、 **SQLSetDescField**和 **SQLSetDescRec**，來操作描述項的某些欄位。  
  
-   藉由呼叫 **SQLGetDiagField** 和 **SQLGetDiagRec**來取得診斷資訊。  
  
-   藉由呼叫 **SQLGetFunctions** 和 **SQLGetInfo**來偵測驅動程式功能。 此外，也會藉由呼叫 **SQLNativeSql**，在將 SQL 語句傳送到資料來源之前，偵測對其進行之任何文字替換的結果。  
  
-   使用 **SQLEndTran** 的語法來認可交易。 核心層級的驅動程式不需要支援真正的交易;因此，應用程式無法為 SQL_ATTR_AUTOCOMMIT 連接屬性指定 SQL_ROLLBACK 或 SQL_AUTOCOMMIT_OFF。  (如需詳細資訊，請參閱 [層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能109。 )   
  
-   呼叫 **SQLCancel** 可取消在多執行緒環境中執行的資料執行對話方塊和，以取消在另一個執行緒中執行的 ODBC 函數。 核心層級介面一致性不會支援非同步執行函式的支援，也不會使用 **SQLCancel** 來取消以非同步方式執行的 ODBC 函數。 平臺或 ODBC 驅動程式都不需要多執行緒，驅動程式就能同時執行獨立的活動。 不過，在多執行緒環境中，ODBC 驅動程式必須是安全線程。 來自應用程式的要求序列化是符合執行此規格的方式，即使它可能會造成嚴重的效能問題。  
  
-   藉由呼叫 **SQLSpecialColumns**，取得資料表的 SQL_BEST_ROWID 資料列識別資料行。  (支援 SQL_ROWVER 在 [層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中為功能208。 )   
  
    > [!IMPORTANT]  
    >  ODBC 驅動程式必須在核心介面一致性層級中執行函數。
