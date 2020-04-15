---
title: 處理錯誤和消息 |微軟文件
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
ms.openlocfilehash: 59bb40dbfc7f8596968d2dc441396dc9c076bb82
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291658"
---
# <a name="handling-errors-and-messages"></a>處理錯誤與訊息
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  當應用程式呼叫 ODBC 函數時，驅動程式會以兩種方式執行函數並傳回診斷資訊：傳回碼會指出整體 ODBC 函數成功或失敗，而診斷記錄會提供函數的相關詳細資訊。 診斷記錄包含標頭記錄和狀態記錄。 即使函數成功，也會傳回至少一個診斷記錄，也就是標頭記錄。  
  
 診斷資訊會在開發時間用於捕捉程式設計錯誤，例如，在硬式編碼 SQL 陳述式中發生無效的控制代碼和語法錯誤。 該資訊也會在執行階段用於捕捉執行階段錯誤和警告，例如，使用者傳回的 SQL 陳述式中發生資料截斷、規則違規和語法錯誤。 程式邏輯通常會以傳回碼為基礎。  
  
 例如,在應用程式調用**SQLFetch**檢索結果集中的行後,返回代碼指示是否到達結果集的末尾(SQL_NO_DATA),是否返回任何資訊性消息(SQL_SUCCESS_WITH_INFO),或者是否發生錯誤(SQL_ERROR)。  
  
 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式返回SQL_SUCCESS以外的任何內容,則應用程式可以調用**SQLGetDiagRec**來檢索任何資訊或錯誤消息。 如果消息集有多個消息,請使用**SQLGetDiagRec**向上和向下滾動消息集。  
  
 傳回碼 SQL_INVALID_HANDLE 永遠會指出程式設計錯誤，而且絕不會在執行階段發生。 雖然 SQL_ERROR 可能會指出程式設計錯誤，其他所有傳回碼還是會提供執行階段資訊。  
  
 原始[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機 API DB-Library 表示 C,允許應用程式安裝回調錯誤處理和消息處理功能,這些函數返回錯誤或消息。 有些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 (例如，PRINT、RAISERROR、DBCC 和 SET) 會將其結果傳回 DB-Library 訊息處理常式函數，而非結果集。 不過，ODBC API 沒有此種回撥能力。 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式檢測到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從返回的消息時,它將ODBC返回代碼設置為SQL_SUCCESS_WITH_INFO或SQL_ERROR,並將消息作為一個或多個診斷記錄返回。 因此,ODBC 應用程式必須仔細測試這些返回代碼,並調用**SQLGetDiagRec**檢索消息數據。  
  
 如需追蹤錯誤的資訊，請參閱 [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (資料存取追蹤)。 如需有關 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中加入之錯誤追蹤增強功能的詳細資訊，請參閱[存取擴充事件記錄檔中的診斷資訊](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [處理產生訊息的陳述式](../../relational-databases/native-client-odbc-error-messages/processing-statements-that-generate-messages.md)  
  
-   [診斷記錄和欄位](../../relational-databases/native-client-odbc-error-messages/diagnostic-records-and-fields.md)  
  
-   [原生錯誤號碼](../../relational-databases/native-client-odbc-error-messages/native-error-numbers.md)  
  
-   [SQLSTATE &#40;ODBC 錯誤代碼&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)  
  
-   [錯誤訊息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
