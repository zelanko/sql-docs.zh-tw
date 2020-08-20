---
description: 核心層級 API 函式 (ODBC Driver for Oracle)
title: " (ODBC Driver for Oracle) 的核心層級 API 函式 |Microsoft Docs"
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
ms.openlocfilehash: c0940dd9fbabc02a5fd384208b2dcd4803f4f24a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471650"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>核心層級 API 函式 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 此層級的函式會組成 ODBC 驅動程式之介面一致性的最低層級。  
  
|API 函式|注意|  
|------------------|-----------|  
|**SQLAllocConnect**|在*henv*所識別的環境內，為連接控制碼*hdbc*配置記憶體。 當呼叫**SQLConnect**、 **SQLBrowseConnect**或**SQLDriverConnect**時，驅動程式管理員會處理此呼叫，並呼叫驅動程式的**SQLAllocConnect**函式。|  
|**SQLAllocEnv**|顯示指定 Oracle 用戶端軟體需求的對話方塊，然後傳回 SQL_Null_HANDLE。 如果未安裝 Oracle 用戶端軟體，此函式會為環境控制碼、 *henv*配置記憶體，並初始化 ODBC 呼叫層級介面，以供應用程式使用。|  
|**SQLAllocStmt**|配置語句控制碼的記憶體，並將語句控制碼與 hdbc 所指定的連接產生關聯。 驅動程式管理員會將此呼叫傳遞給驅動程式，該驅動程式會配置 hstmt 結構的記憶體。|  
|**SQLBindCol**|指派結果資料行的儲存空間，並指定結果的類型。|  
|**SQLCancel**|取消語句控制碼的處理，hstmt。 在某些情況下，Oracle 不允許取消執行中的語句。 這表示執行中的語句會繼續進行，直到 Oracle 完成進程為止，而 ODBC Driver for Oracle 會取消語句的結果。|  
|**SQLColAttributes**|傳回結果集中資料行的描述項資訊。 描述項資訊會以字元字串、32位描述元相依值或整數值的形式傳回。|  
|**SQLConnect**|連接至資料來源。 若要使用 Oracle 作業系統驗證，請指定 "/" 做為 *szUID* 參數，並指定 "" 作為 *szAuthStr* 參數。|  
|**SQLDescribeCol**|傳回指定結果資料行的名稱、類型、有效位數、小數位數和 null 屬性。 **注意： SQLDescribeCol** 會將計算結果欄 SQL_VARCHAR 報表。|  
|**SQLDisconnect**|關閉連接。 如果共用環境已啟用連接共用，而應用程式在該環境的連接上呼叫 **SQLDisconnect** ，則會將連接傳回連接集區，而且仍可使用相同共用環境的其他元件使用該連接。|  
|**SQLError**|傳回有關最後一個錯誤的錯誤或狀態資訊。 驅動程式會維護可針對 *hstmt*、 *hdbc*和 *henv* 引數傳回的堆疊或錯誤清單，取決於如何進行 **SQLError** 的呼叫。 錯誤佇列會在每個語句之後清除。 通常會捕獲 Oracle 錯誤訊息，否則會是空的。|  
|**SQLExecDirect**|執行新的、未準備的 SQL 語句。 如果語句中有任何參數，驅動程式會使用參數標記變數目前的值。 如果您的資料表、視圖或功能變數名稱包含空格，請用引號括住名稱。 例如，如果您的資料庫包含名為 [ *我的資料表* ] 和 [ *我*的欄位] 欄位的資料表，請將識別碼的每個元素括起來，如下所示：<br /><br /> 選取 [ \` 我 \` 的資料表]。 \`我 \` 的 Field1， \`我 \` 的資料表。 \`我 \` 的資料表中的 Field2 \`\`|  
|**SQLExecute**|執行已備妥的 SQL 語句 (**SQLPrepare**) 已備妥的語句。 如果語句中有任何參數，驅動程式會使用參數標記變數目前的值。|  
|**SQLFetch**|從結果集抓取一個資料列至先前呼叫 **SQLBindCol**所指定的位置。 準備驅動程式，以呼叫未系結資料行的 **SQLGetData** 。|  
|**SQLFreeConnect**|釋放連接控制碼，並釋出配置給此控制碼的所有記憶體。|  
|**SQLFreeEnv**|關閉 ODBC Driver for Oracle，並釋放與驅動程式相關聯的所有記憶體。|  
|**SQLFreeStmt**|停止與特定 hstmt 相關聯的處理、關閉與 hstmt 相關聯的任何開啟的資料指標、捨棄暫止的結果，並選擇性地釋放與語句控制碼相關聯的所有資源。|  
|**SQLGetCursorName**|傳回與指定 hstmt 相關聯的資料指標名稱。|  
|**SQLNumResultCols**|傳回結果集資料指標中的資料行數目。|  
|**SQLPrepare**|規劃如何優化和執行語句，以準備 SQL 語句。 **SQLExecDirect**會編譯 SQL 語句以供執行。<br /><br /> 如果您的資料表、視圖或功能變數名稱包含空格，請用引號括住名稱。 例如，如果您的資料庫包含名為 [ *我的資料表* ] 和 [ *我*的欄位] 欄位的資料表，請將識別碼的每個元素括起來，如下所示：<br /><br /> 選取 [ \` 我 \` 的資料表]。 \`我 \` 的資料表中的欄位 \`\`<br /><br /> 如需使用包含陣列做為正式參數之結果集的詳細資訊，請參閱 [從預存程式傳回陣列參數](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLRowCount**|在您提取最後一個資料列之後，Oracle 無法判斷結果集內的資料列數目，因此它會傳回-1。|  
|**SQLSetCursorName**|將資料指標名稱與使用中語句控制碼（ *hstmt*）產生關聯。|  
|**SQLSetParam**|以 ODBC 2 中的 SQLBindParameter 取代。*x*。|  
|**SQLTransact**|針對所有語句控制碼上所有使用中的作業要求認可或復原作業 (hstmt 與連接相關聯的) ，或與環境控制碼 *henv*相關聯的所有連接。 如果在手動模式下認可失敗，則交易會維持作用中狀態;您可以選擇回復交易或重試認可作業。 如果在自動交易模式下認可作業失敗，則會自動回復交易;交易不能為非使用中。|
