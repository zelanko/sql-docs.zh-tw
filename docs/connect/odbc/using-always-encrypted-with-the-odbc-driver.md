---
title: "搭配使用一律加密 with the ODBC Driver for SQL Server |Microsoft 文件"
ms.custom: 
ms.date: 10/01/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
caps.latest.revision: "3"
ms.author: v-chojas
manager: jhubbard
author: MightyPen
ms.workload: On Demand
ms.openlocfilehash: a7e2679b04f55f528de1d90070593f6197160d79
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2018
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>搭配使用一律加密 with the ODBC Driver for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>適用於

- ODBC Driver 13.1 for SQL Server
- ODBC Driver for SQL Server 17

### <a name="introduction"></a>簡介

本文提供有關如何開發使用 ODBC 應用程式資訊[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和[ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。

[永遠加密] 可讓用戶端應用程式加密敏感性資料，且永遠不會顯示資料或 SQL Server 或 Azure SQL Database 的加密金鑰。 啟用 永遠加密驅動程式，例如 ODBC Driver for SQL Server，進而達成此目的透過無障礙地加密與解密用戶端應用程式中的機密資料。 驅動程式會自動判斷哪一個查詢參數對應至敏感性資料庫資料行 (使用 [永遠加密] 保護)，然後加密這些參數值後再將資料傳遞至 SQL Server 或 Azure SQL Database。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 如需詳細資訊，請參閱 [一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。

### <a name="prerequisites"></a>필수 구성 요소

在資料庫中設定永遠加密。 這牽涉到佈建永遠加密金鑰，以及設定加密所選資料庫資料行。 如果您的資料庫尚未設定 [永遠加密]，請遵循 [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(永遠加密快速入門) 中的指示操作。 特別是，您的資料庫應該包含資料行主要金鑰 (CMK)、 資料行加密金鑰 (CEK) 和資料表包含一個或多個使用該 CEK 加密的資料行的中繼資料定義。

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>ODBC 應用程式中啟用永遠加密

若要啟用參數加密和加密的結果集資料行解密最簡單方式是藉由設定的值`ColumnEncryption`連接字串關鍵字設**啟用**。 以下是啟用一律加密的連接字串的範例：

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

永遠加密可能也會啟用在 DSN 組態中，使用相同的索引鍵和值 （這將會覆寫設定連接字串，如果有的話），或以程式設計方式使用`SQL_COPT_SS_COLUMN_ENCRYPTION`預先連接屬性。 將它設定為這種方式，將會覆寫連接字串或 DSN 中設定的值：

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

一旦啟用連線，可調整的永遠加密行為，對個別查詢。 請參閱[控制效能影響的永遠加密](#controlling-the-performance-impact-of-always-encrypted)下方如需詳細資訊。

請注意，啟用 永遠加密不足，無法加密或解密才能成功;您也需要確定：

- 應用程式要有 [檢視任何資料行的主要金鑰定義] 和 [檢視任何資料行的加密金鑰定義] 資料庫權限，才能存取資料庫中永遠加密金鑰的相關中繼資料。 如需詳細資訊，請參閱[資料庫權限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。

- 應用程式可以存取它會保護查詢加密資料行的 Cek CMK。 這是依據儲存 CMK 的金鑰存放區提供者。 請參閱[使用資料行主要金鑰存放區](#working-with-column-master-key-stores)如需詳細資訊。

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料

一旦您啟用 永遠加密的連接上，您可以使用標準 ODBC Api (請參閱[ODBC 範例程式碼](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953)或[ODBC 程式設計人員參考](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx)) 來擷取或修改加密的資料庫資料行中的資料。 假設您的應用程式所需資料庫權限可以存取資料行主要金鑰，驅動程式會加密目標加密資料行，並解密來自加密資料行，其運作方式以透明的方式來擷取資料的任何查詢參數應用程式，如同未加密的資料行。

如果未啟用永遠加密，使用目標加密資料行的參數的查詢將會失敗。 資料仍擷取從加密的資料行，只要查詢沒有任何以加密的資料行為目標的參數。 不過，驅動程式將不會嘗試任何解密，而且應用程式將會收到二進位的加密的資料 （以位元組陣列）。

下表摘要說明查詢，根據是否啟用 永遠加密與否的行為：

|查詢特性 | [永遠加密] 已啟用，且應用程式可以存取金鑰和金鑰中繼資料|[永遠加密] 已啟用，但應用程式不能存取金鑰或金鑰中繼資料 | [永遠加密] 已停用|
|:---|:---|:---|:---|
| 加密的資料行為目標的參數。 | 以清晰簡明的方式加密參數值。 | 錯誤 | 錯誤|
| 從加密的資料行擷取資料，不含加密的資料行為目標的參數。| 以清晰簡明的方式解密來自加密資料行的結果。 應用程式收到純文字資料行值。 | 錯誤 | 不解密來自加密資料行的結果。 應用程式接收加密的值做為位元組陣列。

以下範例將說明擷取和修改加密資料行中的資料。 這些範例假設具有下列結構描述的資料表。 請注意，SSN 和 BirthDate 資料行均已加密。

```
CREATE TABLE [dbo].[Patients](
 [PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] )
 GO
```

#### <a name="data-insertion-example"></a>資料插入範例

本例會將資料列插入病患資料表。 請注意下列事項：

- 範例程式碼中沒有任何需要加密的特定項目。 驅動程式會自動偵測並加密的 SSN 和日期參數，目標加密資料行的值。 這讓加密對應用程式變得透明化。

- 插入至資料庫資料行，包括加密的資料行的值會當做繫結參數傳遞 (請參閱[SQLBindParameter 函數](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx))。 雖然使用參數是選擇性的值傳送至非加密的資料行 （不過強烈建議因有利於防止 SQL 資料隱碼） 時，就需要加密的資料行為目標的值。 如果插入 SSN 或 BirthDate 資料行中的值傳遞做為內嵌在查詢陳述式中的常值，則查詢會失敗，因為驅動程式不會嘗試加密或處理查詢中的常值。 結果，伺服器會因與加密資料行不相容而拒絕它們。

- 插入 SSN 資料行參數的 SQL 型別設定為對應至如 SQL_CHAR **char** SQL Server 資料類型 (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`)。 如果參數的型別設定為 SQL_WCHAR，對應至**nchar**，則查詢會失敗，因為永遠加密 不支援加密的 nchar 值的伺服器端轉換成加密的 char 值。 請參閱[ODBC 程式設計人員參考--附錄 d： 資料型別](https://msdn.microsoft.com/library/ms713607.aspx)有關的資料類型對應。

```
    SQL_DATE_STRUCT date;
    SQLLEN cbdate;   // size of date structure  

    SQLCHAR SSN[12];
    strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

    SQLWCHAR* firstName = L"Catherine";
    SQLWCHAR* lastName = L"Abel";
    SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

    // Initialize the date structure  
    date.day = 10;
    date.month = 9;
    date.year = 1996;

    // Size of structures   
    cbdate = sizeof(SQL_DATE_STRUCT);

    SQLRETURN rc = 0;

    string queryText = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?) ";

    rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

    //SSN
    rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);
    //FirstName
    rc = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)firstName, 0, &cbFirstName);
    //LastName
    rc = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);
    //BirthDate
    rc = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 10, 0, (SQLPOINTER)&date, 0, &cbdate);

    rc = SQLExecute(hstmt);
```

#### <a name="plaintext-data-retrieval-example"></a>純文字資料擷取範例

下例示範根據加密值篩選資料，以及從加密資料行擷取純文字資料。 請注意下列事項：

- 要傳遞使用 SQLBindParameter 等，讓驅動程式可以以透明的方式加密它傳送到伺服器之前，先用在 WHERE 子句來篩選 SSN 資料行需要的值。

- 列印程式的所有值都是純文字，因為驅動程式會以透明的方式解密從 SSN 和 BirthDate 資料行擷取的資料。

> [!NOTE]
> 查詢可以加密的資料行上執行相等比較，只有具決定性加密。 如需詳細資訊，請參閱[選取具確定性或隨機化加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[SSN] = ? ";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//SSN
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="ciphertext-data-retrieval-example"></a>加密文字資料擷取範例

如未啟用 [永遠加密]，只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。

下列範例說明從加密資料行擷取二進位的加密的資料。 請注意下列事項：

- 因為連接字串未啟用 [永遠加密]，所以查詢會以位元組陣列 (程式會將值轉換為字串) 傳回加密的 SSN 和 BirthDate 值。
- 從加密資料行擷取資料但停用 [永遠加密] 的查詢可以有參數，只要沒有任何參數以加密資料行為目標。 上述依 LastName 篩選的查詢，在資料庫中未加密。 如果依 SSN 或 BirthDate 篩選查詢，查詢會失敗。


```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[LastName] = ?";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//LastName
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>避免常見的加密資料行查詢問題

本章節描述常見的錯誤類別，當查詢從 ODBC 應用程式和如何加以避免的一些指導方針的加密資料行。

##### <a name="unsupported-data-type-conversion-errors"></a>不支援的資料類型轉換錯誤

[永遠加密] 支援極少數的加密資料類型轉換。 請參閱[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)支援的類型轉換詳細清單。 若要避免資料類型轉換錯誤，請確定使用 SQLBindParameter 具有加密的資料行為目標的參數時，觀察下列各點：

- 參數的 SQL 型別也可以完全相同的目標資料行中，類型或支援從 SQL 類型轉換成資料行的類型。

- 有效位數和小數位數參數的資料行為目標`decimal`和`numeric`SQL Server 資料類型為相同的有效位數和小數位數設定為目標資料行。

- 參數為目標的資料行的有效位數`datetime2`， `datetimeoffset`，或`time`SQL Server 資料類型不是大於目標資料行，修改目標資料行的查詢中的有效位數。  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳送純文字，而不是傳送加密值所造成的錯誤。

任何目標加密資料行的值必須加密再傳送至伺服器。 嘗試插入、 修改或純文字值，對加密資料行的篩選條件會導致錯誤。 若要避免這類錯誤，請確認：

- 永遠加密 已啟用 (在 DSN 中，連接字串中，之前連接設定`SQL_COPT_SS_COLUMN_ENCRYPTION`是否有特定的連接，連接屬性或`SQL_SOPT_SS_COLUMN_ENCRYPTION`的特定陳述式的陳述式屬性)。

- 您可以使用 SQLBindParameter 來傳送加密的資料行為目標的資料。 下列範例會顯示錯誤篩選常值/常數對加密資料行 (SSN)，而非將常值做為引數傳遞至 SQLBindParameter 的查詢。

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>當使用 SQLSetPos 和 SQLMoreResults 的預防措施

#### <a name="sqlsetpos"></a>SQLSetPos

`SQLSetPos` API 可讓應用程式來更新結果集將使用的緩衝區，已與 SQLBindCol 繫結和先前提取到哪一個資料列資料中的資料列。 由於加密固定長度類型的非對稱式填補行為，它有可能會意外變更這些資料行的資料的資料列中的其他資料行上執行更新時。 AE，如果值小於緩衝區大小，將會以填補固定的長度字元值。

若要減輕這種行為，使用`SQL_COLUMN_IGNORE`旗標來忽略資料行，將不會更新為一部分`SQLBulkOperations`以及何時使用`SQLSetPos`以資料指標為基礎的更新。  不會被直接修改應用程式的所有資料行應該會略過，這兩個效能並避免發生截斷的資料行繫結至緩衝區*小*比其實際 (DB) 的大小。 如需詳細資訊，請參閱[SQLSetPos 函數參考](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx)。

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

應用程式可能會呼叫[SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx)備妥的陳述式中傳回有關資料行的中繼資料。  啟用永遠加密時，呼叫`SQLMoreResults`*之前*呼叫`SQLDescribeCol`導致[sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) ，會呼叫未正確地傳回純文字加密的資料行的中繼資料。 若要避免這個問題，請呼叫`SQLDescribeCol`備妥的陳述式*之前*呼叫`SQLMoreResults`。

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>控制永遠加密的效能影響

因為永遠加密 」 是用戶端加密技術，大部分的效能負擔是在用戶端，不是在資料庫觀察到。 除了加密和解密作業成本，效能負擔的用戶端的其他來源如下：

- 額外反覆存取資料庫以擷取查詢參數的中繼資料。

- 呼叫資料行主要金鑰存放區以存取資料行主要金鑰。

本節描述 ODBC 驅動程式中的內建效能最佳化，適用於 SQL Server 和如何控制上述兩個因素對效能的影響。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制反覆存取以擷取中繼資料的查詢參數

如果連線已啟用永遠加密，驅動程式會根據預設，呼叫[sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)每個參數化查詢，將查詢陳述式 （不含任何參數值） 傳遞至 SQL Server。 這個預存程序會分析查詢陳述式，以找出，如果任何參數需要加密，而且如果是，傳回每個參數，以允許驅動程式才能將其加密的加密相關資訊。 上述行為可確保高透明度，用戶端應用程式： 應用程式 （及應用程式開發人員） 不需要留意哪些查詢存取加密資料行，只要以加密的資料行為目標的值會傳遞至參數中的驅動程式。

### <a name="per-statement-always-encrypted-behavior"></a>每個陳述式永遠加密行為

若要控制擷取參數化查詢的加密中繼資料的效能影響，您可以變更個別查詢的永遠加密行為，如果它已在連接上啟用。 如此一來，您可以確保`sys.sp_describe_parameter_encryption`只會針對查詢，您知道有以加密的資料行為目標的參數叫用。 不過請注意，如此一來，您降低加密的透明度： 如果您在資料庫中加密的其他資料行，您可能需要變更您的應用程式，以配合結構描述變更的程式碼。

若要控制永遠加密行為的陳述式，呼叫 設定 SQLSetStmtAttr`SQL_SOPT_SS_COLUMN_ENCRYPTION`陳述式屬性，以下列值之一：

|Value|Description|
|-|-|
|`SQL_CE_DISABLED` (0)|永遠加密已停用陳述式|
|`SQL_CE_RESULTSETONLY` (1)|只有解密。 結果集和傳回值都會解密，並不會加密參數|
|`SQL_CE_ENABLED` (3) | 永遠加密已啟用，並且參數和結果|

使用 永遠加密的連線建立新的陳述式控制代碼啟用到 SQL_CE_ENABLED 的預設值。 從與它連線建立停用預設為 SQL_CE_DISABLED （和不能夠在其上啟用 永遠加密。）

如果大多數的查詢，用戶端應用程式存取加密資料行，則建議下列：

- 設定`ColumnEncryption`連接字串關鍵字設`Enabled`。

- 設定`SQL_SOPT_SS_COLUMN_ENCRYPTION`屬性`SQL_CE_DISABLED`陳述式不會存取任何加密資料行上。 這會停用這兩個呼叫`sys.sp_describe_parameter_encryption`以及嘗試解密結果中的任何值設定。
    
- 設定`SQL_SOPT_SS_COLUMN_ENCRYPTION`屬性`SQL_CE_RESULTSETONLY`上並沒有任何參數要求加密，但會從加密資料行擷取資料的陳述式。 這會停用呼叫`sys.sp_describe_parameter_encryption`和參數加密。 包含加密資料行的結果會持續進行解密。

## <a name="always-encrypted-security-settings"></a>永遠加密的安全性設定

### <a name="force-column-encryption"></a>強制資料行加密

若要強制將參數加密，設定`SQL_CA_SS_FORCE_ENCRYPT`實作參數描述項 (IPD) 欄位透過 SQLSetDescField 函式呼叫。 為非零的值會使驅動程式相關聯的參數傳回加密的中繼資料時傳回錯誤。

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

如果 SQL Server 通知驅動程式的參數不需要加密，使用該參數的查詢將會失敗。 這會提供額外的防護措施安全性攻擊，事關受危害的 SQL Server 提供不正確的加密中繼資料給用戶端，可能會導致資料洩漏。

### <a name="column-encryption-key-caching"></a>快取的資料行加密金鑰

若要減少資料行主要金鑰存放區來解密資料行加密金鑰的呼叫次數，驅動程式會快取在記憶體中的純文字 Cek。 從接收之後 ECEK 資料庫中繼資料，驅動程式會先嘗試尋找純文字 CEK 值對應的加密金鑰快取中。 驅動程式會呼叫金鑰存放區包含 CMK，只有當快取中找不到對應的純文字 CEK。

> [!NOTE]
> ODBC Driver for SQL Server 中，在兩個小時逾時後收回快取中的項目。 這表示給定 ECEK，為驅動程式會連絡一次金鑰存放區的應用程式或每隔兩小時的存留期間，少者為準。

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區

若要加密或解密資料，驅動程式必須取得 CEK 目標資料行的設定。 Cek 會儲存在資料庫中繼資料中的加密形式 (ECEKs)。 每個 CEK 都有對應的 CMK 用來加密它。 [資料庫中繼資料](../../t-sql/statements/create-column-master-key-transact-sql.md)不會儲存 CMK 本身; 它只包含金鑰存放區和金鑰存放區可以用來找出 CMK 資訊的名稱。

若要取得的 ECEK 純文字值，驅動程式會先取得有關其對應的 CMK 和 CEK 的中繼資料，然後使用此資訊來連絡包含 CMK 的金鑰存放區，並要求它解密 ECEK。 驅動程式會與金鑰存放區使用的金鑰存放區提供者通訊。

### <a name="built-in-keystore-providers"></a>內建金鑰存放區提供者

ODBC Driver for SQL Server 都附有下列內建金鑰存放區提供者：

| 名稱 | Description | 提供者 （中繼資料） 名稱 |可用性|
|:---|:---|:---|:---|
|Azure 金鑰保存庫 |在 Azure 金鑰保存庫中儲存 Cmk | `AZURE_KEY_VAULT` |Windows、 Linux macOS|
|Windows 憑證存放區|本機儲存在 Windows 的金鑰存放區的 Cmk| `MSSQL_CERTIFICATE_STORE`|視窗|

- 您 （或您的 DBA） 需要確定提供者名稱，在資料行主要金鑰中繼資料中，設定正確，而且資料行主要金鑰路徑符合指定的提供者的金鑰路徑格式。 建議您使用 SQL Server Management Studio 等工具設定金鑰，這樣在發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) 陳述式時，會自動產生有效的提供者名稱和金鑰路徑。

- 您必須確定您的應用程式可以存取該金鑰在金鑰存放區。 這可能會授與您的應用程式存取金鑰和/或金鑰存放區根據金鑰存放區，或執行其他的金鑰存放區特有的組態步驟。 例如，若要存取 Azure 金鑰保存庫，您需要提供正確的憑證金鑰存放區。

### <a name="using-the-azure-key-vault-provider"></a>使用 Azure 金鑰保存庫提供者

Azure 金鑰保存庫是存放和管理永遠加密資料行主要金鑰的方便選項 (尤其是當應用程式裝載在 Azure 時)。 ODBC Driver for SQL Server on Linux、 macOS 和 Windows 包含內建的資料行主要金鑰存放區提供者為 Azure 金鑰保存庫。 請參閱[Azure 金鑰保存庫-Step by Step](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)，[開始使用金鑰保存庫](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)，和[Azure 金鑰保存庫中建立資料行主要金鑰](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2)如需有關設定 Azure 金鑰保存庫的永遠加密功能。

此驅動程式支援 Azure 金鑰保存庫使用下列認證類型驗證：

- 使用者名稱/密碼 – 使用此方法，認證就是 Azure Active Directory 使用者和其密碼的名稱。

- 用戶端識別碼/密碼 – 使用此方法，認證就是應用程式用戶端識別碼和應用程式密碼。

若要允許使用儲存在保存資料行加密的 Cmk 驅動程式，請使用下列的只有連接字串關鍵字：

|認證類型| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|Username/password| `KeyVaultPassword`|使用者主體名稱|密碼|
|用戶端識別碼/密碼| `KeyVaultClientSecret`|用戶端識別碼|密碼|

#### <a name="example-connection-strings"></a>範例連接字串

下列連接字串會顯示如何向 Azure 金鑰保存庫，有兩種認證類型：

**ClientID/密碼**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**Username/Password**

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

任何其他的 ODBC 應用程式變更不才能使用 AKV CMK 存放裝置。

### <a name="using-the-windows-certificate-store-provider"></a>使用 Windows 憑證存放區提供者

ODBC Driver for SQL Server on Windows 包含內建的資料行主要金鑰存放區提供者的 Windows 憑證存放區，名為`MSSQL_CERTIFICATE_STORE`。 （此提供者並不適用於 macOS 或 Linux）。與此提供者，CMK 儲存在本機用戶端電腦上，且不需要額外的組態，應用程式所使用的驅動程式所需。 不過，應用程式必須存取憑證和私密金鑰存放區中。 請參閱[建立及儲存資料行主要金鑰 （永遠加密）](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted)如需詳細資訊。

### <a name="using-custom-keystore-providers"></a>使用自訂金鑰存放區提供者

ODBC Driver for SQL Server 也支援自訂的協力廠商金鑰存放區提供者使用 CEKeystoreProvider 介面。 這可讓應用程式載入時，查詢中，並設定金鑰存放區提供者，以便供驅動程式來存取加密資料行。 應用程式可能也會直接互動都會加密 SQL Server 中的儲存體和執行工作存取加密資料行使用 ODBC; 的金鑰存放區提供者如需詳細資訊，請參閱[自訂金鑰存放區提供者](../../connect/odbc/custom-keystore-providers.md)。

兩個連接屬性用來與自訂金鑰存放區提供者互動。 其中包括：

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

前者用來載入及列舉載入金鑰存放區提供者，而後者可讓應用程式提供者通訊。 之前或之後建立連線，因為應用程式提供者互動並不會與 SQL Server 通訊，可能在任何時候，使用這些連接屬性。 不過，因為尚未載入驅動程式，設定和連接之前取得這些屬性會使其可處理由驅動程式管理員，而且可能不會產生預期的結果。

#### <a name="loading-a-keystore-provider"></a>載入金鑰存放區提供者

設定`SQL_COPT_SS_CEKEYSTOREPROVIDER`連接屬性可讓用戶端應用程式載入提供者程式庫，因此可以使用包含的金鑰存放區提供者。

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| 引數 | Description |
|:---|:---|
|`ConnectionHandle`|[輸入]連接控制代碼。 必須是有效的連接控制代碼，但透過一個連接控制代碼載入提供者會從相同的程序中的任何其他可存取。|
|`Attribute`|[輸入]若要設定的屬性：`SQL_COPT_SS_CEKEYSTOREPROVIDER`常數。|
|`ValuePtr`|[輸入]指定的提供者程式庫檔名的 null 結尾字元字串指標。 SQLSetConnectAttrA，這是 ANSI （多位元組） 字串。 對於 SQLSetConnectAttrW，這是 Unicode (wchar_t) 字串。|
|`StringLength`|[輸入]SQL_NTS ValuePtr 字串的長度。|

驅動程式嘗試載入使用平台定義動態程式庫載入機制 ValuePtr 參數所識別的程式庫 (`dlopen()` Linux 及 macOS `LoadLibrary()` Windows 上)，並加入至清單中定義的任何提供者已知的驅動程式提供者。 可能會發生下列錯誤：

| 錯誤 | Description |
|:--|:--|
|`CE203`|無法載入動態程式庫。|
|`CE203`|文件庫中找不到"CEKeyStoreProvider"匯出符號。|
|`CE203`|已載入文件庫中的一個或多個提供者。|

`SQLSetConnectAttr`傳回一般錯誤或成功的值和其他資訊可透過標準的 ODBC 診斷機制發生的任何錯誤。

> [!NOTE]
> 應用程式設計者必須確保透過任何連接傳送要求的任何查詢之前，會載入任何自訂提供者。 這樣會產生錯誤：

| 錯誤 | Description |
|:--|:--|
|`CE200`|金鑰存放區提供者 %1 找不到。 請確定已載入適當的金鑰存放區提供者程式庫。|

> [!NOTE]
> 金鑰存放區提供者實作項應該避免使用`MSSQL`其自訂提供者的名稱。 這個詞彙是專用的 Microsoft 保留，並與未來的內建提供者可能會造成衝突。 使用這個詞彙自訂提供者的名稱，可能會導致 ODBC 警告。

#### <a name="getting-the-list-of-loaded-providers"></a>取得已載入提供者的清單

取得此連接屬性可讓用戶端應用程式，以判斷目前載入的驅動程式 （包括內建的。） 中的金鑰存放區提供者這個屬性只能連接之後執行。

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| 引數 | Description |
|:---|:---|
|`ConnectionHandle`|[輸入]連接控制代碼。 必須是有效的連接控制代碼，但透過一個連接控制代碼載入提供者會從相同的程序中的任何其他可存取。|
|`Attribute`|[輸入]要擷取屬性：`SQL_COPT_SS_CEKEYSTOREPROVIDER`常數。|
|`ValuePtr`|[輸出]這是要傳回的下一個載入提供者名稱中的記憶體指標。|
|`BufferLength`|[輸入]ValuePtr 緩衝區的長度。|
|`StringLengthPtr`|[輸出]這是要傳回的總位元組數 （不包括 null 結束字元） 的緩衝區的指標可用來傳回中\*ValuePtr。 如果 ValuePtr 為 null 指標，則會不傳回任何長度。 如果屬性值是字元字串，而且可用來傳回的位元組數目大於 null 終止的長度減 Columnsize 字元，在資料\*ValuePtr 就會截斷為 Columnsize 減的長度null 結束字元而且是以 null 結束的驅動程式。|

若要讓擷取整份清單，每個 Get 作業會傳回目前的提供者名稱，並累加到下一個內部計數器。 一旦到達清單中，空字串的結尾，此計數器 ("") 會傳回和計數器會重設。後續 Get 作業然後從清單開頭再繼續。

### <a name="communicating-with-keystore-providers"></a>金鑰存放區提供者與通訊

`SQL_COPT_SS_CEKEYSTOREDATA`連接屬性可讓用戶端應用程式載入的金鑰存放區提供者與通訊設定其他參數，設定金鑰材料等等。用戶端應用程式和提供者之間的通訊遵循 Get 為基礎的簡單要求-回應通訊協定，並使用此連接屬性要求。 集。 只將用戶端應用程式起始的通訊。

> [!NOTE]
> 由於的 ODBC 呼叫 ODBC 介面僅支援設定資料的連接內容的解析度 (SQLGet/SetConnectAttr) CEKeyStoreProvider 的回應。

應用程式會透過驅動程式透過 CEKeystoreData 結構的金鑰存放區提供者與通訊：

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```
| 引數 | Description |
|:---|:---|
|`name`|[輸入]集合，提供者的名稱時要傳送資料。 在 Get 時被忽略。 以 null 結束的寬字元字串。|
|`dataSize`|[輸入]下列結構的資料陣列的大小。|
|`data`|[InOut]在集合中，傳送給提供者的資料。 這可能是任意的資料。驅動程式不會嘗試解譯它。 在 Get 時要接收資料的緩衝區讀取從提供者。|

#### <a name="writing-data-to-a-provider"></a>將資料寫入至提供者

A`SQLSetConnectAttr`使用呼叫`SQL_COPT_SS_CEKEYSTOREDATA`屬性寫入至指定的金鑰存放區提供者 」 資料封包 」。
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| 引數 | Description |
|:---|:---|
|`ConnectionHandle`| [輸入]連接控制代碼。 必須是有效的連接控制代碼，但透過一個連接控制代碼載入提供者會從相同的程序中的任何其他可存取。|
|`Attribute`|[輸入]若要設定的屬性：`SQL_COPT_SS_CEKEYSTOREDATA`常數。|
|`ValuePtr`|[輸入]CEKeystoreData 結構指標。 結構的 [名稱] 欄位會識別資料適用的提供者。|
|`StringLength`|[輸入]SQL_IS_POINTER 常數|

可以透過取得其他詳細的錯誤資訊[SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)。

> [!NOTE]
> 如果因此想要提供者可以關聯至特定的連接，寫入的資料使用連接控制代碼。 這可用於實作每個連線設定。 它可能略過的連接內容，並處理資料，不論用來傳送資料的連接即會相同。 請參閱[內容關聯](../../connect/odbc/custom-keystore-providers.md#context-association)如需詳細資訊。

#### <a name="reading-data-from-a-provider"></a>從提供者讀取資料

呼叫`SQLGetConnectAttr`使用`SQL_COPT_SS_CEKEYSTOREDATA`屬性讀取""的資料封包從*上次寫入-對*提供者。 如果為 none，則會發生函數順序錯誤。 金鑰存放區提供者實作器都支援 「 假寫入 「 0 個位元組，如果要這樣做，而不會造成其他的副作用，選取讀取作業的提供者的方式。

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| 引數 | Description |
|:---|:---|
|`ConnectionHandle`|[輸入]連接控制代碼。 必須是有效的連接控制代碼，但透過一個連接控制代碼載入提供者會從相同的程序中的任何其他可存取。|
|`Attribute`|[輸入]要擷取屬性：`SQL_COPT_SS_CEKEYSTOREDATA`常數。|
|`ValuePtr`|[輸出]用來放置資料提供者讀取 CEKeystoreData 結構的指標。|
|`BufferLength`|[輸入]SQL_IS_POINTER 常數|
|`StringLengthPtr`|[輸出]這是要傳回 Columnsize 的緩衝區指標。 如果 * ValuePtr 為 null 指標，則傳回任何長度。|

呼叫端必須確保下列 CEKEYSTOREDATA 結構的長度足夠的緩衝區會配置在寫入提供者。 傳回時，其 dataSize 欄位會更新提供者讀取資料的實際長度。 可以透過取得其他詳細的錯誤資訊[SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)。

這個介面會將不需要額外放在應用程式的金鑰存放區提供者之間傳輸的資料格式。 每個提供者可以定義自己的通訊協定/資料格式，視其需求而定。

如需實作您自己的金鑰存放區提供者的範例，請參閱[自訂金鑰存放區提供者](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>使用永遠加密時的 ODBC 驅動程式的限制

### <a name="asynchronous-operations"></a>非同步作業
當 ODBC 驅動程式將會允許使用[非同步作業](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md)透過永遠加密，效能造成影響的作業時沒有啟用 永遠加密。 若要呼叫`sys.sp_describe_parameter_encryption`為決定加密中繼資料會封鎖陳述式，並會導致驅動程式等候伺服器傳回中繼資料，再傳回`SQL_STILL_EXECUTING`。

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>在使用 SQLGetData 組件中擷取資料
SQL server ODBC 驅動程式 17 加密之前使用 SQLGetData 組件中無法擷取字元和二進位資料行。 可以進行只有一個呼叫 SQLGetData，以包含整個資料行的資料長度足夠的緩衝區。

### <a name="send-data-in-parts-with-sqlputdata"></a>將資料傳送 SQLPutData 使用組件中
插入或比較資料無法傳送 SQLPutData 使用組件中。 可以進行 SQLPutData 只有一個呼叫，以包含整個資料緩衝區。 Long 資料插入加密的資料行中，使用下一節中所述，與輸入的資料檔大量複製 API。

### <a name="encrypted-money-and-smallmoney"></a>加密的 money 和 smallmoney
加密**money**或**smallmoney**資料行不能為目標的參數，因為沒有任何特定 ODBC 資料類型並對應至這些型別，造成運算元類型衝突錯誤。

## <a name="bulk-copy-of-encrypted-columns"></a>大量複製加密的資料行

使用[SQL 大量複製函數](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)和**bcp**公用程式使用 永遠加密後 ODBC 驅動程式 17 for SQL Server 支援。 純文字 （插入上加密和解密上擷取） 和加密文字 （逐字傳輸） 可插入和擷取使用大量複製 （bcp_ *） 應用程式開發介面和**bcp**公用程式。

- 要擷取密碼文字形式 （例如，用於大量載入不同的資料庫） varbinary （max）、 連接，而不`ColumnEncryption`選項 (或將它設定為`Disabled`) 和執行 BCP OUT 作業。

- 插入和擷取純文字，並讓此驅動程式會明確地執行加密和解密為必要項目，設定`ColumnEncryption`至`Enabled`已足夠。 BCP API 的功能則未變更。

- 若要在 varbinary （max） 的形式 （例如上方處擷取） 插入加密文字，請設定`BCPMODIFYENCRYPTED`選項設定為 TRUE，並執行 BCP IN 作業。 為了讓未產生資料，請確認目的地資料行的 CEK 是原先取得從中加密文字相同。

當使用**bcp**公用程式： 控制`ColumnEncryption`設定，請使用-D 選項，並指定包含所需的值的 DSN。 若要插入的加密文字，請確定`ALLOW_ENCRYPTED_VALUE_MODIFICATIONS`啟用使用者的設定。

加密的資料行上運作時下, 表提供動作的摘要：

|`ColumnEncryption`|BCP 方向|Description|
|----------------|-------------|-----------|
|`Disabled`|OUT （至用戶端）|擷取密碼文字。 觀察到的資料類型是**varbinary （max)**。|
|`Enabled`|OUT （至用戶端）|擷取純文字。 驅動程式會解密資料行的資料。|
|`Disabled`|在 （伺服器）|將插入的加密文字。 這被為了透明而不需要移動加密的資料解密。 如果作業會失敗`ALLOW_ENCRYPTED_VALUE_MODIFICATIONS`選項未設定使用者，或連接控制代碼上未設定 BCPMODIFYENCRYPTED。 如需詳細資訊，請參閱下方內容。|
|`Enabled`|在 （伺服器）|將純文字。 驅動程式會加密資料行的資料。|

### <a name="the-bcpmodifyencrypted-option"></a>BCPMODIFYENCRYPTED 選項

若要避免資料損毀，伺服器通常不允許直接插入加密的資料行的加密文字，因此嘗試這樣做將會失敗。不過，對於大量載入加密資料使用 BCP API，設定`BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)為 TRUE 的選項將允許所有直接插入的加密文字，並降低加密的資料損毀高於設定的風險`ALLOW_ENCRYPTED_VALUE_MODIFICATIONS`使用者帳戶上的選項。 然而，金鑰必須符合資料而且最好先執行一些唯讀檢查的插入的資料大量插入後，才能進一步使用。

請參閱[移轉保護的敏感性資料透過永遠加密](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)如需詳細資訊。

## <a name="always-encrypted-api-summary"></a>一律加密 API 摘要

### <a name="connection-string-keywords"></a>連接字串關鍵字

|名稱|Description|  
|----------|-----------------|  
|`ColumnEncryption`|接受的值為`Enabled` / `Disabled`。<br>`Enabled`-啟用連接的一律加密功能。<br>`Disabled`-停用連線的永遠加密功能。 <br><br>預設值為 `Disabled`。|  
|`KeyStoreAuthentication` | 有效值： `KeyVaultPassword`，`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | 當`KeyStoreAuthentication`  =  `KeyVaultPassword`，將此值設定為有效的 Azure Active Directory 使用者主體名稱。 <br>當`KeyStoreAuthetication`  =  `KeyVaultClientSecret`將此值設定為有效 Azure Active Directory 應用程式用戶端識別碼 |
|`KeyStoreSecret` | 當`KeyStoreAuthentication`  =  `KeyVaultPassword`將此值設定為對應的使用者名稱的密碼。 <br>當`KeyStoreAuthentication`  =  `KeyVaultClientSecret`將此值設定為有效 Azure Active Directory 應用程式用戶端識別碼相關聯的應用程式密碼|

### <a name="connection-attributes"></a>連接屬性

|名稱|型別|Description|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|連線前|`SQL_COLUMN_ENCRYPTION_DISABLE`(0)--停用永遠加密 <br>`SQL_COLUMN_ENCRYPTION_ENABLE`(1)--啟用永遠加密|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|連線後|[設定]嘗試載入 CEKeystoreProvider<br>[取得]傳回 CEKeystoreProvider 名稱|
|`SQL_COPT_SS_CEKEYSTOREDATA`|連線後|[設定]將資料寫入至 CEKeystoreProvider<br>[取得]從 CEKeystoreProvider 讀取資料|

### <a name="statement-attributes"></a>陳述式屬性

|名稱|Description|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED`(0)--永遠加密已停用陳述式 <br>`SQL_CE_RESULTSETONLY`(1)--只解密。 結果集和傳回值都會解密，並不會加密參數 <br>`SQL_CE_ENABLED`(3)--一律加密是啟用及使用參數和結果|

### <a name="descriptor-fields"></a>描述項欄位

|IPD 欄位|大小/類型|預設值|Description|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD （2 個位元組）|0|當 0 （預設值）： 決策，來加密此參數由加密中繼資料的可用性。<br><br>當為非零： 如果加密中繼資料可供此參數，它會加密。 否則，要求會失敗，錯誤 [CE300] [Microsoft] [ODBC Driver 13 for SQL Server] 強制加密已指定參數，但伺服器未提供任何加密中繼資料。|

### <a name="bcpcontrol-options"></a>bcp_control 選項

|選項名稱|預設值|Description|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|若為 TRUE，允許 varbinary （max） 值插入加密的資料行。 若為 FALSE，防止插入提供正確型別和加密的中繼資料。|

## <a name="see-also"></a>另請參閱

- [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [永遠加密部落格](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

