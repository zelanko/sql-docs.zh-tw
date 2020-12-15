---
description: 從 DB-Library 轉換成 ODBC 大量複製
title: 從 DB-Library 轉換為 ODBC 大量複製 |Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 488f3f1583a58431c5606fade81e9eb3f56bd076
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465029"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>從 DB-Library 轉換成 ODBC 大量複製
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  將 DB-Library 大量複製程式轉換成 ODBC 很簡單，因為 Native Client ODBC 驅動程式所支援的大量複製函數與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB-Library 大量複製函數類似，但有下列例外狀況：  
  
-   DB-Library 應用程式會將指向 DBPROCESS 結構的指標當做大量複製函數的第一個參數傳遞。 在 ODBC 應用程式中，DBPROCESS 指標會由 ODBC 連接控制代碼所取代。  
  
-   DB-Library 的應用程式會在連接之前呼叫 **BCP_SETL** ，以啟用 DBPROCESS 上的大量複製作業。 ODBC 應用程式會在連接之前呼叫 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) ，以在連接控制碼上啟用大量作業：  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式不支援 DB-Library 訊息和錯誤處理常式; 您必須呼叫 **SQLGetDiagRec** 來取得 ODBC 大量複製函數所引發的錯誤和訊息。 大量複製函數的 ODBC 版本會傳回標準的大量複製傳回碼 SUCCEED 或 FAILED，而非 ODBC 樣式的傳回碼，例如 SQL_SUCCESS 或 SQL_ERROR。  
  
-   針對 DB-Library [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen* 參數指定的值會以不同于 ODBC **bcp_bind**_cbData_ 參數的方式來解釋。  
  
    |指示的條件|DB-Library *varlen* 值|ODBC *cbData* 值|  
    |-------------------------|--------------------------------|-------------------------|  
    |提供了 Null 值|0|-1 (SQL_NULL_DATA)|  
    |提供了變數資料|-1|-10 (SQL_VARLEN_DATA)|  
    |長度為零的字元或二進位字串|NA|0|  
  
     在 DB-LIBRARY 中， *varlen* 值為-1 表示會提供變數長度資料，而在 ODBC *cbData* 中則會將它解釋為表示只提供 Null 值。 將-1 的任何 DB-Library *varlen* 規格變更為 SQL_VARLEN_DATA，並將任何 *varlen* 規格0變更為 SQL_Null_DATA。  
  
-   DB-Library **bcp_colfmt**_file_collen_ 和 ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*cbUserData* 與上面所述的 **bcp_bind**_varlen_ 和 *cbData* 參數有相同的問題。 將-1 的任何 DB-Library *file_collen* 規格變更為 SQL_VARLEN_DATA，並將任何 *file_collen* 規格0變更為 SQL_Null_DATA。  
  
-   ODBC [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)函數的 *iValue* 參數是 void 指標。 在 DB-LIBRARY 中， *iValue* 是整數。 將 ODBC *iValue* 的值轉換成 void *。  
  
-   **Bcp_control** 選項 BCPMAXERRS 指定大量複製作業失敗之前，有多少個別的資料列可能有錯誤。 BCPMAXERRS 的預設值為 0 (在 DB-Library 版本的 **bcp_control** 中第一次發生) 錯誤時失敗，以及在 ODBC 版本中為10。 DB-Library 相依于預設值0以終止大量複製作業的應用程式，必須變更為呼叫 ODBC **bcp_control** ，將 BCPMAXERRS 設定為0。  
  
-   ODBC **bcp_control** 函式支援下列 DB-Library 版本 **bcp_control** 不支援的選項：  
  
    -   BCPODBC  
  
         當設為 TRUE 時，指定以字元格式儲存的 **datetime** 和 **Smalldatetime** 值將會有 ODBC 時間戳記的逸出序列前置詞和尾碼。 這僅適用於 BCP_OUT 作業。  
  
         當 BCPODBC.BCP 設定為 FALSE 時，轉換成字元字串的 **日期時間** 值會輸出為：  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         當 BCPODBC.BCP 設定為 TRUE 時，相同的 **日期時間** 值會輸出為：  
  
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
  
-   ODBC **bcp_colfmt** 函數不支援 SQLCHAR 的 *file_type* 指標，因為它與 ODBC SQLCHAR typedef 衝突。 請改用 SQLCHARACTER 來 **bcp_colfmt**。  
  
-   在 ODBC 版本的大量複製函式中，以字元字串處理 **datetime** 和 **Smalldatetime** 值的格式是 yyyy-mm-dd hh： MM： ss 的 odbc 格式。 **Smalldatetime** 值使用格式為 yyyy-mm-dd hh： mm： SS 的 ODBC 格式。  
  
     大量複製函數的 DB-Library 版本，會使用數種格式接受字元字串中的 **datetime** 和 **Smalldatetime** 值：  
  
    -   預設格式為 *mmm dd yyyy hh： mmxx* ，其中 *xx* 是 AM 或 PM。  
  
    -   DB-Library **dbconvert** 函式所支援之任何格式的 **datetime** 和 **Smalldatetime** 字元字串。  
  
    -   當您在用戶端網路公用程式的 [DB-Library **選項**] 索引標籤上核取 [**使用國際設定**] 方塊時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，DB-Library 大量複製函式也會接受針對用戶端電腦登錄地區設定所定義之地區日期格式的日期。  
  
     DB-Library 大量複製函數不接受 ODBC **datetime** 和 **Smalldatetime** 格式。  
  
     如果 SQL_SOPT_SS_REGIONALIZE 陳述式屬性設定為 SQL_RE_ON，ODBC 大量複製函數會接受採用針對用戶端電腦登錄地區設定所定義之地區日期格式的日期。  
  
-   以字元格式輸出 **money** 值時，ODBC 大量複製函式提供四位數的有效位數，而且沒有逗號分隔符號;DB-Library 版本只會提供兩位數的精確度，並包含逗號分隔符號。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行大量複製作業 ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
