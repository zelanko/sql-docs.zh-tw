---
title: SQLCancelHandle 函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 629ff63f6fd06aaccc1f60209231f5c937f4a67d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036129"
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函式
**標準**  
 引進的版本： ODBC 3。8  
  
 標準合規性：無  
  
 預期大部分的 ODBC 3.8 （和更新版本）驅動程式都會執行此函式。 如果驅動程式不是，則在*handle*參數中使用連接控制碼呼叫**SQLCancelHandle**時，將會傳回具有 IM001 之 SQLSTATE 的 SQL_ERROR，而訊息 ' 驅動程式不支援此函式 ' '，因為*handle*參數將會對應至**SQLCancel**的**呼叫，並**可在驅動程式執行**SQLCancel**時處理。 應用程式可以使用**SQLGetFunctions**來判斷驅動程式是否支援**SQLCancelHandle**。  
  
 **摘要**  
 **SQLCancelHandle**會取消對連接或語句的處理。 當 SQL_HANDLE_STMT *HandleType*時，驅動程式管理員會將對**SQLCancelHandle**的呼叫對應至**SQLCancel**的呼叫。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 源要 cacel 處理的控制碼類型。 有效的值為 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
 *圖*  
 源要取消處理的控制碼。  
  
 如果*handle*不是*HandleType*所指定之類型的有效控制碼， **SQLCancelHandle**會傳回 SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCancelHandle**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*的**SQLGetDiagRec**以及語句控制碼*句*柄或 SQL_HANDLE_DBC 和連接控制碼*句*柄的*HandleType* ，來取得相關聯的 SQLSTATE 值。  
  
 下表列出**SQLCancelHandle**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)在引數* \*MessageText*緩衝區中傳回的錯誤訊息描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|已針對與*控制碼*相關聯的其中一個語句控制碼呼叫以非同步方式執行的語句相關函式，而且*HandleType*已設定為 SQL_HANDLE_DBC。 呼叫**SQLCancelHandle**時，非同步函數仍在執行中。<br /><br /> （DM）已 SQL_HANDLE_STMT *HandleType*引數;在相關聯的連接控制碼上呼叫了非同步執行的函式;呼叫這個函式時，函數仍在執行。<br /><br /> 已針對與*控制碼*相關聯的其中一個語句控制碼呼叫（DM） **SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並將*HandleType*設定為 SQL_HANDLE_DBC，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> 已針對*ConnectionHandle*呼叫**SQLBrowseConnect** ，並 SQL_NEED_DATA 傳回。 此函式是在流覽程式完成之前呼叫。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY092|不正確屬性/選項識別碼|*HandleType*已設定為 SQL_HANDLE_ENV 或 SQL_HANDLE_DESC。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*控制碼*相關聯的驅動程式不支援函式。|  
  
 如果呼叫**SQLCancelHandle**時，將*HandleType*設為 SQL_HANDLE_STMT，它會傳回可由函式**SQLCancel**傳回的任何 SQLSTATE。  
  
## <a name="comments"></a>註解  
 此函式類似于**SQLCancel** ，但可能會採用連接或語句控制碼做為參數，而不只是語句控制碼。 當 SQL_HANDLE_STMT *HandleType*時，驅動程式管理員會將對**SQLCancelHandle**的呼叫對應至**SQLCancel**的呼叫。 這可讓應用程式使用**SQLCancelHandle**來取消語句作業，即使驅動程式未執行**SQLCancelHandle**也是一樣。  
  
 如需有關取消語句作業的詳細資訊，請參閱[SQLCancel 函數](../../../odbc/reference/syntax/sqlcancel-function.md)。  
  
 如果*處理* **SQLCancelHandle**的呼叫沒有任何進行中的作業，則不會有任何作用。  
  
 連接控制碼上的**SQLCancelHandle**可以取消下列類型的處理：  
  
-   在連接上以非同步方式執行的函式。  
  
-   在另一個執行緒上的連接控制碼上執行的函式。  
  
 當呼叫**SQLCancelHandle**來取消在連接中以非同步方式執行的函式時， **SQLCancelHandle**所張貼的診斷記錄會附加至取消的作業所傳回的狀態;不過，當取消另一個執行緒上的連接上執行的函式時， **SQLCancelHandle**不會傳回診斷記錄。  
  
 使用**SQLCancelHandle**取消**SQLEndTran**可能會使連接處於暫停狀態。 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  如需如何在 Windows 7 之前的 Windows 作業系統上部署的應用程式中使用**SQLCancelHandle**的相關資訊，請參閱[相容性比較表](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>取消與連接相關的非同步處理  
 如果函式傳回 SQL_STILL_EXECUTING，應用程式可以呼叫**SQLCancelHandle**來取消作業。 如果取消要求成功， **SQLCancelHandle**會傳回 SQL_SUCCESS。 這並不表示已取消原始函式;這表示已處理取消要求。 驅動程式和資料來源會判斷作業是否已取消。 應用程式必須繼續呼叫原始函式，直到傳回碼不 SQL_STILL_EXECUTING 為止。 如果原始函式已取消，則傳回碼為 SQL_ERROR 並 SQLSTATE HY008 （作業已取消）。 如果原始函式已完成其正常處理（未取消），則傳回碼會 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，或 SQL_ERROR 以及 HY008 以外的 SQLSTATE （作業已取消）（如果原始函式失敗）。  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>取消在另一個執行緒上執行的函式  
 在多執行緒應用程式中，應用程式可以取消正在另一個執行緒上執行的作業。 若要取消作業，應用程式會使用函式所使用的控制碼呼叫**SQLCancelHandle** ，但在不同的執行緒上。 驅動程式和作業系統會決定操作的取消方式。 **SQLCancelHandle**傳回碼會指出驅動程式是否已處理要求，並傳回 SQL_SUCCESS 或 SQL_ERROR （不會傳回任何診斷資訊）。 如果已取消對原始函式的處理，原始函式會傳回 SQL_ERROR 並 SQLSTATE HY008 （作業已取消）。  
  
 如果在另一個執行緒上呼叫**SQLCancelHandle**來取消函式時，函式正在執行，則函式可能會成功並傳回 SQL_SUCCESS 之後，取消才會生效。 如果作業在**SQLCancelHandle**能夠取消作業之前完成，則呼叫**SQLCancelHandle**不會有任何作用。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取消在語句控制碼上非同步執行的函式、在需要資料的語句上取消函式，或取消在另一個執行緒上的語句上執行的函數。|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
