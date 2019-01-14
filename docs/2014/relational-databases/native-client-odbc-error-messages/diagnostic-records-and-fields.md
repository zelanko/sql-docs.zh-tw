---
title: 診斷記錄和欄位 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.assetid: 4949530c-62d1-4f1a-b592-144244444ce0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 173d0287ba1b63e8811e2d340448d03c3bbf961d
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133138"
---
# <a name="diagnostic-records-and-fields"></a>診斷記錄和欄位
  診斷記錄與 ODBC 環境、連接、陳述式或描述項控制代碼相關聯。 當任何 ODBC 函數引發 SQL_SUCCESS 或 SQL_INVALID_HANDLE 以外的傳回碼時，該函數所呼叫的控制代碼會有包含參考用訊息或錯誤訊息的相關聯診斷記錄。 這些記錄會保留到系統使用該控制代碼呼叫另一個函數為止，屆時將捨棄這些記錄。 不論何時，可與控制代碼相關聯的診斷記錄數目沒有任何限制。  
  
 共有兩種診斷記錄：標頭和狀態。 標頭記錄為記錄 0，而當有狀態記錄時，這兩種記錄分別為記錄 1 和具有更大編號的記錄。 診斷記錄包含標頭記錄和狀態記錄的不同欄位。 ODBC 元件也可以定義本身的診斷記錄欄位。  
  
 標頭記錄中的欄位包含有關函數執行的一般資訊，包括傳回碼、資料列計數、狀態記錄的數目和所執行的陳述式類型。 除非 ODBC 函數傳回 SQL_INVALID_HANDLE，否則一定會建立標頭記錄。 如需標頭記錄中欄位的完整清單，請參閱 < [SQLGetDiagField](../native-client-odbc-api/sqlgetdiagfield.md)。  
  
 狀態記錄中的欄位包含有關 ODBC 驅動程式管理員、驅動程式或資料來源所傳回的特定錯誤或警告的詳細資訊，包括 SQLSTATE、原生錯誤號碼、診斷訊息、資料行號碼和資料列號碼。 只有在函數傳回 SQL_ERROR、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_NEED_DATA 或 SQL_STILL_EXECUTING 時，才會建立狀態記錄。 如需狀態記錄中欄位的完整清單，請參閱 < **SQLGetDiagField**。  
  
 **SQLGetDiagRec**擷取單一的診斷記錄，以及其 ODBC SQLSTATE、 自發性錯誤號碼和診斷訊息欄位。 這項功能是類似於 ODBC 2。_x_**SQLError**函式。 ODBC 3 中的簡單錯誤處理函式。*x*是重複地呼叫**SQLGetDiagRec**開頭*RecNumber*參數設定為 1，並遞增*RecNumber*直到 1**SQLGetDiagRec**傳回 sql_no_data 為止。 這是相當於 ODBC 2。*x*應用程式呼叫**SQLError**直到它傳回 SQL_NO_DATA_FOUND 為止。  
  
 ODBC 3。*x*支援更多診斷資訊比 ODBC 2。*x*。 這項資訊會儲存在其他欄位中使用擷取的診斷記錄**SQLGetDiagField**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式具有驅動程式專用診斷欄位，可以使用擷取**SQLGetDiagField**。 這些驅動程式特定欄位的標籤會定義在 sqlncli.h 中。 請使用這些標籤來擷取與每個診斷記錄相關聯的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 狀態、嚴重性層級、伺服器名稱、程序名稱和行號。 此外，sqlncli.h 也會包含的驅動程式用來識別 TRANSACT-SQL 陳述式，如果應用程式呼叫的程式碼定義**SQLGetDiagField**具有*Sqlgetdiagfield*設 SQL_DIAG_DYNAMIC_FUNCTION_CODE。  
  
 **SQLGetDiagField**處理由 ODBC 驅動程式管理員使用它從基礎驅動程式會快取的錯誤資訊。 在成功建立連接之前，ODBC 驅動程式管理員不會快取驅動程式專用的診斷欄位。 **SQLGetDiagField**如果呼叫它來取得驅動程式專用診斷欄位，在完成成功連接之前，會傳回 SQL_ERROR。 如果 ODBC 連接函數傳回 SQL_SUCCESS_WITH_INFO，則連接函數的驅動程式特定的診斷欄位就還不能使用。 您可以開始呼叫**SQLGetDiagField**才是您所做其他的 ODBC 驅動程式專用診斷欄位的函式之後的連線函式的呼叫。  
  
 報告的大部分錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式可以進行有效的診斷使用所傳回的資訊**SQLGetDiagRec**。 不過，在某些情況下，由驅動程式特定的診斷欄位所傳回的資訊對於診斷錯誤十分重要。 使用應用程式的 ODBC 錯誤處理常式撰寫程式碼時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式，它是個不錯的主意，同時使用**SQLGetDiagField**以至少擷取 SQL_DIAG_SS_MSGSTATE 和 SQL_DIAG_SS_SEVERITY驅動程式特有的欄位。 如果特定錯誤可能會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程式碼中的數個位置引發，SQL_DIAG_SS_MSGSTATE 會向 Microsoft 支援工程師明確地指出引發錯誤的位址，這項功能有時可以協助診斷問題。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](handling-errors-and-messages.md)  
  
  
