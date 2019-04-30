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
manager: craigg
ms.openlocfilehash: bac7f88dcbd9895cfd0d07a5993ab9e38a4608d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061896"
---
# <a name="sqldrivers-function"></a>SQLDrivers 函式
**合規性**  
 導入的版本：ODBC 2.0 標準合規性：ODBC  
  
 **摘要**  
 **SQLDrivers**列出驅動程式的描述以及驅動程式屬性的關鍵字。 此函數會實作僅由驅動程式管理員。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 [輸入]環境控制代碼。  
  
 *方向*  
 [輸入]判斷驅動程式管理員是否會擷取下一個驅動程式中的說明 (SQL_FETCH_NEXT) 的清單，或是否從清單 (SQL_FETCH_FIRST) 的開頭開始搜尋。  
  
 *DriverDescription*  
 [輸出]在其中傳回的驅動程式描述緩衝區的指標。  
  
 如果*DriverDescription*為 NULL，就*DescriptionLengthPtr*仍會傳回 （不含字元資料的 null 終止字元） 的字元總數可用來傳回中所指向的緩衝區*DriverDescription*。  
  
 *BufferLength1*  
 [輸入]長度 **DriverDescription*緩衝區，以字元為單位。  
  
 *DescriptionLengthPtr*  
 [輸出]在其中傳回 （不包括 null 結束字元） 的字元總數緩衝區的指標來傳回在可用\* *DriverDescription*。 可用來傳回字元的數目是否大於或等於*BufferLength1*中的驅動程式說明\* *DriverDescription*會被截斷成*BufferLength1*減去 null 結束字元的長度。  
  
 *DriverAttributes*  
 [輸出]這是要傳回的驅動程式 （請參閱 「 註解 」） 的屬性值組清單中的緩衝區的指標。  
  
 如果*DriverAttributes*為 NULL，就*AttributesLengthPtr*仍會傳回的總位元組數 （不含字元資料之 null 結束字元） 可用來傳回緩衝區中指向*DriverAttributes*。  
  
 *BufferLength2*  
 [輸入]長度\* *DriverAttributes*緩衝區，以字元為單位。 如果 *\*DriverDescription*值為 Unicode 字串 (呼叫時**SQLDriversW**)，則*Columnsize*引數必須是偶數。  
  
 *AttributesLengthPtr*  
 [輸出]在其中傳回的總位元組數 （不含終止 null 位元組） 緩衝區的指標來傳回在可用\* *DriverAttributes*。 如果傳回可用的位元組數目大於或等於*BufferLength2*，清單中的屬性值組\* *DriverAttributes*會被截斷成*BufferLength2*減去之 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDrivers**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可取得相關聯的 SQLSTATE 值，請呼叫**SQLGetDiagRec**具有*HandleType*的SQL_HANDLE_ENV 並*處理*的*EnvironmentHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDrivers** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|(DM) 驅動程式管理員特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|(DM) 緩衝區\* *DriverDescription*仍不夠大，無法傳回完整的驅動程式的描述。 因此，描述已遭截斷。 完整的驅動程式描述的長度會傳入\* *DescriptionLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> (DM) 緩衝區\* *DriverAttributes*仍不夠大，無法傳回屬性值組的完整清單。 因此，清單已截斷。 中傳回的屬性值組未截斷的清單長度 **AttributesLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式管理員 」 (DM) 無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*BufferLength1*為小於 0。<br /><br /> (DM) 引數指定的值*BufferLength2*為小於 0 或等於 1。|  
|HY103|無效的擷取程式碼|(DM) 引數指定的值*方向*不是等於 SQL_FETCH_FIRST 或 SQL_FETCH_NEXT。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>註解  
 **SQLDrivers**驅動程式說明中的會傳回\* *DriverDescription*緩衝區。 它會傳回在驅動程式的其他資訊\* *DriverAttributes*緩衝區為關鍵字-值配對的清單。 系統資訊中的驅動程式就會傳回所有的驅動程式，除了列出的所有關鍵字**CreateDSN**，這用來建立資料來源的提示，並因此是選擇性的。 每組都終止 null 位元組，且完整的清單會終止 null 位元組 （也就是兩個 null 位元組標記清單的結尾）。 例如，檔案為基礎的驅動程式使用 C 的語法可能會傳回下列 （"\0 」 代表一個 null 字元） 的屬性清單：  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 如果\* *DriverAttributes*不是足夠容納整個清單，將遭到截斷的清單， **SQLDrivers**傳回 SQLSTATE 01004 （資料已截斷） 和清單的長度 (不包括最後一個 null 結束位元組） 會傳回 **AttributesLengthPtr*。  
  
 安裝驅動程式時，驅動程式屬性關鍵字會加入從系統資訊。 如需詳細資訊，請參閱 <<c0> [ 安裝 ODBC 元件](../../../odbc/reference/install/installing-odbc-components.md)。  
  
 應用程式可以呼叫**SQLDrivers**多次，以便擷取所有的驅動程式描述。 驅動程式管理員會將這項資訊擷取系統資訊。 有沒有更多的驅動程式描述，當**SQLDrivers**傳回 sql_no_data 為止。 如果**SQLDrivers** SQL_FETCH_NEXT 它傳回 SQL_NO_DATA 之後，它會傳回第一個驅動程式說明，請立即呼叫。 如需應用程式如何使用傳回的資訊**SQLDrivers**，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果傳遞至 SQL_FETCH_NEXT **SQLDrivers**呼叫它時，第一次**SQLDrivers**傳回第一個資料來源的名稱。  
  
 因為**SQLDrivers**實作在驅動程式管理員 中，它支援所有的驅動程式，不論特定驅動程式的標準相容性。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|探索並列出連接到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|傳回的資料來源名稱|[SQLDataSources 函式](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
