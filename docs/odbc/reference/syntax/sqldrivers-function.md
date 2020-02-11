---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f54be3d11f4870533513f464c1afdae13e04f367
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104657"
---
# <a name="sqldrivers-function"></a>SQLDrivers 函式
**標準**  
 引進的版本： ODBC 2.0 標準合規性： ODBC  
  
 **摘要**  
 **SQLDrivers**列出驅動程式描述和驅動程式屬性關鍵字。 此函式只會由驅動程式管理員執行。  
  
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
 源環境控制碼。  
  
 *方向*  
 源決定驅動程式管理員是否提取清單中的下一個驅動程式描述（SQL_FETCH_NEXT），或搜尋是否從清單的開頭（SQL_FETCH_FIRST）開始。  
  
 *DriverDescription*  
 輸出要在其中傳回驅動程式描述的緩衝區指標。  
  
 如果*DriverDescription*為 Null， *DescriptionLengthPtr*仍會傳回*DriverDescription*所指向的緩衝區中可傳回的字元總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength1*  
 源**DriverDescription*緩衝區的長度（以字元為單位）。  
  
 *DescriptionLengthPtr*  
 輸出緩衝區的指標，要在其中傳回\* *DriverDescription*中可傳回的字元總數（不包括 null 終止字元）。 如果可傳回的字元數大於或等於*BufferLength1*， \* *DriverDescription*中的驅動程式描述會截斷為*BufferLength1*減去 null 終止字元的長度。  
  
 *DriverAttributes*  
 輸出緩衝區的指標，要在其中傳回驅動程式屬性值組的清單（請參閱「批註」）。  
  
 如果*DriverAttributes*為 Null， *AttributesLengthPtr*仍會傳回*DriverAttributes*所指向的緩衝區中可傳回的位元組總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength2*  
 源\* *DriverAttributes*緩衝區的長度（以字元為單位）。 如果* \*DriverDescription*值是 Unicode 字串（在呼叫**SQLDriversW**時），則*BufferLength*引數必須是偶數。  
  
 *AttributesLengthPtr*  
 輸出緩衝區的指標，要在其中傳回\* *DriverAttributes*中可傳回的位元組總數（不包括 null 終止位元組）。 如果可傳回的位元組數目大於或等於*BufferLength2*， \* *DriverAttributes*中的屬性值組清單會截斷為*BufferLength2*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDrivers**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_ENV *HandleType*和*EnvironmentHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出通常由**SQLDrivers**所傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|（DM）驅動程式管理員特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|（DM）緩衝區\* *DriverDescription*不夠大，無法傳回完整的驅動程式描述。 因此，描述已被截斷。 完整驅動程式描述的長度會在\* *DescriptionLengthPtr*中傳回。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> （DM）緩衝區\* *DriverAttributes*不夠大，無法傳回完整的屬性值組清單。 因此，清單已遭截斷。 屬性值配對的 untruncated 清單長度會在 **AttributesLengthPtr*中傳回。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|（DM）驅動程式管理員無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|（DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）為引數*BufferLength1*指定的值小於0。<br /><br /> （DM）為引數*BufferLength2*指定的值小於0或等於1。|  
|HY103|不正確抓取程式碼|（DM）為引數*方向*指定的值不等於 SQL_FETCH_FIRST 或 SQL_FETCH_NEXT。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
  
## <a name="comments"></a>註解  
 **SQLDrivers**會傳回\* *DriverDescription*緩衝區中的驅動程式描述。 它會在\* *DriverAttributes*緩衝區中傳回有關驅動程式的其他資訊，作為關鍵字-值組的清單。 除了**CreateDSN**之外，所有驅動程式的系統資訊中所列的所有關鍵詞都會傳回，這是用來提示建立資料來源，因此是選擇性的。 每個配對都會以 null 位元組結束，而完整的清單會以 null 位元組結束（也就是兩個 null 位元組會標示清單結尾）。 例如，以檔案為基礎的驅動程式（使用 C 語法）可能會傳回下列屬性清單（"\ 0" 代表 null 字元）：  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 如果\* *DriverAttributes*不夠大，無法保存整個清單，則清單會被截斷， **SQLDrivers**會傳回 SQLSTATE 01004 （資料已截斷），而清單的長度（不包括最終 null 終止位元組）則會在 **AttributesLengthPtr*中傳回。  
  
 安裝驅動程式時，會從系統資訊新增驅動程式屬性關鍵字。 如需詳細資訊，請參閱[安裝 ODBC 元件](../../../odbc/reference/install/installing-odbc-components.md)。  
  
 應用程式可以多次呼叫**SQLDrivers** ，以取得所有驅動程式描述。 驅動程式管理員會從系統資訊抓取這則資訊。 當沒有其他驅動程式描述時， **SQLDrivers**會傳回 SQL_NO_DATA。 如果**SQLDrivers**在傳回 SQL_NO_DATA 後立即以 SQL_FETCH_NEXT 呼叫，它會傳回第一個驅動程式描述。 如需有關應用程式如何使用**SQLDrivers**傳回之資訊的詳細資訊，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果 SQL_FETCH_NEXT 在第一次呼叫時傳遞至**SQLDrivers** ， **SQLDrivers**會傳回第一個資料來源名稱。  
  
 由於**SQLDrivers**是在驅動程式管理員中執行，因此支援所有驅動程式，而不論特定驅動程式的標準合規性為何。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|探索和列出連接至資料來源所需的值|[SQLBrowseConnect 函數](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|傳回資料來源名稱|[SQLDataSources 函式](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|使用連接字串或對話方塊連接到資料來源|[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
