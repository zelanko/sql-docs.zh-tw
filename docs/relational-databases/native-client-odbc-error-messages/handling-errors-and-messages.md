---
title: 處理錯誤和訊息 |Microsoft Docs
description: 瞭解當應用程式呼叫 ODBC 函數時所傳回的診斷資訊，包括成功或失敗，以及詳細的資訊。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 92a47417e8b8b133bd8956d0ba02d8f0037d0111
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868335"
---
# <a name="handling-errors-and-messages"></a>處理錯誤與訊息
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  當應用程式呼叫 ODBC 函數時，驅動程式會以兩種方式執行函數並傳回診斷資訊：傳回碼會指出整體 ODBC 函數成功或失敗，而診斷記錄會提供函數的相關詳細資訊。 診斷記錄包含標頭記錄和狀態記錄。 即使函數成功，也會傳回至少一個診斷記錄，也就是標頭記錄。  
  
 診斷資訊會在開發時間用於捕捉程式設計錯誤，例如，在硬式編碼 SQL 陳述式中發生無效的控制代碼和語法錯誤。 該資訊也會在執行階段用於捕捉執行階段錯誤和警告，例如，使用者傳回的 SQL 陳述式中發生資料截斷、規則違規和語法錯誤。 程式邏輯通常會以傳回碼為基礎。  
  
 例如，在應用程式呼叫 **SQLFetch** 來取出結果集中的資料列之後，傳回碼會指出是否已到達結果集的結尾 (SQL_NO_DATA) ，如果傳回任何參考訊息 (SQL_SUCCESS_WITH_INFO) ，或發生 (SQL_ERROR) 錯誤。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式傳回 SQL_SUCCESS 以外的任何資訊，應用程式可以呼叫 **SQLGetDiagRec** 來取出任何資訊或錯誤訊息。 如果有一個以上的訊息，請使用 **SQLGetDiagRec** 來向上和向下移動訊息集。  
  
 傳回碼 SQL_INVALID_HANDLE 永遠會指出程式設計錯誤，而且絕不會在執行階段發生。 雖然 SQL_ERROR 可能會指出程式設計錯誤，其他所有傳回碼還是會提供執行階段資訊。  
  
 適用于 C 的原始原 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生 API （DB-Library）可讓應用程式安裝回呼錯誤處理以及傳回錯誤或訊息的訊息處理函式。 有些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 (例如，PRINT、RAISERROR、DBCC 和 SET) 會將其結果傳回 DB-Library 訊息處理常式函數，而非結果集。 不過，ODBC API 沒有此種回撥能力。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式偵測回來的訊息時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，它會將 ODBC 傳回碼設定為 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，並將訊息傳回為一或多個診斷記錄。 因此，ODBC 應用程式必須仔細測試這些傳回碼，然後呼叫 **SQLGetDiagRec** 來取出訊息資料。  
  
 如需追蹤錯誤的資訊，請參閱 [Data Access Tracing](/previous-versions/sql/sql-server-2008/cc765421(v=sql.100)) (資料存取追蹤)。 如需有關 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中加入之錯誤追蹤增強功能的詳細資訊，請參閱[存取擴充事件記錄檔中的診斷資訊](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [處理產生訊息的陳述式](../../relational-databases/native-client-odbc-error-messages/processing-statements-that-generate-messages.md)  
  
-   [診斷記錄和欄位](../../relational-databases/native-client-odbc-error-messages/diagnostic-records-and-fields.md)  
  
-   [原生錯誤號碼](../../relational-databases/native-client-odbc-error-messages/native-error-numbers.md)  
  
-   [SQLSTATE &#40;ODBC 錯誤碼&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)  
  
-   [錯誤訊息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
