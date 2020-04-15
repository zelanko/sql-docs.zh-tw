---
title: 診斷記錄和欄位 |微軟文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- header records [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], diagnostic records
- ODBC error handling, diagnostic records
- SQLGetDiagField function
- diagnostic records [ODBC]
- errors [ODBC], diagnostic records
- fields [ODBC]
- status information [ODBC]
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b9cfea2db0ad0a5eadeede6df3f76ea3979243d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291796"
---
# <a name="diagnostic-records-and-fields"></a>診斷記錄和欄位
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  診斷記錄與 ODBC 環境、連接、陳述式或描述項控制代碼相關聯。 當任何 ODBC 函數引發 SQL_SUCCESS 或 SQL_INVALID_HANDLE 以外的傳回碼時，該函數所呼叫的控制代碼會有包含參考用訊息或錯誤訊息的相關聯診斷記錄。 這些記錄會保留到系統使用該控制代碼呼叫另一個函數為止，屆時將捨棄這些記錄。 不論何時，可與控制代碼相關聯的診斷記錄數目沒有任何限制。  
  
 共有兩種診斷記錄：標頭和狀態。 標頭記錄為記錄 0，而當有狀態記錄時，這兩種記錄分別為記錄 1 和具有更大編號的記錄。 診斷記錄包含標頭記錄和狀態記錄的不同欄位。 ODBC 元件也可以定義本身的診斷記錄欄位。  
  
 標頭記錄中的欄位包含有關函數執行的一般資訊，包括傳回碼、資料列計數、狀態記錄的數目和所執行的陳述式類型。 除非 ODBC 函數傳回 SQL_INVALID_HANDLE，否則一定會建立標頭記錄。 有關標頭記錄中欄位的完整清單,請參閱[SQLGetDiagField](../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md)。  
  
 狀態記錄中的欄位包含有關 ODBC 驅動程式管理員、驅動程式或資料來源所傳回的特定錯誤或警告的詳細資訊，包括 SQLSTATE、原生錯誤號碼、診斷訊息、資料行號碼和資料列號碼。 只有在函數傳回 SQL_ERROR、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_NEED_DATA 或 SQL_STILL_EXECUTING 時，才會建立狀態記錄。 有關狀態記錄中欄位的完整清單,請參閱**SQLGetDiagField**。  
  
 **SQLGetDiagRec**檢索單個診斷記錄及其 ODBC SQLSTATE、本機錯誤編號和診斷訊息欄位。 此功能類似於 ODBC 2。_x_**SQLError**函數。 ODBC 3 中最簡單的錯誤處理功能。*x*是重複調用**SQLGetDiagRec,** 從*RecNumber*參數設置為 1 開始,並將*RecNumber*增加 1,直到**SQLGetDiagRec**返回SQL_NO_DATA。 這相當於 ODBC 2。*x*應用程式呼叫**SQLError,** 直到它傳回SQL_NO_DATA_FOUND。  
  
 ODBC 3.*x*支援比 ODBC 2 更多的診斷資訊。*x*. . 此資訊存儲在使用**SQLGetDiagField**檢索的診斷記錄中的其他欄位中。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式具有特定於驅動程式的診斷欄位,可以使用**SQLGetDiagField**檢索這些欄位。 這些驅動程式特定欄位的標籤會定義在 sqlncli.h 中。 請使用這些標籤來擷取與每個診斷記錄相關聯的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 狀態、嚴重性層級、伺服器名稱、程序名稱和行號。 此外,sqlncli.h 包含驅動程式用於標識 Transact-SQL 語句的代碼的定義,如果應用程式呼叫**SQLGetDiagField,** 而*Diag識別符*設定為SQL_DIAG_DYNAMIC_FUNCTION_CODE。  
  
 **SQLGetDiagField**由 ODBC 驅動程式管理器使用從基礎驅動程式緩存的錯誤資訊進行處理。 在成功建立連接之前，ODBC 驅動程式管理員不會快取驅動程式專用的診斷欄位。 如果調用 SQLGetDiagField 在成功連接完成之前獲取特定於驅動程序的診斷欄位,則**SQLGetDiagField**將返回SQL_ERROR。 如果 ODBC 連接函數傳回 SQL_SUCCESS_WITH_INFO，則連接函數的驅動程式特定的診斷欄位就還不能使用。 只有在連接函數之後進行另一個 ODBC 函數調用後,才能開始調用**SQLGetDiagField**以進行特定於驅動程式的診斷欄位。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式報告的大多數錯誤都可以使用**SQLGetDiagRec**返回的資訊進行有效診斷。 不過，在某些情況下，由驅動程式特定的診斷欄位所傳回的資訊對於診斷錯誤十分重要。 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式對應用程式編碼 ODBC 錯誤處理程式時,最好也使用**SQLGetDiagField**檢索至少SQL_DIAG_SS_MSGSTATE,並SQL_DIAG_SS_SEVERITY特定於驅動程式的欄位。 如果特定錯誤可能會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程式碼中的數個位置引發，SQL_DIAG_SS_MSGSTATE 會向 Microsoft 支援工程師明確地指出引發錯誤的位址，這項功能有時可以協助診斷問題。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
