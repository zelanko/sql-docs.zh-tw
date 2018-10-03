---
title: 核心層級 API 函式 (ODBC Driver for Oracle) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ead4e816049f6dcce6bfc560a60d8f8bafa9d61c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724686"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>核心層級 API 函式 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 在此層級的函式由 ODBC 驅動程式介面一致性的最低層級所組成。  
  
|API 函式|注意|  
|------------------|-----------|  
|**SQLAllocConnect**|配置連接控制代碼，記憶體*hdbc*，由識別環境內*henv*。 驅動程式管理員會處理此呼叫，並呼叫的驅動程式**SQLAllocConnect**函式每當**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**呼叫。|  
|**SQLAllocEnv**|顯示對話方塊，指定 Oracle 用戶端軟體的需求，然後傳回 SQL_NULL_HANDLE。 如果未安裝 Oracle 用戶端軟體，此函式會配置的記憶體環境控制代碼*henv*，並初始化應用程式使用的 ODBC 呼叫層級介面。|  
|**SQLAllocStmt**|會配置陳述式控制代碼的記憶體，並關聯 hdbc 所指定的連接中的陳述式控制代碼。 驅動程式管理員會傳遞給驅動程式會將記憶體配置 hstmt 結構的這個呼叫。|  
|**SQLBindCol**|指派結果資料行的儲存空間，並指定結果的型別。|  
|**SQLCancel**|取消陳述式控制代碼，hstmt 上的處理。 在某些情況下，Oracle 不允許取消執行的陳述式。 這表示執行的陳述式，將會繼續直到 Oracle 完成此程序，ODBC Driver for Oracle 取消這段陳述式的結果。|  
|**SQLColAttributes**|在結果集中傳回的資料行的描述項資訊。 為字元字串、 32 位元描述元相依值或整數值，會傳回描述元資訊。|  
|**SQLConnect**|連接到資料來源。 若要使用 Oracle 作業系統驗證，請指定"/"作為*szUID*參數和 「"作為*szAuthStr*參數。|  
|**SQLDescribeCol**|傳回名稱、 類型、 有效位數、 小數位數和指定的結果資料行 null 屬性。 **注意︰****SQLDescribeCol**報告為 SQL_VARCHAR 的導出資料行。  |  
|**SQLDisconnect**|關閉連接。 如果連接共用已啟用共用的環境，而且應用程式呼叫**SQLDisconnect**在該環境中連接之後，連接傳回連接集區並仍可使用其他元件相同的共用的環境中。|  
|**SQLError**|傳回最後一個錯誤的錯誤或狀態資訊。 驅動程式會維護的堆疊或可針對傳回的錯誤清單*hstmt*， *hdbc*，並*henv*引數，視呼叫**SQLError**為止。 錯誤佇列中排清每個陳述式之後。 通常擷取 Oracle 錯誤訊息，並為空白。|  
|**SQLExecDirect**|執行新的、 已取消準備的 SQL 陳述式。 如果陳述式中存在的任何參數，驅動程式會使用參數標記變數的目前值。 如果您的資料表、 檢視或欄位名稱包含空格，括住名稱後引號標記。 比方說，如果您的資料庫包含名為資料表*My Table*和欄位*My Field*，括住識別項的每個項目就像這樣：<br /><br /> 選取 \`表格\`。 \`我 Field1\`，;\`表格\`。\`我 Field2\` FROM\`表格 '|  
|**SQLExecute**|執行已備妥的 SQL 陳述式 (已備妥的陳述式**SQLPrepare**)。 如果陳述式中存在的任何參數，驅動程式會使用參數標記變數的目前值。|  
|**SQLFetch**|擷取結果集的先前呼叫所指定的位置中的一個資料列**SQLBindCol**。 準備驅動程式呼叫**SQLGetData**未繫結的資料行。|  
|**SQLFreeConnect**|釋放連接控制代碼，並釋放所有記憶體配置控制代碼。|  
|**SQLFreeEnv**|關閉 ODBC Driver for Oracle 並釋放與驅動程式相關聯的所有記憶體。|  
|**SQLFreeStmt**|停止特定 hstmt 相關聯的處理、 關閉任何開啟的資料指標相關聯的 hstmt、 捨棄暫止的結果，並選擇性地釋放陳述式控制代碼相關聯的所有資源。|  
|**SQLGetCursorName**|傳回與指定的 hstmt 相關聯的資料指標名稱。|  
|**SQLNumResultCols**|在結果集資料指標中傳回資料行的數目。|  
|**SQLPrepare**|規劃如何最佳化和執行陳述式會準備 SQL 陳述式。 執行 SQL 陳述式編譯**SQLExecDirect**。<br /><br /> 如果您的資料表、 檢視或欄位名稱包含空格，括住名稱後引號標記。 例如，如果您的資料庫包含名為資料表*My Table*和欄位*My Field*，括住識別項的每個項目，如下所示：<br /><br /> 選取 \`表格\`。\`My Field\` FROM\`表格 '<br /><br /> 如需使用結果集包含與型式參數的陣列，請參閱[從預存程序傳回陣列參數](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLRowCount**|Oracle 不提供一個方式來判斷結果集，直到擷取最後一個資料列之後，所以它會傳回 – 1 中的資料列數目。|  
|**SQLSetCursorName**|將資料指標名稱關聯到作用中陳述式控制代碼*hstmt*。|  
|**SQLSetParam**|SQLBindParameter ODBC 2 中被取代。*x*。|  
|**SQLTransact**|要求認可或回復作業的所有陳述式控制代碼 (hstmt) 與連接相關聯的所有作用中作業，或環境控制代碼相關聯的所有連線*henv*。 如果認可失敗，在手動模式中，交易會維持使用中;您可以選擇要回復交易，或重試認可作業。 如果認可作業失敗時在自動的交易模式下，異動會自動回復;交易不可為非作用中。|
