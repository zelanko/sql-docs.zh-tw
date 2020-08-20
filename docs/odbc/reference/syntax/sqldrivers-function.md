---
description: SQLDrivers 函式
title: SQLDrivers 函式 |Microsoft Docs
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
ms.openlocfilehash: 9abe7502b7efcfba695bd58081752342504378ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461160"
---
# <a name="sqldrivers-function"></a>SQLDrivers 函式
**一致性**  
 引進的版本： ODBC 2.0 標準合規性： ODBC  
  
 **總結**  
 **SQLDrivers** 會列出驅動程式描述和驅動程式屬性關鍵字。 此函數只會由驅動程式管理員執行。  
  
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
 *EnvironmentHandle*  
 輸出環境控制碼。  
  
 *方向*  
 輸出決定驅動程式管理員是否要在清單中提取下一個驅動程式描述 (SQL_FETCH_NEXT) 或搜尋是否從清單的開頭開始 (SQL_FETCH_FIRST) 。  
  
 *DriverDescription*  
 出要在其中傳回驅動程式描述的緩衝區指標。  
  
 如果 *DriverDescription* 是 Null， *DescriptionLengthPtr* 仍會傳回字元總數 (排除字元資料的 Null 終止字元) 可在 *DriverDescription*所指向的緩衝區中傳回。  
  
 *BufferLength1*  
 輸出**DriverDescription* 緩衝區的長度（以字元為單位）。  
  
 *DescriptionLengthPtr*  
 出緩衝區的指標，此緩衝區會傳回字元總數 (不包括 null 終止字元) 可在 \* *DriverDescription*中傳回。 如果可傳回的字元數大於或等於*BufferLength1*，DriverDescription 中的驅動程式描述 \* *DriverDescription*會截斷為*BufferLength1*減去 null 終止字元的長度。  
  
 *DriverAttributes*  
 出要傳回驅動程式屬性值組清單的緩衝區指標 (請參閱「批註」 ) 。  
  
 如果 *DriverAttributes* 為 Null， *AttributesLengthPtr* 仍會傳回位元組總數 (排除字元資料的 Null 終止字元) 可在 *DriverAttributes*所指向的緩衝區中傳回。  
  
 *BufferLength2*  
 輸出\* *DriverAttributes*緩衝區的長度（以字元為單位）。 如果* \* DriverDescription*值是在呼叫**SQLDriversW**) 時 (的 Unicode 字串，則*BufferLength*引數必須是偶數。  
  
 *AttributesLengthPtr*  
 出緩衝區的指標，此緩衝區會傳回位元組總數 (不包括 null 終止位元組) 可在 \* *DriverAttributes*中傳回。 如果可傳回的位元組數目大於或等於*BufferLength2*，DriverAttributes 中的屬性值組清單 \* *DriverAttributes*會被截斷為*BufferLength2*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDrivers**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_ENV）和*EnvironmentHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLDrivers** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告| (DM) 驅動程式管理員特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷| (DM) 緩衝區 \* *DriverDescription*不夠大，無法傳回完整的驅動程式描述。 因此，描述已被截斷。 完整驅動程式描述的長度會在 \* *DescriptionLengthPtr*中傳回。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) <br /><br />  (DM) 緩衝區 \* *DriverAttributes*不夠大，無法傳回屬性值配對的完整清單。 因此，清單已被截斷。 **AttributesLengthPtr*中會傳回屬性值組的 untruncated 清單長度。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤| (DM) 驅動程式管理員無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤|針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 引數 *BufferLength1* 指定的值小於0。<br /><br />  (DM) 引數 *BufferLength2* 指定的值小於0或等於1。|  
|HY103|不正確抓取碼| (DM) 引數 *方向* 指定的值不等於 SQL_FETCH_FIRST 或 SQL_FETCH_NEXT。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>註解  
 **SQLDrivers**會在 \* *DriverDescription*緩衝區中傳回驅動程式描述。 它會傳回 DriverAttributes 緩衝區中驅動程式的其他相關資訊 \* *DriverAttributes* ，做為關鍵字-值組的清單。 所有驅動程式都會傳回所有驅動程式之系統資訊中所列的所有關鍵詞，但 **CreateDSN**除外，後者是用來提示建立資料來源，因此是選擇性的。 每一組都會以 null 位元組結束，且完整清單會以 null 位元組結束 (也就是兩個 null 位元組標記清單結尾) 。 例如，使用 C 語法的檔案驅動驅動程式可能會傳回下列屬性清單 ( "\ 0" 代表 null 字元) ：  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 如果 \* *DriverAttributes*不夠大，無法容納整個清單，則會截斷清單、 **SQLDrivers**會傳回 SQLSTATE 01004 (資料已截斷) ，而清單的長度 (不包含最終 null 終止位元組) 會在 **AttributesLengthPtr*中傳回。  
  
 安裝驅動程式時，系統資訊會加入驅動程式屬性關鍵字。 如需詳細資訊，請參閱 [安裝 ODBC 元件](../../../odbc/reference/install/installing-odbc-components.md)。  
  
 應用程式可以多次呼叫 **SQLDrivers** 來取得所有驅動程式描述。 驅動程式管理員會從系統資訊抓取此資訊。 當沒有其他驅動程式描述時， **SQLDrivers** 會傳回 SQL_NO_DATA。 如果使用 SQL_FETCH_NEXT 在傳回 SQL_NO_DATA 之後立即呼叫 **SQLDrivers** ，它會傳回第一個驅動程式描述。 如需應用程式如何使用 **SQLDrivers**所傳回信息的相關資訊，請參閱 [選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果 SQL_FETCH_NEXT 在第一次呼叫時傳遞至 **SQLDrivers** ， **SQLDrivers** 會傳回第一個資料來源名稱。  
  
 因為 **SQLDrivers** 是在驅動程式管理員中執行，所以無論特定驅動程式的標準合規性為何，所有驅動程式都支援此功能。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|探索和列出連接到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連線到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|傳回資料來源名稱|[SQLDataSources 函式](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|使用連接字串或對話方塊連接到資料來源|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
