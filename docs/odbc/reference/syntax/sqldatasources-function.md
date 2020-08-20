---
description: SQLDataSources 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcf57779916b7a9d3189a5ce37b8603e5da5cb74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461180"
---
# <a name="sqldatasources-function"></a>SQLDataSources 函式
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLDataSources** 會傳回資料來源的相關資訊。 此函數只會由驅動程式管理員執行。  
  
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
 輸出環境控制碼。  
  
 *方向*  
 輸出決定驅動程式管理員傳回相關資訊的資料來源。 可為以下項目：  
  
 SQL_FETCH_NEXT (提取清單) 中的下一個資料來源名稱，SQL_FETCH_FIRST (從清單) 的開頭提取，SQL_FETCH_FIRST_USER (提取第一個使用者 DSN) ，或 SQL_FETCH_FIRST_SYSTEM (提取第一個系統 DSN) 。  
  
 當 *方向* 設定為 SQL_FETCH_FIRST 時，對 **SQLDataSources** 的後續呼叫會將 *方向* 設為 SQL_FETCH_NEXT 會傳回使用者和系統 dsn。 當 *方向* 設定為 SQL_FETCH_FIRST_USER 時，對 **SQLDataSources** 的所有後續呼叫都會將 *方向* 設為 SQL_FETCH_NEXT 只會傳回使用者 dsn。 當 *方向* 設定為 SQL_FETCH_FIRST_SYSTEM 時，對 **SQLDataSources** 的所有後續呼叫都會將 *方向* 設為 SQL_FETCH_NEXT 只會傳回系統 dsn。  
  
 *ServerName*  
 出要傳回資料來源名稱之緩衝區的指標。  
  
 如果 *ServerName* 為 Null， *NameLength1Ptr* 仍會傳回字元總數 (排除字元資料的 Null 終止字元) 可在 *servername*所指向的緩衝區中傳回。  
  
 *BufferLength1*  
 輸出**ServerName* 緩衝區的長度（以字元為單位）;這不需要超過 SQL_MAX_DSN_LENGTH 加上 null 終止字元。  
  
 *NameLength1Ptr*  
 出緩衝區的指標，此緩衝區會傳回字元總數 (不包括 null 終止字元) 可在 \* *ServerName*中傳回。 如果可傳回的字元數大於或等於*BufferLength1*，會將 ServerName 中的資料來源名稱 \* *ServerName*截斷為*BufferLength1*減去 null 終止字元的長度。  
  
 *說明*  
 出緩衝區的指標，此緩衝區會傳回與資料來源相關聯之驅動程式的描述。 例如，dBASE 或 SQL Server。  
  
 如果 *Description* 為 Null， *NameLength2Ptr* 仍會傳回字元總數 (排除字元資料的 Null 終止字元) 可在 *描述*所指向的緩衝區中傳回。  
  
 *BufferLength2*  
 輸出**描述* 緩衝區的字元長度（以字元為單位）。  
  
 *NameLength2Ptr*  
 出緩衝區的指標，此緩衝區會傳回字元總數 (不包括 null 終止字元) 可在 \* *描述*中傳回。 如果可傳回的字元數大於或等於*BufferLength2*，則描述中的驅動程式描述 \* *Description*會截斷為*BufferLength2*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDataSources**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_ENV）和*EnvironmentHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLDataSources** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告| (DM) 驅動程式管理員特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷| (DM) 緩衝區 \* *伺服器*名稱不夠大，無法傳回完整的資料來源名稱。 因此，名稱已被截斷。 整個資料來源名稱的長度會在 NameLength1Ptr 中傳回 \* * *。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) <br /><br />  (DM) 緩衝區 \* *描述*不夠大，無法傳回完整的驅動程式描述。 因此，描述已被截斷。 Untruncated 資料來源描述的長度會在 **NameLength2Ptr*中傳回。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|HY000|一般錯誤| (DM) 發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤| (DM) 驅動程式管理員無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤|針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 引數 *BufferLength1* 指定的值小於0。<br /><br />  (DM) 引數 *BufferLength2* 指定的值小於0。|  
|HY103|不正確抓取碼| (DM) 引數 *方向* 指定的值不等於 SQL_FETCH_FIRST、SQL_FETCH_FIRST_USER、SQL_FETCH_FIRST_SYSTEM 或 SQL_FETCH_NEXT。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>註解  
 因為 **SQLDataSources** 是在驅動程式管理員中執行，所以無論特定驅動程式的標準合規性為何，所有驅動程式都支援此功能。  
  
 應用程式可以多次呼叫 **SQLDataSources** 來取出所有資料來源名稱。 驅動程式管理員會從系統資訊抓取此資訊。 如果沒有更多的資料來源名稱，驅動程式管理員會傳回 SQL_NO_DATA。 如果使用 SQL_FETCH_NEXT 在傳回 SQL_NO_DATA 之後立即呼叫 **SQLDataSources** ，它會傳回第一個資料來源名稱。 如需應用程式如何使用 **SQLDataSources**所傳回信息的相關資訊，請參閱 [選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果 SQL_FETCH_NEXT 是在第一次呼叫時傳遞給 **SQLDataSources** ，它會傳回第一個資料來源名稱。  
  
 驅動程式會決定資料來源名稱如何對應到實際的資料來源。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|探索和列出連接到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連線到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|使用連接字串或對話方塊連接到資料來源|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回驅動程式描述和屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
