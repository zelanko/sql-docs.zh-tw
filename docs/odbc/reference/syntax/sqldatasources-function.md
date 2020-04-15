---
title: SQLData源函數 |微軟文件
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
ms.openlocfilehash: b56a6c25e54897e67beaf39d3b7797ac45391d7b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301178"
---
# <a name="sqldatasources-function"></a>SQLDataSources 函式
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLDataSource**傳回有關資料來源的資訊。 此函數僅由驅動程式管理員實現。  
  
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
 *環境處理*  
 [輸入]環境句柄。  
  
 *方向*  
 [輸入]確定驅動程式管理員返回的資訊來源。 可為以下項目：  
  
 SQL_FETCH_NEXT(獲取清單中的下一個數據源名稱)、SQL_FETCH_FIRST(從清單開頭提取)、SQL_FETCH_FIRST_USER(獲取第一個使用者 DSN)或SQL_FETCH_FIRST_SYSTEM(獲取第一個系統 DSN)。  
  
 當*方向*設置為SQL_FETCH_FIRST時,後續對**SQLDataSources***的調用*設置為SQL_FETCH_NEXT返回使用者和系統 DSN。 當*方向*設置為SQL_FETCH_FIRST_USER時,所有後續對**SQLDataSources***的調用*,方向設置為SQL_FETCH_NEXT僅返回使用者 DSN。 當*方向*設置為SQL_FETCH_FIRST_SYSTEM時,所有後續對**SQLDataSources**的調用(*方向*設置為SQL_FETCH_NEXT僅返回系統 DSN。  
  
 *ServerName*  
 【輸出]指向要返回數據源名稱的緩衝區的指標。  
  
 如果*伺服器名稱*為*NULL,NameLength1Ptr*仍將傳回字元總數(不包括字元資料的空終止字元),這些字元可在*伺服器名稱*指向的緩衝區中返回。  
  
 *緩衝區長度1*  
 [輸入]**伺服器名稱*緩衝區的長度(以字元表示);這不需要超過SQL_MAX_DSN_LENGTH加上 null 終止字元。  
  
 *名稱長度1Ptr*  
 【輸出]指向緩衝區的指標,其中返回可在\**ServerName*中傳回的字元總數(不包括空終止字元)。 如果可供返回的字元數大於或等於*BufferLength1,* 則\**ServerName*中的數據來源名稱將截斷為*BufferLength1*減去空終止字元的長度。  
  
 *說明*  
 【輸出]指向緩衝區的指標,用於返回與數據源關聯的驅動程序的說明。 例如,dBASE或 SQL 伺服器。  
  
 如果*描述*為*NULL,NameLength2Ptr*仍將傳回字元總數(不包括字元資料的空終止字元),這些字元可在*描述*指向的緩衝區中返回。  
  
 *緩衝區長度2*  
 [輸入]**描述*緩衝區的字元的長度。  
  
 *名稱長度2Ptr*  
 【輸出]指向緩衝區的指標,其中返回可在\**「描述」* 中返回的字元總數(不包括空終止字元)。 如果可返回的字元數大於或等於*BufferLength2,* 則\**「描述」* 中的驅動程式描述將截斷為*BufferLength2*減去空終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDataSources**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以通過調用**SQLGetDiagRec**獲取關聯的 SQLSTATE*Handle*值,該值具有SQL_HANDLE_ENV 的*句柄類型*和環境*句柄*句柄。 下表列出了**SQLDataSources**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|(DM) 特定於驅動程式管理員的資訊訊息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|(DM) 緩衝\*區*伺服器名稱*不夠大,無法返回完整的數據源名稱。 因此,名稱被截斷。 整個資料來源名稱的長度在\**NameLength1Ptr*中傳回。 (函數返回SQL_SUCCESS_WITH_INFO。<br /><br /> (DM) 緩衝\*區*描述*不夠大,無法返回完整的驅動程序說明。 因此,描述被截斷。 未壓縮的資料來源描述的長度在 #*NameLength2Ptr*中傳回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|HY000|一般錯誤|(DM) 發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|(DM) 驅動程式管理員無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 為參數*BufferLength1*指定的值小於 0。<br /><br /> (DM) 為參數*BufferLength2*指定的值小於 0。|  
|HY103|不合法的索代碼|(DM) 為參數*方向*指定的值不等於SQL_FETCH_FIRST、SQL_FETCH_FIRST_USER、SQL_FETCH_FIRST_SYSTEM 或SQL_FETCH_NEXT。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>註解  
 由於**SQLDataSources**是在驅動程式管理器中實現的,因此無論特定驅動程序的標準符合性如何,它都支援所有驅動程式。  
  
 應用程式可以多次調用**SQLDataSource**來檢索所有數據源名稱。 驅動程式管理器從系統資訊中檢索此資訊。 當不再有數據源名稱時,驅動程式管理器將返回SQL_NO_DATA。 如果在**SQLDataSource**返回SQL_NO_DATA後立即用 SQL_FETCH_NEXT 調用它,它將返回第一個數據原始名稱。 有關應用程式如何使用**SQLDataSource**傳回的資訊的資訊,請參考[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果SQL_FETCH_NEXT在第一次調用時傳遞給**SQLDataSource,** 它將返回第一個數據原始名稱。  
  
 驅動程序確定數據源名稱如何映射到實際數據源。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|發現並列出連線到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|使用連接字串或對話框連接到資料來源|[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回驅動程式描述與屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
