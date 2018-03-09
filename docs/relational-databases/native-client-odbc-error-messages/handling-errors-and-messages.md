---
title: "處理錯誤和訊息 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-error-messages
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, about error handling
- errors [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], about messages
- ODBC error handling
- SQL_INVALID_HANDLE return code
- errors [ODBC], about error handling
- messages [ODBC]
ms.assetid: 74ea9630-e482-4a46-bb45-f5234f079b48
caps.latest.revision: "34"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ace5aa790162d91203019d8c7d5cae5375cc281
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="handling-errors-and-messages"></a>處理錯誤與訊息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  當應用程式呼叫 ODBC 函數時，驅動程式會以兩種方式執行函數並傳回診斷資訊：傳回碼會指出整體 ODBC 函數成功或失敗，而診斷記錄會提供函數的相關詳細資訊。 診斷記錄包含標頭記錄和狀態記錄。 即使函數成功，也會傳回至少一個診斷記錄，也就是標頭記錄。  
  
 診斷資訊會在開發時間用於捕捉程式設計錯誤，例如，在硬式編碼 SQL 陳述式中發生無效的控制代碼和語法錯誤。 該資訊也會在執行階段用於捕捉執行階段錯誤和警告，例如，使用者傳回的 SQL 陳述式中發生資料截斷、規則違規和語法錯誤。 程式邏輯通常會以傳回碼為基礎。  
  
 例如，在應用程式呼叫之後**SQLFetch**擷取結果集的資料列，傳回碼會指出是否已到達的結果集結尾 (SQL_NO_DATA)，如果任何參考用訊息傳回 (SQL_SUCCESS_WITH_INFO)，或發生錯誤 (SQL_ERROR)。  
  
 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會傳回 SQL_SUCCESS 以外的任何項目，應用程式可以呼叫**SQLGetDiagRec**來擷取任何資訊或錯誤訊息。 使用**SQLGetDiagRec**來上下捲動訊息集如果有一個以上的訊息。  
  
 傳回碼 SQL_INVALID_HANDLE 永遠會指出程式設計錯誤，而且絕不會在執行階段發生。 雖然 SQL_ERROR 可能會指出程式設計錯誤，其他所有傳回碼還是會提供執行階段資訊。  
  
 原始[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生 API，Db-library for C 中，可讓應用程式安裝錯誤處理回呼和訊息處理函式傳回錯誤或訊息。 有些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 (例如，PRINT、RAISERROR、DBCC 和 SET) 會將其結果傳回 DB-Library 訊息處理常式函數，而非結果集。 不過，ODBC API 沒有此種回撥能力。 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式偵測到來自訊息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它將 ODBC 傳回碼設定為 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，並傳回訊息以一個或多個診斷記錄。 因此，ODBC 應用程式必須仔細測試這些傳回碼，然後呼叫**SQLGetDiagRec**來擷取訊息資料。  
  
 追蹤錯誤的相關資訊，請參閱[資料存取追蹤](http://go.microsoft.com/fwlink/?LinkId=125805)。 錯誤追蹤中新增的增強功能相關資訊的[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，請參閱[存取擴充事件記錄檔中的診斷資訊](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [處理產生訊息的陳述式](../../relational-databases/native-client-odbc-error-messages/processing-statements-that-generate-messages.md)  
  
-   [診斷記錄和欄位](../../relational-databases/native-client-odbc-error-messages/diagnostic-records-and-fields.md)  
  
-   [原生錯誤碼](../../relational-databases/native-client-odbc-error-messages/native-error-numbers.md)  
  
-   [SQLSTATE &#40; ODBC 錯誤碼 &#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)  
  
-   [錯誤訊息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
