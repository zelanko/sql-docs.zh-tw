---
title: SQLDataSources 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6de6bf96c05925e9044be5955036cd9c663501a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqldatasources-function"></a>SQLDataSources 函式
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
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
 [輸入]判斷哪一個資料來源驅動程式管理員會傳回資訊的相關。 可為以下項目：  
  
 SQL_FETCH_NEXT （若要擷取清單中的下一個資料來源名稱）、 （若要從清單開頭提取） SQL_FETCH_FIRST SQL_FETCH_FIRST_USER （若要擷取第一個使用者 DSN） 或 SQL_FETCH_FIRST_SYSTEM （來擷取第一個系統 DSN）。  
  
 當*方向*設 SQL_FETCH_FIRST，後續呼叫**SQLDataSources**與*方向*設 SQL_FETCH_NEXT 傳回使用者和系統 Dsn。 當*方向*設 SQL_FETCH_FIRST_USER，所有後續呼叫**SQLDataSources**與*方向*設 SQL_FETCH_NEXT 傳回只有使用者名稱 （dsn）。 當*方向*設 SQL_FETCH_FIRST_SYSTEM，所有後續呼叫**SQLDataSources**與*方向*設 SQL_FETCH_NEXT 傳回系統 Dsn。  
  
 *ServerName*  
 [輸出]這是要傳回的資料來源名稱的緩衝區指標。  
  
 如果*ServerName*是 NULL， *NameLength1Ptr*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回中所指向的緩衝區*ServerName*。  
  
 *BufferLength1*  
 [輸入]長度 **ServerName*緩衝區，以字元為單位; 這不需要超過 SQL_MAX_DSN_LENGTH 加上 null 結束字元。  
  
 *NameLength1Ptr*  
 [輸出]這是要傳回的總字元數 （不包括 null 結束字元） 中的緩衝區指標可用來傳回中\* *ServerName*。 可傳回的字元數目是否大於或等於*BufferLength1*中的資料來源名稱\* *ServerName*會被截斷成*BufferLength1*減去 null 結束字元的長度。  
  
 *說明*  
 [輸出]這是要傳回的資料來源相關聯的驅動程式描述的緩衝區指標。 例如，dBASE 或 SQL Server。  
  
 如果*描述*是 NULL， *NameLength2Ptr*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回中所指向的緩衝區*描述*。  
  
 *BufferLength2*  
 [輸入]中的字元長度 **描述*緩衝區。  
  
 *NameLength2Ptr*  
 [輸出]這是要傳回的總字元數 （不包括 null 結束字元） 中的緩衝區指標可用來傳回中\**描述*。 可傳回的字元數目是否大於或等於*BufferLength2*中的驅動程式描述\**描述*會被截斷成*BufferLength2*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDataSources**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以藉由呼叫取得相關聯的 SQLSTATE 值**SQLGetDiagRec**與*HandleType*利用 SQL_HANDLE_ENV 的和*處理*的*EnvironmentHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDataSources** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|(DM) 驅動程式管理員特有的資訊訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|(DM) 緩衝區\* *ServerName*仍不夠大，無法傳回完整的資料來源名稱。 因此，名稱被截斷。 中會傳回整個資料來源名稱的長度\* *NameLength1Ptr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> (DM) 緩衝區\**描述*仍不夠大，無法傳回完整的驅動程式描述。 因此，描述已截斷。 中會傳回未截斷的資料來源描述的長度 **NameLength2Ptr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|(DM) 發生錯誤，其中沒有任何特定的 SQLSTATE 和不定義的任何實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|(DM) 驅動程式管理員無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*BufferLength1*小於 0。<br /><br /> (DM) 引數指定的值*BufferLength2*小於 0。|  
|HY103|無效的擷取程式碼|(DM) 指定的引數的值*方向*不等於 SQL_FETCH_FIRST、 SQL_FETCH_FIRST_USER、 SQL_FETCH_FIRST_SYSTEM 或 SQL_FETCH_NEXT。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>註解  
 因為**SQLDataSources**實作驅動程式管理員 中會支援它所有的驅動程式，不論特定驅動程式標準相容性。  
  
 應用程式可以呼叫**SQLDataSources**多次，以便擷取所有資料來源名稱。 驅動程式管理員會將此資訊擷取系統資訊。 沒有更多的資料來源名稱時，驅動程式管理員會傳回 sql_no_data 為止。 如果**SQLDataSources** SQL_FETCH_NEXT 它傳回 SQL_NO_DATA 之後，它會傳回第一個資料來源名稱，立即呼叫。 如需有關應用程式如何使用所傳回的資訊資訊**SQLDataSources**，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果傳遞至 SQL_FETCH_NEXT **SQLDataSources**非常第一次呼叫時，它會傳回第一個資料來源名稱。  
  
 驅動程式判斷資料來源名稱會對應至實際的資料來源的方式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|探索及列出連接到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回的驅動程式描述和屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
