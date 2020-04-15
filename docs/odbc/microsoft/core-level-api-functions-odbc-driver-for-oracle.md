---
title: 核心級 API 功能(Oracle 的 ODBC 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19751bb6d0556b117d0a73967d4db00c408733ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281018"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>核心層級 API 函式 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 此等級的功能包括 ODBC 驅動程式的最小介面一致性級別。  
  
|API 功能|注意|  
|------------------|-----------|  
|**SQLAlloc 連線**|在*henv*標識的環境中為連接句柄*hdbc*分配記憶體。 驅動程式管理員處理此調用,並在調用**SQLConnect、SQLBrowseConnect**或**SQLConnect****SQLDriverConnect**時調用驅動程式的**SQLAllocConnect**函數。|  
|**SQLAllocEnv**|顯示一個對話框,指定 Oracle 用戶端軟體的要求,然後返回SQL_NULL_HANDLE。 如果未安裝 Oracle 用戶端軟體,此函數將記憶體分配給環境句柄*henv,* 並初始化 ODBC 調用級介面供應用程式使用。|  
|**SQLAllocStmt**|為語句句柄分配記憶體,並將語句句柄與 hdbc 指定的連接關聯。 驅動程式管理員將此調用傳遞給驅動程式,驅動程式為 hstmt 結構分配記憶體。|  
|**SQLBindCol**|為結果列分配存儲空間並指定結果的類型。|  
|**SQLCancel**|取消語句句柄上的處理,hstmt。 在某些情況下,Oracle 不允許取消正在運行的語句。 這意味著運行語句將繼續,直到 Oracle 完成該過程,此時來自語句的結果將由 Oracle 的 ODBC 驅動程式取消。|  
|**SQLColattributes**|返回結果集中列的描述符資訊。 描述符資訊將作為字串、32 位描述符相關值或整數值返回。|  
|**SQLConnect**|連接到數據源。 要使用 Oracle 作業系統認證,請指定/"作為*szUID*參數,「"""作為*szAuthStr 參數*。|  
|**SQLDescribeCol**|返回給定結果列的名稱、類型、精度、比例和空度。 **注意:SQLDescribeCol**將計算的列報告為SQL_VARCHAR。|  
|**SQL 斷線**|關閉連接。 如果為共用環境啟用了連接池,並且應用程式在該環境中的連接上調用**SQLDisconnect,** 則連接將返回到連接池,並且仍然可用於使用相同的共享環境的其他元件。|  
|**SQLError**|返回有關上次錯誤的錯誤或狀態資訊。 驅動程式維護一個堆疊或錯誤列表,這些錯誤可以返回*用於 hstmt、hdbc*和*henv*參數,具體取決於對**SQLError**的調用方式。 *hdbc* 在每個語句之後刷新錯誤佇列。 通常檢索 Oracle 錯誤訊息,否則為空。|  
|**SQLExecDirect**|執行新的、未準備好的 SQL 語句。 如果語句中存在任何參數,驅動程式將使用參數標記變數的當前值。 如果表、檢視或欄位名稱包含空格,請將名稱包含在回引號中。 例如,如果資料庫包含名為 *「我的表」的表*和欄位 *「我的欄位」,* 則將識別符的每個元素都包含在內,如下所示:<br /><br /> 選擇\`我的\`表格 。 \`我的欄位1,;\`\`我的桌子\`。\`我的欄位2\`從\`我的 表格\`|  
|**SQLExecute**|執行準備好的 SQL 語句(由**SQLPrepare**編寫的語句)。 如果語句中存在任何參數,驅動程式將使用參數標記變數的當前值。|  
|**SQLFetch**|從結果集中檢索到以前調用**SQLBindCol**指定的位置中的一行。 為調用**SQLGetData**為未綁定列準備驅動程式。|  
|**SQLFreeConnect**|釋放連接句柄並釋放為該句柄分配的所有記憶體。|  
|**SQLFreeEnv**|關閉 Oracle 的 ODBC 驅動程式並釋放與驅動程式關聯的所有記憶體。|  
|**SQLFreeStmt**|停止與特定 hstmt 關聯的處理,關閉與 hstmt 關聯的任何打開的游標,丟棄掛起的結果,並可以選擇釋放與語句句柄關聯的所有資源。|  
|**SQLGetCursorName**|返回與給定 hstmt 關聯的游標的名稱。|  
|**SQLNumResultCols**|返回結果集游標中的列數。|  
|**SQLPrepare**|通過規劃如何優化和執行該語句來準備 SQL 語句。 SQL 語句編譯供**SQLExecDirect**執行。<br /><br /> 如果表、檢視或欄位名稱包含空格,請將名稱包含在回引號中。 例如,如果資料庫包含名為 *「我的表*」的表和欄位 *「我的欄位」,* 則將識別符的每個元素包含如下:<br /><br /> 選擇\`我的\`表格 。\`我的欄位\`從\`我的 表格\`<br /><br /> 有關使用包含數位式作為正式參數的結果集的資訊,請參閱[從儲存過程傳回陣列參數](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLRowCount**|Oracle 不提供一種方法來確定結果集中的行數,直到提取最後一行之後,因此返回 -1。|  
|**SQLSetCursor 名稱**|將游標名稱與活動語句句柄*hstmt*關聯。|  
|**SQLSetParam**|在 ODBC 2 中替換為 SQLBind 參數。*x*. .|  
|**SQLTransact**|請求所有與連接關聯的語句句柄 (hstmts) 或與環境句柄關聯的所有連接*henv*的所有活動操作的提交或回滾操作。 如果在手動模式下提交失敗,則事務將保持活動狀態;如果提交處於手動模式下,則事務將保持活動狀態。您可以選擇回滾事務或重試提交操作。 如果在自動事務模式下提交操作失敗,則事務將自動回滾;事務不能處於非活動狀態。|
