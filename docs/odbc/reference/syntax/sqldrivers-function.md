---
title: SQL驅動程式功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDrivers
helpviewer_keywords:
- SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2496e7cd5f2abe0831c72484bed374d7aa1513ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302759"
---
# <a name="sqldrivers-function"></a>SQLDrivers 函式
**一致性**  
 版本介紹: ODBC 2.0 標準合規性: ODBC  
  
 **摘要**  
 **SQLDriver**列出了驅動程式描述和驅動程式屬性關鍵字。 此函數僅由驅動程式管理員實現。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLDrivers(  
     SQLHENV         EnvironmentHandle,  
     SQLUSMALLINT    Direction,  
     SQLCHAR *       DriverDescription,  
     SQLSMALLINT     BufferLength1,  
     SQLSMALLINT *   DescriptionLengthPtr,  
     SQLCHAR *       DriverAttributes,  
     SQLSMALLINT     BufferLength2,  
     SQLSMALLINT *   AttributesLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *環境處理*  
 [輸入]環境句柄。  
  
 *方向*  
 [輸入]確定驅動程式管理器是獲取清單中的下一個驅動程式說明(SQL_FETCH_NEXT),還是搜索從清單開頭 (SQL_FETCH_FIRST) 開始。  
  
 *驅動程式描述*  
 【輸出]指向要返回驅動程式描述的緩衝區的指標。  
  
 如果*驅動程式描述*為 NULL,*則描述長度 Ptr*仍將傳回字元總數(不包括字元資料的空終止字元),這些字元可在*驅動程式描述*指向的緩衝區中返回。  
  
 *緩衝區長度1*  
 [輸入]**驅動程式描述*緩衝區的長度(以字元表示)。  
  
 *描述長度*  
 【輸出]指向緩衝區的指標,其中返回可在\**Driver 描述*中返回的字元總數(不包括空終止字元)。 如果可返回的字元數大於或等於*BufferLength1,* 則\**驅動程式描述中的驅動程式描述*將截斷為*BufferLength1*減去空終止字元的長度。  
  
 *驅動程式屬性*  
 【輸出]指向要返回驅動程式屬性值對清單的緩衝區的指標(請參閱"註釋"  
  
 如果*驅動程式屬性*為 NULL,*屬性長度 Ptr*仍將傳回*可用的驅動程式屬性*指向的緩衝區中的位元總數(不包括字元資料的空終止字元)。  
  
 *緩衝區長度2*  
 [輸入]\**驅動程式屬性*緩衝區的長度(以字元表示)。 如果*\*Driver 描述*值是 Unicode 字串(在呼叫**SQLDriverW**時),*緩衝區長度*參數必須是偶數。  
  
 *屬性長度Ptr*  
 【輸出]指向緩衝區的指標,用於返回可在\**DriverAttributes*中返回的位元組總數(不包括空終止位元組)。 如果可供返回的位元組數大於或等於*BufferLength2,* 則\**DriverAttributes*中的屬性值對清單將截斷為*BufferLength2*減去空終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDrivers**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以通過調用**SQLGetDiagRec**獲取關聯的 SQLSTATE*Handle*值,該值具有SQL_HANDLE_ENV 的*句柄類型*和環境*句柄*句柄。 下表列出了**SQLDRIVERS**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|(DM) 特定於驅動程式管理員的資訊訊息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|(DM) 緩衝\*區*驅動程式描述*不夠大,無法返回完整的驅動程序說明。 因此,描述被截斷。 完整的驅動程式描述的長度在\**描述長度Ptr*中返回。 (函數返回SQL_SUCCESS_WITH_INFO。<br /><br /> (DM) 緩衝\*區*驅動程式屬性*不夠大,無法返回屬性值對的完整清單。 因此,清單被截斷。 屬性值對的未壓縮清單的長度在 **屬性長度Ptr*中返回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|(DM) 驅動程式管理員無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 為參數*BufferLength1*指定的值小於 0。<br /><br /> (DM) 為參數*BufferLength2*指定的值小於 0 或等於 1。|  
|HY103|不合法的索代碼|(DM) 為參數*方向*指定的值不等於SQL_FETCH_FIRST或SQL_FETCH_NEXT。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>註解  
 **SQLDriver**在驅動程式描述緩衝區\*中傳回*驅動程式說明*。 它將有關\**DriverAttributes*緩衝區中的驅動程式的其他資訊作為關鍵字-值對的清單。 驅動程式的系統資訊中列出的所有關鍵字都將返回所有驅動程式,但**CreateDSN**除外,它用於提示數據源的創建,因此是可選的。 每個對都用空位元節終止,並且整個清單用空位元組終止(即,兩個空位元組標記清單的末尾)。 例如,使用 C 語法的基於檔案的驅動程式可能會傳回以下屬性清單(「\0」表示空字元):  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 如果\* *DriverAttributes*不夠大以容納整個清單,則清單將被截斷 **,SQLDriver**返回 SQLSTATE 01004(數據截斷),並且列表的長度(不包括最終的 null 終止位元組)在 #*屬性 LengthPtr*中返回。  
  
 安裝驅動程式時,將從系統資訊中添加驅動程式屬性關鍵字。 有關詳細資訊,請參閱安裝[ODBC 元件](../../../odbc/reference/install/installing-odbc-components.md)。  
  
 應用程式可以多次調用**SQLDriver**來檢索所有驅動程式說明。 驅動程式管理器從系統資訊中檢索此資訊。 當不再有驅動程式描述時 **,SQLDriver**將返回SQL_NO_DATA。 如果在**SQLDriver**返回SQL_NO_DATA後立即調用 SQL_FETCH_NEXT,它將返回第一個驅動程序說明。 有關應用程式如何使用**SQLDriver**傳回的資訊的資訊,請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果SQL_FETCH_NEXT在第一次調用時傳遞給**SQLDrivers,****則 SQLDrivers**將返回第一個數據原始名稱。  
  
 由於**SQLDriver**是在驅動程式管理器中實現的,因此無論特定驅動程序的標準符合性如何,它都支援所有驅動程式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|發現並列出連線到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|傳回資料來源名稱|[SQLDataSources 函式](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|使用連接字串或對話框連接到資料來源|[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
