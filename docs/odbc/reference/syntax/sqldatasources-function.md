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
manager: craigg
ms.openlocfilehash: b7b04dc2554b820fc6ac8344457754aae984d4b8
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53213107"
---
# <a name="sqldatasources-function"></a>SQLDataSources 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLDataSources**傳回的資料來源的相關資訊。 此函數會實作僅由驅動程式管理員。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 [輸入]環境控制代碼。  
  
 *方向*  
 [輸入]判斷哪一個資料來源驅動程式管理員相關資訊傳回。 可為以下項目：  
  
 （若要擷取清單中的下一個資料來源名稱） 的 SQL_FETCH_NEXT，SQL_FETCH_FIRST （若要擷取清單的開頭）、 SQL_FETCH_FIRST_USER （若要擷取第一個使用者 DSN） 或 SQL_FETCH_FIRST_SYSTEM （若要擷取的第一個系統 DSN）。  
  
 當*方向*設為 SQL_FETCH_FIRST，後續呼叫**SQLDataSources**使用*方向*SQL_FETCH_NEXT 設傳回使用者和系統名稱 （dsn）。 當*方向*設為 SQL_FETCH_FIRST_USER，所有的後續呼叫**SQLDataSources**與*方向*SQL_FETCH_NEXT 設傳回只有使用者名稱 （dsn）。 當*方向*設為 SQL_FETCH_FIRST_SYSTEM，所有的後續呼叫**SQLDataSources**與*方向*SQL_FETCH_NEXT 設傳回系統 Dsn。  
  
 *ServerName*  
 [輸出]在其中傳回的資料來源名稱之緩衝區的指標。  
  
 如果*ServerName*為 NULL，就*NameLength1Ptr*仍會傳回 （不含字元資料的 null 終止字元） 的字元總數可用來傳回中所指向的緩衝區*ServerName*。  
  
 *BufferLength1*  
 [輸入]長度 **ServerName*緩衝區，以字元為單位; 這不需要為超過 SQL_MAX_DSN_LENGTH 加上 null 結束字元。  
  
 *NameLength1Ptr*  
 [輸出]在其中傳回 （不包括 null 結束字元） 的字元總數緩衝區的指標來傳回在可用\* *ServerName*。 可用來傳回字元的數目是否大於或等於*BufferLength1*中的資料來源名稱\* *ServerName*會被截斷成*BufferLength1*減去 null 結束字元的長度。  
  
 *說明*  
 [輸出]在其中傳回的資料來源相關聯的驅動程式描述緩衝區的指標。 比方說，dBASE 或 SQL Server。  
  
 如果*描述*為 NULL，就*NameLength2Ptr*仍會傳回 （不含字元資料的 null 終止字元） 的字元總數可用來傳回中所指向的緩衝區*描述*。  
  
 *BufferLength2*  
 [輸入]中的字元長度 **描述*緩衝區。  
  
 *NameLength2Ptr*  
 [輸出]在其中傳回 （不包括 null 結束字元） 的字元總數緩衝區的指標來傳回在可用\**描述*。 可用來傳回字元的數目是否大於或等於*BufferLength2*中的驅動程式說明\**描述*會被截斷成*BufferLength2*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDataSources**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可取得相關聯的 SQLSTATE 值，請呼叫**SQLGetDiagRec**使用*HandleType*SQL_HANDLE_ENV 的和 a*處理*的*EnvironmentHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDataSources** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|(DM) 驅動程式管理員特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|(DM) 緩衝區\* *ServerName*仍不夠大，無法傳回完整的資料來源的名稱。 因此，名稱已被截斷。 中會傳回整個資料來源名稱的長度\* *NameLength1Ptr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> (DM) 緩衝區\**描述*仍不夠大，無法傳回完整的驅動程式的描述。 因此，描述已遭截斷。 未截斷的資料來源描述的長度會傳入 **NameLength2Ptr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|(DM) 發生錯誤，其中沒有任何特定的 SQLSTATE 和已定義的任何實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式管理員 」 (DM) 無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*BufferLength1*為小於 0。<br /><br /> (DM) 引數指定的值*BufferLength2*為小於 0。|  
|HY103|無效的擷取程式碼|(DM) 引數指定的值*方向*未 SQL_FETCH_FIRST、 SQL_FETCH_FIRST_USER、 SQL_FETCH_FIRST_SYSTEM 或 SQL_FETCH_NEXT 相同。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>註解  
 因為**SQLDataSources**實作在驅動程式管理員 中，它支援所有的驅動程式，不論特定驅動程式的標準相容性。  
  
 應用程式可以呼叫**SQLDataSources**多次，以便擷取所有的資料來源名稱。 驅動程式管理員會將這項資訊擷取系統資訊。 沒有更多的資料來源名稱時，驅動程式管理員會傳回 sql_no_data 為止。 如果**SQLDataSources** SQL_FETCH_NEXT 它傳回 SQL_NO_DATA 之後，它會傳回第一個資料來源的名稱，請立即呼叫。 如需應用程式如何使用傳回的資訊**SQLDataSources**，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果傳遞至 SQL_FETCH_NEXT **SQLDataSources**第一次呼叫它時，它會傳回第一個資料來源的名稱。  
  
 驅動器會決定如何將資料來源名稱對應到實際的資料來源。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|探索並列出連接到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回的驅動程式描述和屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
