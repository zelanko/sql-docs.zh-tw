---
title: 從 Db-library 轉換成 ODBC 大量複製 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- converting DB-Library to ODBC bulk copy
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], DB-Library bulk copy
- ODBC, bulk copy operations
- DB-Library bulk copy
ms.assetid: 0bc15bdb-f19f-4537-ac6c-f249f42cf07f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55069754f96c36eb30d4f4af9229333405f0a982
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130891"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>從 DB-Library 轉換成 ODBC 大量複製
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  將 Db-library 大量複製程式轉換成 ODBC 很簡單，因為大量複製函數所支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會與 Db-library 大量複製函數，但有下列例外狀況：  
  
-   DB-Library 應用程式會將指向 DBPROCESS 結構的指標當做大量複製函數的第一個參數傳遞。 在 ODBC 應用程式中，DBPROCESS 指標會由 ODBC 連接控制代碼所取代。  
  
-   Db-library 應用程式會呼叫**BCP_SETL**才能連線到啟用 dbprocess 的大量複製作業。 ODBC 應用程式改為呼叫[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)才能連線到啟用連接控制代碼上的大量作業：  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不支援 Db-library 訊息和錯誤處理常式，您必須呼叫**SQLGetDiagRec**以取得錯誤和 ODBC 大量複製函數所引發的訊息。 大量複製函數的 ODBC 版本會傳回標準的大量複製傳回碼 SUCCEED 或 FAILED，而非 ODBC 樣式的傳回碼，例如 SQL_SUCCESS 或 SQL_ERROR。  
  
-   DB 程式庫所指定的值[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen*參數會被解譯方式與 ODBC **bcp_bind**_cbData_參數。  
  
    |指示的條件|Db-library *varlen*值|ODBC *cbData*值|  
    |-------------------------|--------------------------------|-------------------------|  
    |提供了 Null 值|0|-1 (SQL_NULL_DATA)|  
    |提供了變數資料|-1|-10 (SQL_VARLEN_DATA)|  
    |長度為零的字元或二進位字串|NA|0|  
  
     在 DB 程式庫*varlen* -1 值表示，要提供可變長度資料，而在 ODBC *cbData*則解譯成表示提供的是只有 NULL 值。 變更任何 Db-library *varlen* -1 為 SQL_VARLEN_DATA，以及任何的規格*varlen* 0 為 SQL_NULL_DATA 的規格。  
  
-   Db-library **bcp_colfmt**_file_collen_和 ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*cbUserData*具有相同的問題為**bcp_bind**_varlen_並*cbData*先前所述的參數。 變更任何 Db-library *file_collen* -1 為 SQL_VARLEN_DATA，以及任何的規格*file_collen* 0 為 SQL_NULL_DATA 的規格。  
  
-   *IValue*參數的 ODBC [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)函式是 void 的指標。 在 DB 程式庫*iValue*是整數。 值轉換為 ODBC *iValue*為 void *。  
  
-   **Bcp_control**選項 BCPMAXERRS 會指定大量複製作業失敗前幾個個別的資料列可能有錯誤。 BCPMAXERRS 的預設值為 0 （失敗發生在第一個錯誤） 的 Db-library 版本中**bcp_control**和 10 中的 ODBC 版本。 依賴預設值 0 來結束大量複製作業的 Db-library 應用程式必須變更為呼叫 ODBC **bcp_control**以便將 BCPMAXERRS 設定為 0。  
  
-   ODBC **bcp_control**函式支援下列選項的 Db-library 版本不支援**bcp_control**:  
  
    -   BCPODBC  
  
         當設定為 TRUE，表示**datetime**並**smalldatetime** ODBC 時間戳記逸出序列前置詞和後置詞，都以字元格式儲存的值。 這僅適用於 BCP_OUT 作業。  
  
         當 bcpodbc 設定為 FALSE 時， **datetime**轉換成字元字串的值會輸出為：  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         當 bcpodbc 設定為 TRUE 時，相同**datetime**值輸出為：  
  
        ```  
        {ts '1997-01-01 00:00:00.000' }  
        ```  
  
    -   BCPKEEPIDENTITY  
  
         當設定為 TRUE 時，這個選項會指定大量複製函數插入提供給含有識別條件約束之資料行的資料值。 如果沒有設定，就會為插入的資料列產生新的識別值。  
  
    -   BCPHINTS  
  
         指定各種大量複製最佳化。 這個選項無法在 6.5 或舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上使用。  
  
    -   BCPFILECP  
  
         指定大量複製檔案的字碼頁。  
  
    -   BCPUNICODEFILE  
  
         指定字元模式大量複製檔案為 Unicode 檔案。  
  
-   ODBC **bcp_colfmt**函式不支援*file_type*指標的 SQLCHAR 因為與 ODBC SQLCHAR typedef 衝突。 改用 SQLCHARACTER **bcp_colfmt**。  
  
-   在大量複製函數，使用格式的 ODBC 版本**datetime**並**smalldatetime**字元字串中的值是 ODBC 格式 yyyy-mm-dd 的-ss.sss**smalldatetime**值使用 ODBC 格式 yyyy-mm-dd 的-hh: mm:。  
  
     大量複製函數的 Db-library 版本接受**datetime**並**smalldatetime**使用數種格式的字元字串中的值：  
  
    -   預設的格式是*mmm dd yyyy hh: mmxx*何處*xx*是 AM 或 PM。  
  
    -   **日期時間**並**smalldatetime**字元 DB 程式庫所支援的任何格式的字串**dbconvert**函式。  
  
    -   當**使用國際設定**Db-library 上核取方塊**選項**索引標籤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端網路公用程式，Db-library 大量複製函數也接受區域中的日期針對用戶端電腦登錄地區設定所定義的日期格式。  
  
     Db-library 大量複製函數不接受 ODBC **datetime**並**smalldatetime**格式。  
  
     如果 SQL_SOPT_SS_REGIONALIZE 陳述式屬性設定為 SQL_RE_ON，ODBC 大量複製函數會接受採用針對用戶端電腦登錄地區設定所定義之地區日期格式的日期。  
  
-   當輸出流通時**金錢**字元格式、 ODBC 大量複製函數會提供四位數的精確度和沒有逗號加以區隔; 中的值Db-library 版本僅提供兩位數的有效位數，且包括逗號區隔。  
  
## <a name="see-also"></a>另請參閱  
 [執行大量複製作業&#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
