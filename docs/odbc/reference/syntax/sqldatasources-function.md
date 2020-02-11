---
title: SQLDataSources 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSources
helpviewer_keywords:
- SQLDataSources function [ODBC]
ms.assetid: 3f63b1b4-e70e-44cd-96c6-6878d50d0117
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 28fcf56293516937455afc387a8d478734f5b006
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68121384"
---
# <a name="sqldatasources-function"></a>SQLDataSources 函式
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLDataSources**會傳回資料來源的相關資訊。 此函式只會由驅動程式管理員執行。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLDataSources(  
     SQLHENV          EnvironmentHandle,  
     SQLUSMALLINT     Direction,  
     SQLCHAR *        ServerName,  
     SQLSMALLINT      BufferLength1,  
     SQLSMALLINT *    NameLength1Ptr,  
     SQLCHAR *        Description,  
     SQLSMALLINT      BufferLength2,  
     SQLSMALLINT *    NameLength2Ptr);  
```  
  
## <a name="arguments"></a>引數  
 *EnvironmentHandle*  
 源環境控制碼。  
  
 *方向*  
 源決定驅動程式管理員會傳回哪些資料來源的相關資訊。 可為以下項目：  
  
 SQL_FETCH_NEXT （若要提取清單中的下一個資料來源名稱）、SQL_FETCH_FIRST （從清單開頭提取）、SQL_FETCH_FIRST_USER （以提取第一個使用者 DSN），或 SQL_FETCH_FIRST_SYSTEM （提取第一個系統 DSN）。  
  
 當 [*方向*] 設定為 [SQL_FETCH_FIRST] 時，後續呼叫**SQLDataSources** ，並將*方向*設定為 SQL_FETCH_NEXT 會同時傳回使用者和系統 dsn。 當 [*方向*] 設定為 [SQL_FETCH_FIRST_USER] 時，所有後續呼叫**SQLDataSources** ，並將*方向*設定為 SQL_FETCH_NEXT 只會傳回使用者的 dsn。 當 [*方向*] 設定為 [SQL_FETCH_FIRST_SYSTEM] 時，所有後續呼叫**SQLDataSources** ，並將*方向*設定為 [SQL_FETCH_NEXT 只會傳回系統 dsn。  
  
 *ServerName*  
 輸出要傳回資料來源名稱之緩衝區的指標。  
  
 如果*servername*是 Null，則*NameLength1Ptr*仍然會傳回*servername*所指向的緩衝區中可傳回的字元總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength1*  
 源**ServerName*緩衝區的長度（以字元為單位）;這不需要超過 SQL_MAX_DSN_LENGTH 加上 null 終止字元。  
  
 *NameLength1Ptr*  
 輸出緩衝區的指標，要在其中傳回\* *ServerName*中可傳回的字元總數（不包括 null 終止字元）。 如果可傳回的字元數大於或等於*BufferLength1*， \* *ServerName*中的資料來源名稱會截斷為*BufferLength1*減去 null 終止字元的長度。  
  
 *說明*  
 輸出緩衝區的指標，要在其中傳回與資料來源相關聯之驅動程式的描述。 例如，dBASE 或 SQL Server。  
  
 如果*description*是 Null，則*NameLength2Ptr*仍然會傳回可在*描述*所指向的緩衝區中傳回的字元總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength2*  
 源**描述*緩衝區的長度（以字元為單位）。  
  
 *NameLength2Ptr*  
 輸出緩衝區的指標，傳回\**描述*中可傳回的字元總數（不包括 null 終止字元）。 如果可傳回的字元數大於或等於*BufferLength2*，則\**描述*中的驅動程式描述會截斷為*BufferLength2*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDataSources**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_ENV *HandleType*和*EnvironmentHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出通常由**SQLDataSources**所傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|（DM）驅動程式管理員特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|（DM）緩衝區\* *ServerName*不夠大，無法傳回完整的資料來源名稱。 因此，名稱已被截斷。 整個資料來源名稱的長度會在\* *NameLength1Ptr*中傳回。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> （DM）緩衝區\**描述*不夠大，無法傳回完整的驅動程式描述。 因此，描述已被截斷。 Untruncated 資料來源描述的長度會在 **NameLength2Ptr*中傳回。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|（DM）發生錯誤，其中沒有特定的 SQLSTATE，而且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|（DM）驅動程式管理員無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|（DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）為引數*BufferLength1*指定的值小於0。<br /><br /> （DM）為引數*BufferLength2*指定的值小於0。|  
|HY103|不正確抓取程式碼|（DM）為引數*方向*指定的值不等於 SQL_FETCH_FIRST、SQL_FETCH_FIRST_USER、SQL_FETCH_FIRST_SYSTEM 或 SQL_FETCH_NEXT。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
  
## <a name="comments"></a>註解  
 由於**SQLDataSources**是在驅動程式管理員中執行，因此支援所有驅動程式，而不論特定驅動程式的標準合規性為何。  
  
 應用程式可以多次呼叫**SQLDataSources** ，以取得所有資料來源名稱。 驅動程式管理員會從系統資訊抓取這則資訊。 當沒有其他資料來源名稱時，驅動程式管理員會傳回 SQL_NO_DATA。 如果**SQLDataSources**在傳回 SQL_NO_DATA 後立即以 SQL_FETCH_NEXT 呼叫，它會傳回第一個資料來源名稱。 如需有關應用程式如何使用**SQLDataSources**傳回之資訊的詳細資訊，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果 SQL_FETCH_NEXT 在第一次呼叫時傳遞至**SQLDataSources** ，它會傳回第一個資料來源名稱。  
  
 驅動程式會決定資料來源名稱如何對應至實際的資料來源。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|探索和列出連接至資料來源所需的值|[SQLBrowseConnect 函數](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|使用連接字串或對話方塊連接到資料來源|[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回驅動程式描述和屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
