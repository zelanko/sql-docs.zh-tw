---
title: SQL取消處理功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 059ed283032feb96ca5e6b12520682ccb034752a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299663"
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函式
**一致性**  
 版本介紹: ODBC 3.8  
  
 標準合規性:無  
  
 預計大多數 ODBC 3.8(以及更高版本)驅動程式將實現此功能。 如果驅動程式沒有,則調用**SQLCancelHandle**與*句柄*參數中的連接句柄將返回SQL_ERROR,其中 SQLSTATE 為 IM001,消息"驅動程式不支援此功能";對**SQLCancelHandle**的調用具有語句句柄,因為*句柄*參數將映射到驅動程式管理器對**SQLCancel**的調用,如果驅動程式實現**SQLCancel,** 則可以進行處理。 應用程式可以使用**SQLGet 函數**來確定驅動程式是否支援**SQLCancelHandle**。  
  
 **摘要**  
 **SQLCancelHandle**取消連接或語句上的處理。 當*處理類型*SQL_HANDLE_STMT時,驅動程式管理員將**SQLCancelHandle**的呼叫映射到**SQLCancel**的調用。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]要處理的句柄的類型。 有效值SQL_HANDLE_DBC或SQL_HANDLE_STMT。  
  
 *Handle*  
 [輸入]要取消處理的句柄。  
  
 如果*句柄*不是*HandleType*指定的類型的有效句柄 **,SQLCancelHandle**將返回SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCancelHandle**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和語句*句柄*或SQL_HANDLE_DBC的處理*類型*和連接*句柄句柄*。  
  
 下表列出了**SQLCancelHandle**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)在參數*\*MessageText*緩衝區中返回的錯誤消息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|對於與*句柄*關聯的語句句柄之一,調用了非同步執行語句相關的函數,並且*HandleType*設置為SQL_HANDLE_DBC。 調用**SQLCancelHandle**時,非同步函數仍在執行。<br /><br /> (DM)*句柄類型*參數SQL_HANDLE_STMT;在關聯的連接句柄上調用了非同步執行函數;調用此函數時,該函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用,其中一個語句句柄與*句柄*和*句柄類型*相關聯,**SQLExecDirect**設置為SQL_HANDLE_DBC,並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> **SQLBrowseConnect**被呼叫為*連接句柄*,並返回SQL_NEED_DATA。 在流覽過程完成之前調用此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY092|不合法屬性/選項識別碼|*句柄類型*設置為SQL_HANDLE_ENV或SQL_HANDLE_DESC。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*句柄*關聯的驅動程式不支援該功能。|  
  
 如果**SQLCancelHandle**調用的*句柄設置為*SQL_HANDLE_STMT,它可以返回函數**SQLCancel**可以返回的任何 SQLSTATE。  
  
## <a name="comments"></a>註解  
 此功能類似於**SQLCancel,** 但可以將連接或語句句柄作為參數,而不僅僅是語句句柄。 當*處理類型*SQL_HANDLE_STMT時,驅動程式管理員將**SQLCancelHandle**的呼叫映射到**SQLCancel**的調用。 這允許應用程式使用**SQLCancelHandle**取消敘述操作,即使驅動程式未實現**SQLCancelHandle**。  
  
 有關取消語句操作的詳細資訊,請參閱[SQLCancel 函數](../../../odbc/reference/syntax/sqlcancel-function.md)。  
  
 如果*處理***SQLCancelHandle**的調用沒有正在進行的操作,則不起作用。  
  
 **連接句柄上的 SQLCancelHandle**可以取消以下類型的處理:  
  
-   在連接上異步運行的函數。  
  
-   在另一個線程的連接句柄上運行的函數。  
  
 當調用 SQLCancelHandle 以取消在連接中非同步執行的函數時 **,SQLCancelHandle**發布的診斷記錄將追加到被取消的操作返回的那些記錄中;如果調用**SQLCancelHandle,** 則將 SQLCancelHandle 發布的診斷記錄追加到已取消的操作返回的那些記錄中。但是,當取消在另一個線程上的連接上運行的函數時 **,SQLCancelHandle**不會返回診斷記錄。  
  
 使用**SQLCancelHandle**取消**SQLEndTran**可能會將連接置於掛起狀態。 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  有關如何在將部署在 Windows 作業系統早於 Windows 7 的 Windows 作業系統上的應用程式中使用**SQLCancelHandle**的資訊,請參閱[相容性矩陣](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>取消連線相關的非同步處理  
 如果函數返回SQL_STILL_EXECUTING,應用程式可以調用**SQLCancelHandle**取消該操作。 如果取消請求成功 **,SQLCancelHandle**將返回SQL_SUCCESS。 這並不意味著原始函數已取消;因此,它未取消原始函數。它表示已處理取消請求。 驅動程式和數據源確定何時取消操作或是否取消操作。 應用程式必須繼續調用原始函數,直到返回代碼不SQL_STILL_EXECUTING。 如果原始函數已取消,則返回代碼SQL_ERROR SQLSTATE HY008(操作已取消)。 如果原始函數完成其正常處理(未取消),則返回代碼SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,或SQL_ERROR和 SQLSTATE 以外的 HY008(操作已取消),如果原始函數失敗。  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>取消在另一個緒執行的函數  
 在多線程應用程式中,應用程式可以取消在另一個線程上運行的操作。 要取消該操作,應用程式調用**SQLCancelHandle,** 該句柄由函數使用,但調用其他線程。 驅動程式和作業系統確定如何取消操作。 **SQLCancelHandle**返回代碼指示驅動程式是處理請求,返回SQL_SUCCESS或SQL_ERROR(不返回任何診斷資訊)。 如果取消對原始函數的處理,則原始函數將返回SQL_ERROR和 SQLSTATE HY008(操作已取消)。  
  
 如果在調用另一個線程上調用**SQLCancelHandle**來取消該函數時正在執行函數,則函數可以成功並返回SQL_SUCCESS,然後取消才能生效。 如果**SQLCancelHandle**之前的操作已完成,則對**SQLCancelHandle**的調用不起作用。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取消在語句句柄上非同步運行的函數,取消需要資料的語句上的函數,或取消在另一個線程上運行語句上的函數。|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
