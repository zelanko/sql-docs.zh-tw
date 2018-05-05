---
title: 核心層級的 API 函式 （如 Oracle 的 ODBC 驅動程式） |Microsoft 文件
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
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4135e192a2a97944ff455c72c76c136faaac4652
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>核心層級的 API 函式 （如 Oracle 的 ODBC 驅動程式）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 在此層級的函式組成 ODBC 驅動程式介面符合最低的層的級。  
  
|應用程式開發介面函式|注意|  
|------------------|-----------|  
|**SQLAllocConnect**|將記憶體配置連接控制代碼給*hdbc*，識別在環境內*henv*。 驅動程式管理員會處理此呼叫，並呼叫驅動程式的**SQLAllocConnect**函式每當**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**呼叫。|  
|**SQLAllocEnv**|顯示對話方塊，指定 Oracle 用戶端軟體的需求，然後傳回 SQL_NULL_HANDLE。 如果未安裝 Oracle 用戶端軟體，此函式會將記憶體配置環境控制代碼給*henv*，並初始化應用程式所使用的 ODBC 呼叫層級介面。|  
|**SQLAllocStmt**|將記憶體配置陳述式控制代碼，並將陳述式控制代碼與 hdbc 所指定的連接產生關聯。 驅動程式管理員會將傳遞 hstmt 結構配置記憶體的驅動程式，此呼叫。|  
|**SQLBindCol**|指派結果資料行的儲存空間，並指定結果的類型。|  
|**SQLCancel**|取消陳述式控制代碼，hstmt 上的處理。 在某些情況下，Oracle 不允許取消執行的陳述式。 這表示執行陳述式會繼續直到 Oracle 完成此程序，ODBC Driver for Oracle 取消的陳述式的結果。|  
|**SQLColAttributes**|在結果集中傳回的資料行的描述項資訊。 描述項資訊是以字元字串、 32 位元描述元相依值或整數值傳回。|  
|**SQLConnect**|連接到資料來源。 若要使用 Oracle 作業系統驗證，請指定"/"為*szUID*參數和""做為*szAuthStr*參數。|  
|**SQLDescribeCol**|傳回名稱、 類型、 有效位數、 小數位數，以及指定的結果資料行 null 屬性。 **注意：****SQLDescribeCol**報告為 SQL_VARCHAR 導出資料行。|  
|**SQLDisconnect**|關閉連接。 如果連接共用已啟用共用的環境，而且應用程式呼叫**SQLDisconnect**該環境中的連接，連接傳回連接集區且上仍可使用其他元件共用相同的環境。|  
|**SQLError**|傳回最後一個錯誤的錯誤或狀態資訊。 驅動程式會維護堆疊或在傳回的錯誤清單*hstmt*， *hdbc*，和*henv*引數，根據如何呼叫**SQLError**進行。 錯誤佇列會排清，每個陳述式之後。 通常擷取 Oracle 錯誤訊息，否則為空白。|  
|**SQLExecDirect**|執行新的、 已取消準備的 SQL 陳述式。 如果陳述式中存在的任何參數，驅動程式會使用目前的參數標記變數值。 如果您的資料表、 檢視或欄位名稱包含空格，括住名稱後方括號標記。 例如，如果您的資料庫包含名為的資料表*My Table*和欄位*My Field*，括住的識別項的每個項目如下所示：<br /><br /> 選取\`表格\`。 \`我 Field1\`，;\`表格\`。\`我 Field2\` FROM\`表格 '|  
|**SQLExecute**|執行已備妥的 SQL 陳述式 (已備妥的陳述式**SQLPrepare**)。 如果陳述式中存在的任何參數，驅動程式會使用目前的參數標記變數值。|  
|**SQLFetch**|從結果集置入先前呼叫所指定的位置擷取一個資料列**SQLBindCol**。 驅動程式會準備呼叫**SQLGetData**未繫結的資料行。|  
|**SQLFreeConnect**|釋放連接控制代碼，並釋放所有記憶體配置控制代碼。|  
|**SQLFreeEnv**|關閉 ODBC Driver for Oracle 並釋放與驅動程式相關聯的所有記憶體。|  
|**SQLFreeStmt**|停止特定 hstmt 相關聯的處理、 關閉任何開啟的資料指標相關聯的 hstmt、 捨棄暫止的結果，並選擇性地釋放陳述式控制代碼相關聯的所有資源。|  
|**SQLGetCursorName**|傳回給定 hstmt 相關聯的資料指標的名稱。|  
|**SQLNumResultCols**|在結果集資料指標中傳回資料行的數目。|  
|**SQLPrepare**|您可以規劃如何最佳化及執行陳述式準備的 SQL 陳述式。 SQL 陳述式會編譯執行**SQLExecDirect**。<br /><br /> 如果您的資料表、 檢視或欄位名稱包含空格，括住名稱後方括號標記。 例如，如果您的資料庫包含名為的資料表*My Table*和欄位*My Field*，括住的識別項的每個項目，如下所示：<br /><br /> 選取\`表格\`。\`My Field\` FROM\`表格 '<br /><br /> 使用結果集包含陣列做為型式參數的相關資訊，請參閱[從預存程序傳回陣列參數](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLRowCount**|Oracle 不提供一個方式來判斷結果集，直到擷取最後一個資料列之後，所以它會傳回 – 1 中的資料列數目。|  
|**SQLSetCursorName**|資料指標名稱關聯的使用中陳述式控制代碼， *hstmt*。|  
|**SQLSetParam**|SQLBindParameter ODBC 2 中被取代。*x*。|  
|**SQLTransact**|要求認可或回復作業上的所有陳述式控制代碼 (hstmts) 與連接相關聯的所有作用中作業或環境控制代碼相關聯的所有連線*henv*。 如果認可失敗，在手動模式中，交易會維持使用中。您可以選擇要回復交易，或重試認可操作。 如果在自動交易模式中，認可作業失敗，異動會自動回復;無法非使用中交易。|
