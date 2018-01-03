---
title: "SQLDrivers 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLDrivers
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDrivers
helpviewer_keywords: SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad4afa4a54b63b759b03774f77ed7ec0371ff931
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqldrivers-function"></a>SQLDrivers 函數
**一致性**  
 版本引進了： ODBC 2.0 標準相容性： ODBC  
  
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
 [輸入]決定是否驅動程式管理員會提取下一個驅動程式描述的清單 (SQL_FETCH_NEXT) 或搜尋是否會開始從清單 (SQL_FETCH_FIRST) 開頭。  
  
 *DriverDescription*  
 [輸出]這是要傳回的驅動程式描述的緩衝區指標。  
  
 如果*DriverDescription*是 NULL， *DescriptionLengthPtr*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回中緩衝區所指*DriverDescription*。  
  
 *BufferLength1*  
 [輸入]長度 **DriverDescription*緩衝區，以字元為單位。  
  
 *DescriptionLengthPtr*  
 [輸出]這是要傳回的總字元數 （不包括 null 結束字元） 中的緩衝區指標可用來傳回中\* *DriverDescription*。 可傳回的字元數目是否大於或等於*BufferLength1*中的驅動程式描述\* *DriverDescription*會被截斷成*BufferLength1*減去 null 結束字元的長度。  
  
 *DriverAttributes*  
 [輸出]這是要傳回的驅動程式 （請參閱 「 註解 」） 的屬性值組清單中的緩衝區指標。  
  
 如果*DriverAttributes*是 NULL， *AttributesLengthPtr*仍會傳回的總位元組數 （不含字元資料 null 結束字元） 可用來傳回緩衝區中所指*DriverAttributes*。  
  
 *BufferLength2*  
 [輸入]長度\* *DriverAttributes*緩衝區，以字元為單位。 如果 *\*DriverDescription*值為 Unicode 字串 (當呼叫**SQLDriversW**)、 *Columnsize*引數必須是偶數。  
  
 *AttributesLengthPtr*  
 [輸出]這是要傳回的總位元組數 （不含 null 結束位元組） 的緩衝區指標可用來傳回中\* *DriverAttributes*。 如果傳回可用的位元組數目大於或等於*BufferLength2*，清單中的屬性值組的\* *DriverAttributes*會被截斷成*BufferLength2*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDrivers**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以藉由呼叫取得相關聯的 SQLSTATE 值**SQLGetDiagRec**與*HandleType*的SQL_HANDLE_ENV 並*處理*的*EnvironmentHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDrivers** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|(DM) 驅動程式管理員特有的資訊訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|(DM) 緩衝區\* *DriverDescription*仍不夠大，無法傳回完整的驅動程式描述。 因此，描述已截斷。 在傳回完成的驅動程式描述的長度\* *DescriptionLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> (DM) 緩衝區\* *DriverAttributes*仍不夠大，無法傳回屬性值組的完整清單。 因此，已截斷參數清單。 中會傳回屬性值組的未截斷的清單長度 **AttributesLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|(DM) 驅動程式管理員無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*BufferLength1*小於 0。<br /><br /> (DM) 引數指定的值*BufferLength2*小於 0 或等於 1。|  
|HY103|無效的擷取程式碼|(DM) 指定的引數的值*方向*不等於 SQL_FETCH_FIRST 或 SQL_FETCH_NEXT。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
  
## <a name="comments"></a>註解  
 **SQLDrivers**傳回中的驅動程式描述\* *DriverDescription*緩衝區。 它會傳回的驅動程式的其他資訊\* *DriverAttributes*緩衝區做為關鍵字-值配對的清單。 系統資訊中的驅動程式就會傳回所有驅動程式，除了列出的所有關鍵字**CreateDSN**，其用於提示輸入的資料來源建立，因此是選擇性的。 每一組已終止 null 位元組，且以 null 位元組終止的完整清單 （也就是兩個 null 位元組標記清單的結尾）。 例如，使用 C 語法以檔案為基礎驅動程式可能會傳回以下清單中的屬性 （"\0 」 代表一個 null 字元）：  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 如果\* *DriverAttributes*不是足夠容納整個清單，清單遭到截斷， **SQLDrivers**傳回 SQLSTATE 01004 （資料已截斷） 和清單的長度 (不包括中的最後一個 null 結束位元組） 會傳回 **AttributesLengthPtr*。  
  
 安裝驅動程式時，驅動程式屬性的關鍵字會加入從系統資訊。 如需詳細資訊，請參閱[安裝 ODBC 元件](../../../odbc/reference/install/installing-odbc-components.md)。  
  
 應用程式可以呼叫**SQLDrivers**多次，以便擷取所有的驅動程式描述。 驅動程式管理員會將此資訊擷取系統資訊。 當沒有多個驅動程式描述、 **SQLDrivers**傳回 sql_no_data 為止。 如果**SQLDrivers** SQL_FETCH_NEXT 它傳回 SQL_NO_DATA 之後，它會傳回第一個驅動程式的說明，請立即呼叫。 如需有關應用程式如何使用所傳回的資訊資訊**SQLDrivers**，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果傳遞至 SQL_FETCH_NEXT **SQLDrivers**第一次呼叫， **SQLDrivers**傳回第一個資料來源名稱。  
  
 因為**SQLDrivers**實作驅動程式管理員 中會支援它所有的驅動程式，不論特定驅動程式標準相容性。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|探索及列出連接到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|傳回的資料來源名稱|[SQLDataSources 函式](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
