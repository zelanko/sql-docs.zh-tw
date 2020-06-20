---
title: 從 DB-LIBRARY 轉換成 ODBC 大量複製 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 29a8ee59db4cade8cc3ddf649b54d4c2c47e87ee
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021318"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>從 DB-Library 轉換成 ODBC 大量複製
  將 DB-LIBRARY 大量複製程式轉換成 ODBC 很簡單，因為 Native Client ODBC 驅動程式所支援的大量複製函數與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] db-library 大量複製函數類似，但有下列例外狀況：  
  
-   DB-Library 應用程式會將指向 DBPROCESS 結構的指標當做大量複製函數的第一個參數傳遞。 在 ODBC 應用程式中，DBPROCESS 指標會由 ODBC 連接控制代碼所取代。  
  
-   DB-LIBRARY 應用程式會在連接之前呼叫**BCP_SETL** ，以在 DBPROCESS 上啟用大量複製作業。 ODBC 應用程式會改為在連接之前呼叫[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) ，以在連接控制碼上啟用大量作業：  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式不支援 db-library 訊息和錯誤處理常式; 您必須呼叫**SQLGetDiagRec** ，以取得 ODBC 大量複製函數所引發的錯誤和訊息。 大量複製函數的 ODBC 版本會傳回標準的大量複製傳回碼 SUCCEED 或 FAILED，而非 ODBC 樣式的傳回碼，例如 SQL_SUCCESS 或 SQL_ERROR。  
  
-   針對 DB-LIBRARY [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen*參數所指定的值，與 ODBC **bcp_bind**_cbData_參數的轉譯方式不同。  
  
    |指示的條件|DB-LIBRARY *varlen*值|ODBC *cbData*值|  
    |-------------------------|--------------------------------|-------------------------|  
    |提供了 Null 值|0|-1 (SQL_NULL_DATA)|  
    |提供了變數資料|-1|-10 (SQL_VARLEN_DATA)|  
    |長度為零的字元或二進位字串|NA|0|  
  
     在 DB-LIBRARY 中， *varlen*值-1 表示正在提供可變長度的資料，而在 ODBC *cbData*中會將它解讀為表示只提供 Null 值。 將任何-1 的 DB-LIBRARY *varlen*規格變更為 SQL_VARLEN_DATA，並將任何0的*varlen*規格變更為 SQL_Null_DATA。  
  
-   DB-LIBRARY **bcp \_ colfmt**_file \_ collen_和 ODBC [bcp_colfmt](../native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*CbUserData*與上面所述的**bcp_bind**_varlen_和*cbData*參數有相同的問題。 將任何-1 的 DB-LIBRARY *file_collen*規格變更為 SQL_VARLEN_DATA，並將任何*file_collen*規格0變更為 SQL_Null_DATA。  
  
-   ODBC [bcp_control](../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)函數的*iValue*參數是 void 指標。 在 DB-LIBRARY 中， *iValue*是整數。 將 ODBC *iValue*的值轉換為 void *。  
  
-   **Bcp_control**選項 BCPMAXERRS 指定大量複製作業失敗之前，有多少個個別的資料列可以有錯誤。 BCPMAXERRS 的預設值為0（在第一次錯誤時失敗），位於 ODBC 版本的**bcp_control**和10中。 相依于預設值0來終止大量複製作業的 DB-LIBRARY 應用程式，必須變更為呼叫 ODBC **bcp_control**以將 BCPMAXERRS 設定為0。  
  
-   ODBC **bcp_control**函數支援下列不受 db-library 版本的**bcp_control**支援的選項：  
  
    -   BCPODBC  
  
         當設定為 TRUE 時，指定以字元格式儲存的**datetime**和**Smalldatetime**值會有 ODBC 時間戳記 escape 序列前置詞和後置詞。 這僅適用於 BCP_OUT 作業。  
  
         當 BCPODBC.BCP 設定為 FALSE 時，轉換為字元字串的**日期時間**值會輸出為：  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         當 BCPODBC.BCP 設定為 TRUE 時，相同的**datetime**值會輸出為：  
  
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
  
-   ODBC **bcp_colfmt**函數不支援 SQLCHAR 的*file_type*指標，因為它與 ODBC SQLCHAR typedef 衝突。 請改用 SQLCHARACTER 來進行**bcp_colfmt**。  
  
-   在 ODBC 版本的大量複製函式中，在字元字串中使用**datetime**和**Smalldatetime**值的格式為 yyyy-mm-dd hh： MM： ss 的 odbc 格式。**Smalldatetime**值使用 yyyy-mm-dd hh： mm： SS 的 ODBC 格式。  
  
     大量複製函數的 DB-LIBRARY 版本會使用數種格式，接受字元字串中的**datetime**和**Smalldatetime**值：  
  
    -   預設格式為*mmm dd yyyy hh： mmxx* ，其中*xx*為 AM 或 PM。  
  
    -   以 DB-LIBRARY **dbconvert**函數支援的任何格式的**datetime**和**Smalldatetime**字元字串。  
  
    -   在用戶端網路公用程式的 [DB-LIBRARY**選項**] 索引標籤上核取 [**使用國際設定**] 方塊時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，db-library 大量複製函數也會接受針對用戶端電腦登錄的地區設定所定義之地區日期格式的日期。  
  
     DB-LIBRARY 大量複製函數不接受 ODBC **datetime**和**Smalldatetime**格式。  
  
     如果 SQL_SOPT_SS_REGIONALIZE 陳述式屬性設定為 SQL_RE_ON，ODBC 大量複製函數會接受採用針對用戶端電腦登錄地區設定所定義之地區日期格式的日期。  
  
-   以字元格式輸出**money**值時，ODBC 大量複製函數會提供四位數的精確度，而且不會有逗號分隔符號;DB-LIBRARY 版本只提供兩位數的精確度，並包含逗號分隔符號。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行大量複製作業](performing-bulk-copy-operations-odbc.md)   
 [大量複製函數](../native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
