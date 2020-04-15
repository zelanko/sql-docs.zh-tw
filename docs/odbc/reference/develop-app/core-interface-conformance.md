---
title: 核心介面一致性 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302130"
---
# <a name="core-interface-conformance"></a>核心介面一致性
所有 ODBC 驅動程式必須至少顯示核心級介面一致性。 由於 Core 級別的功能是大多數通用可互通應用程式所需的功能,因此驅動程式可以使用此類應用程式。 核心等級的功能也對應於 ISO CLI 規範中定義的功能以及開放組 CLI 規範中定義的非可選功能。 核心級介面一致的 ODBC 驅動程式允許應用程式執行以下所有操作:  
  
-   通過調用**SQLAllocHandle**和**SQLFreeHandle**來分配和釋放所有類型的句柄。  
  
-   使用**SQLFreeStmt**函數的所有形式。  
  
-   通過調用**SQLBindCol**綁定結果集列。  
  
-   僅透過呼叫**SQLBind 參數**和**SQLNumParams**處理動態參數(包括參數陣列)。 (輸出方向的參數是[2 級介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的要素 203 。  
  
-   指定綁定偏移量。  
  
-   使用執行時的數據對話框,涉及對**SQLParamData**和**SQLPutData**的調用。  
  
-   通過呼叫**SQLCloseCursor、SQLGetCursorName**和**SQLSetCursorName**來管理游標和**SQLCloseCursor**游標名稱。  
  
-   通過調用 SQLColattribute、SQLDescribeCol、SQLNumResultCols**SQLDescribeCol**和**SQLRowCount,** 訪問結果集的描述(**SQLColAttribute****SQLNumResultCols**中繼資料)。 (在列號 0 上使用這些函數來檢索書簽元數據是[2 級介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能 204 。  
  
-   通過調用目錄函數**SQLColumns、SQLGetTypeInfo、SQL****SQLColumns****統計**和**SQLTables**查詢資料字典。  
  
     不需要驅動程式來支援資料庫表和檢視的多部分名稱。 (有關詳細資訊,請參閱[級別 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)中的要素 101 和 2[級介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能 201 。但是,SQL-92 規範的某些功能(如列限定和索引名稱)在語法上可與多部分命名相媲美。 本 ODBC 功能清單無意在 SQL-92 的這些方面引入新選項。  
  
-   通過調用**SQLConnect** **、SQLDataSources、SQL****斷開連接**和**SQLDriverConnect**來管理數據源和連接。 通過調用**SQLDrivers**獲取有關驅動程式的資訊,無論他們支援哪個 ODBC 級別。  
  
-   通過調用**SQLExecDirect、SQLExecute**和**SQLExecute****SQLPrepare**來準備和執行 SQL 語句。  
  
-   僅按正向方向獲取結果集的一行或多行,通過調用**SQLFetch**或調用**SQLFetchScroll,** 將*Fetch 方向*參數設置為SQL_FETCH_NEXT。  
  
-   通過調用**SQLGetData,** 獲取部分未綁定列。  
  
-   通過調用**SQLGetConnectAttr、SQLGetEnvAttr**和**SQLGetStmtAttr**獲取所有屬性的當前值,並將所有屬性設置為其預設值,並透過調用**SQLSetConnectAttr、SQLSetEnv Attr**和**SQLGetEnvAttr****SQLSetStmtAttr****SQLSetEnvAttr**將某些屬性設置為非預設值。  
  
-   用 SQLCopyDesc、SQLGetDescField、SQLGetDescRec、SQLSetDescField 與**SQLSetDescRec,** 操作描述符號的某些**SQLCopyDesc****SQLGetDescField****SQLGetDescRec****欄位**。  
  
-   通過調用**SQLGetDiagField**和**SQLGetDiagRec**獲取診斷資訊。  
  
-   通過調用**SQLGet 函數**和**SQLGetInfo 來**檢測驅動程式功能。 此外,通過調用**SQLNativeSql,** 在 SQL 語句發送到數據源之前,檢測對 SQL 語句所做的任何文本替換的結果。  
  
-   使用**SQLEndTran**的語法提交事務。 核心級驅動程式不需要支援真正的事務;因此,應用程式不能為SQL_ATTR_AUTOCOMMIT連接屬性指定SQL_ROLLBACK或SQL_AUTOCOMMIT_OFF。 (有關詳細資訊,請參閱[2 級介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能 109 。  
  
-   調用**SQLCancel**以取消執行時的資料對話框,並在多線程環境中取消在另一個線程中執行的 ODBC 函數。 核心級介面一致性不要求支援非同步執行函數,也不要求使用**SQLCancel**取消非同步執行的 ODBC 函數。 平臺和ODBC驅動程式都不需要多線程,以便驅動程式同時進行獨立活動。 但是,在多線程環境中,ODBC 驅動程式必須是線程安全的。 應用程式請求的序列化是實現此規範的一種一致方法,即使它可能會造成嚴重的性能問題。  
  
-   通過調用**SQL 特別列**獲取表的SQL_BEST_ROWID行標識列。 ( 支援SQL_ROWVER是[2 層介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的功能 208 。  
  
    > [!IMPORTANT]  
    >  ODBC 驅動程式必須實現核心介面一致性級別的功能。
