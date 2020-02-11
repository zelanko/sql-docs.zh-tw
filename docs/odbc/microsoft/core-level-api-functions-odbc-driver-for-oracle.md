---
title: 核心層級 API 函式（ODBC Driver for Oracle） |Microsoft Docs
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
ms.openlocfilehash: cc95ec17dc221cb77bd94fc3378af483aeee92dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081975"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>核心層級 API 函式 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 此層級的函式包含 ODBC 驅動程式的最基本介面一致性層級。  
  
|API 函式|注意|  
|------------------|-----------|  
|**SQLAllocConnect**|在*henv*所識別的環境中，配置連接控制碼*hdbc*的記憶體。 驅動程式管理員會處理此呼叫，並在每次呼叫**SQLConnect**、 **SQLBrowseConnect**或**SQLDriverConnect**時呼叫驅動程式的**SQLAllocConnect**函數。|  
|**SQLAllocEnv**|顯示對話方塊，其中指定 Oracle 用戶端軟體的需求，然後傳回 SQL_Null_HANDLE。 如果未安裝 Oracle 用戶端軟體，此函式會為環境控制碼、 *henv*配置記憶體，並初始化 ODBC 呼叫層級介面供應用程式使用。|  
|**SQLAllocStmt**|配置語句控制碼的記憶體，並將語句控制碼與 hdbc 所指定的連接產生關聯。 驅動程式管理員會將此呼叫傳遞給驅動程式，以配置 hstmt 結構的記憶體。|  
|**SQLBindCol**|指派結果資料行的儲存空間，並指定結果的類型。|  
|**SQLCancel**|取消語句控制碼上的處理，hstmt。 在某些情況下，Oracle 不允許取消執行中的語句。 這表示執行中的語句會繼續進行，直到 Oracle 完成進程為止，而 ODBC Driver for Oracle 則會取消語句的結果。|  
|**SQLColAttributes**|傳回結果集中資料行的描述項資訊。 描述元資訊會以字元字串、32位描述項相依值或整數值的形式傳回。|  
|**SQLConnect**|連接至資料來源。 若要使用 Oracle 作業系統驗證，請指定 "/" 做為*szUID*參數，並將 "" 當做*szAuthStr*參數。|  
|**SQLDescribeCol**|傳回給定結果資料行的名稱、類型、有效位數、小數位數和 null 屬性。 **注意： SQLDescribeCol**會以 SQL_VARCHAR 的形式來報告計算結果欄。|  
|**SQLDisconnect**|關閉連接。 如果已針對共用環境啟用連接共用，且應用程式在該環境的連接上呼叫**SQLDisconnect** ，則連接會傳回至連接集區，而且仍然可供使用相同共用環境的其他元件使用。|  
|**SQLError**|傳回關於最後一個錯誤的錯誤或狀態資訊。 驅動程式會維護可針對*hstmt*、 *hdbc*和*henv*引數傳回的堆疊或錯誤清單，視對**SQLError**的呼叫的方式而定。 錯誤佇列會在每個語句之後清除。 通常會抓取 Oracle 錯誤訊息，否則會是空的。|  
|**SQLExecDirect**|執行新的、未準備的 SQL 語句。 如果語句中有任何參數，驅動程式會使用參數標記變數的目前值。 如果您的資料表、視圖或功能變數名稱包含空格，請將名稱括在後引號中。 例如，如果您的資料庫包含名為「*我的資料表*」的資料表和「*我的欄位*」欄位，請將識別碼的每個元素括起來，如下所示：<br /><br /> 選取\`[我\`的資料表]。 \`我的\`Field1，;\`我的\`資料表。\`我的\`資料表\`中的 Field2\`|  
|**SQLExecute**|執行備妥的 SQL 語句（已由**SQLPrepare**準備的語句）。 如果語句中有任何參數，驅動程式會使用參數標記變數的目前值。|  
|**SQLFetch**|將結果集的一個資料列，抓取至先前呼叫**SQLBindCol**所指定的位置。 準備驅動程式以呼叫未系結資料行的**SQLGetData** 。|  
|**SQLFreeConnect**|釋放連接控制碼，並釋出配置給控制碼的所有記憶體。|  
|**SQLFreeEnv**|關閉 ODBC Driver for Oracle，並釋放與驅動程式相關聯的所有記憶體。|  
|**SQLFreeStmt**|停止與特定 hstmt 相關聯的處理、關閉與 hstmt 相關聯的任何開啟的資料指標、捨棄暫止的結果，並選擇性地釋放與語句控制碼相關聯的所有資源。|  
|**SQLGetCursorName**|傳回與指定 hstmt 相關聯的資料指標名稱。|  
|**SQLNumResultCols**|傳回結果集資料指標中的資料行數目。|  
|**SQLPrepare**|藉由規劃如何優化和執行語句來準備 SQL 語句。 **SQLExecDirect**會編譯 SQL 語句以供執行。<br /><br /> 如果您的資料表、視圖或功能變數名稱包含空格，請將名稱括在後引號中。 例如，如果您的資料庫包含名為「*我的資料表*」的資料表和「*我的欄位*」欄位，請將識別碼的每個元素括起來，如下所示：<br /><br /> 選取\`[我\`的資料表]。\`我的\`資料表\`中的欄位\`<br /><br /> 如需使用包含陣列做為正式參數之結果集的詳細資訊，請參閱[從預存程式傳回陣列參數](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLRowCount**|Oracle 不會提供方法來判斷結果集中的資料列數目，直到您提取最後一個資料列之後，才會傳回-1。|  
|**SQLSetCursorName**|將資料指標名稱與現用語句控制碼（ *hstmt*）產生關聯。|  
|**SQLSetParam**|已由 ODBC 2 中的 SQLBindParameter 取代。*x*。|  
|**SQLTransact**|針對與連接相關聯之所有語句控制碼（hstmt）上的所有作用中作業，或與環境控制碼*henv*相關聯的所有連接，要求認可或回復操作。 如果在手動模式下認可失敗，則交易會保持作用中狀態;您可以選擇復原交易，或重試認可作業。 如果在自動交易模式中，認可作業失敗，則會自動回復交易。交易不可為非使用中。|
