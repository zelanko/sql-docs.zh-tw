---
title: 搭配使用 Always Encrypted 與 ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: a0c917c6f7200db2b5a04b47185ba6b61f59ad34
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506833"
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>搭配使用 Always Encrypted 與 ODBC Driver for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>適用於

- ODBC Driver 13.1 for SQL Server
- ODBC Driver 17 for SQL Server

### <a name="introduction"></a>簡介

本文章提供有關如何開發使用 ODBC 應用程式的資訊[Always Encrypted （資料庫引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)並[ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。

[永遠加密] 可讓用戶端應用程式加密敏感性資料，且永遠不會顯示資料或 SQL Server 或 Azure SQL Database 的加密金鑰。 ODBC Driver for SQL Server 等啟用了 Always Encrypted 的驅動程式，以清晰簡明的方式加密與解密用戶端應用程式中的敏感性資料來達成此目的。 驅動程式會自動判斷哪一個查詢參數對應至敏感性資料庫資料行 (使用 [永遠加密] 保護)，然後加密這些參數值後再將資料傳遞至 SQL Server 或 Azure SQL Database。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 如需詳細資訊，請參閱 [一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。

### <a name="prerequisites"></a>Prerequisites

在資料庫中設定永遠加密。 這牽涉到佈建永遠加密金鑰，以及設定加密所選資料庫資料行。 如果您的資料庫尚未設定 [永遠加密]，請遵循 [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(永遠加密快速入門) 中的指示操作。 特別是，您的資料庫應該包含資料行主要金鑰 (CMK)、 資料行加密金鑰 (CEK) 和資料表，其中包含一或多個使用該 CEK 加密的資料行的中繼資料定義。

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>啟用 永遠加密在 ODBC 應用程式

啟用參數加密和加密的結果集資料行解密的最簡單方式是藉由設定的值`ColumnEncryption`連接字串關鍵字設**已啟用**。 可啟用 Always Encrypted 的連接字串範例如下：

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

可能也會啟用 永遠加密在 DSN 組態中，使用相同的索引鍵和值 （這將會覆寫設定連接字串，如果有的話），或以程式設計方式使用`SQL_COPT_SS_COLUMN_ENCRYPTION`預先連接屬性。 將它設定為這種方式，將會覆寫連接字串或 DSN 中設定的值：

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

針對連接啟用之後，可調整的 Always Encrypted 行為，個別查詢。 請參閱[控制的效能影響的 Always Encrypted](#controlling-the-performance-impact-of-always-encrypted)如下如需詳細資訊。

請注意，啟用 永遠加密不足，無法加密或解密成功;您也需要確定：

- 應用程式要有 [檢視任何資料行的主要金鑰定義] 和 [檢視任何資料行的加密金鑰定義] 資料庫權限，才能存取資料庫中永遠加密金鑰的相關中繼資料。 如需詳細資訊，請參閱 <<c0> [ 資料庫的權限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。

- 應用程式可以存取用來保護查詢加密資料行的 Cek CMK。 這是相依於儲存 CMK 的金鑰儲存區提供者。 請參閱[使用 資料行主要金鑰存放區](#working-with-column-master-key-stores)如需詳細資訊。

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料

一旦您啟用 「 一律加密的連接上，您可以使用標準 ODBC Api (請參閱[ODBC 範例程式碼](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953)或是[ODBC 程式設計人員參考](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx)) 來擷取或修改加密的資料庫資料行中的資料。 假設您的應用程式具有必要資料庫權限可以存取資料行主要金鑰，驅動程式會將加密的目標加密資料行和資料擷取自加密資料行，以透明的方式運作，以解密任何查詢參數應用程式，如同未加密的資料行。

如未啟用 Always Encrypted，使用目標加密資料行參數的查詢就會失敗。 只要查詢沒有以加密資料行為目標的參數，就仍然可以從加密資料行擷取資料。 不過，此驅動程式將不會嘗試任何解密，而且應用程式將會收到二進位的加密的資料 （以位元組陣列）。

下表摘要說明查詢的行為，視 Always Encrypted 是否啟用而定：

|查詢特性 | [永遠加密] 已啟用，且應用程式可以存取金鑰和金鑰中繼資料|[永遠加密] 已啟用，但應用程式不能存取金鑰或金鑰中繼資料 | [永遠加密] 已停用|
|:---|:---|:---|:---|
| 以加密的資料行為目標的參數。 | 以清晰簡明的方式加密參數值。 | 錯誤 | 錯誤|
| 從加密的資料行擷取資料，沒有任何以加密資料行為目標的參數。| 以清晰簡明的方式解密來自加密資料行的結果。 應用程式收到純文字資料行的值。 | 錯誤 | 不解密來自加密資料行的結果。 應用程式收到位元組陣列形態的加密值。

以下範例將說明擷取和修改加密資料行中的資料。 此範例假設具有下列結構描述的資料表。 請注意，SSN 和 BirthDate 資料行均已加密。

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

- 範例程式碼中沒有任何需要加密的特定項目。 驅動程式會自動偵測並加密的 SSN 和日期參數，其目標為加密的資料行的值。 這讓加密對應用程式變得透明化。

- 插入至資料庫資料行的值，包括加密的資料行，會傳遞為繫結參數 (請參閱 [SQLBindParameter 函式](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx))。 雖然將值傳送到未加密的資料行時，使用參數是選擇性項目 (還是強烈建議使用，因有利於防止 SQL 插入式攻擊)，但它對以加密資料行為目標的值卻是必要項目。 如果插入 SSN 或 BirthDate 資料行中的值傳遞做為內嵌在查詢陳述式中的常值，則查詢會失敗，因為驅動程式不會嘗試加密，或處理查詢中的常值。 結果，伺服器會因與加密資料行不相容而拒絕它們。

- SQL 類型的插入 SSN 資料行的參數設定為 SQL_CHAR，這會對應到**char** SQL Server 資料類型 (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`)。 如果參數的型別設定為 SQL_WCHAR，這會對應到**nchar**，則查詢會失敗，因為永遠加密 不支援加密的 nchar 值的伺服器端轉換成加密的 char 值。 請參閱[ODBC 程式設計人員參考-附錄 d： 資料類型](https://msdn.microsoft.com/library/ms713607.aspx)如需有關資料類型對應資訊。

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

- 在 WHERE 子句中用來篩選 SSN 資料行的值，需要使用 SQLBindParameter 傳遞，如此驅動程式可以清晰簡明方式來加密它，再將它傳送至伺服器。

- 程式列印的所有值都是純文字格式，因為驅動程式會以清晰簡明方式來解密從 SSN 和 BirthDate 資料行擷取的資料。

> [!NOTE]
> 查詢可以加密資料行上執行相等比較，只有具決定性加密。 如需詳細資訊，請參閱[選取確定性或隨機化加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

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

#### <a name="ciphertext-data-retrieval-example"></a>密碼文字資料擷取範例

如未啟用 [永遠加密]，只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。

下列範例會示範從加密資料行擷取二進位的加密資料。 請注意下列事項：

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

本節描述從 ODBC 應用程式查詢加密資料行時常見的錯誤類別，以及如何避免的一些指導方針。

##### <a name="unsupported-data-type-conversion-errors"></a>不支援的資料類型轉換錯誤

[永遠加密] 支援極少數的加密資料類型轉換。 如需支援的類型轉換詳細清單，請參閱 [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 若要避免資料類型轉換錯誤，請確定 SQLBindParameter 使用以加密的資料行為目標的參數時，觀察下列幾點：

- 參數的 SQL 型別正是可以做為目標的資料行的類型相同，或支援從 SQL 類型轉換成資料行的類型。

- 以 `decimal` 和 `numeric` SQL Server 資料類型資料行為目標之參數的有效位數和小數位數，和為目標資料行設定的有效位數和小數位數相同。

- 在修改目標資料行的查詢中，以 `datetime2`、`datetimeoffset` 或 `time` SQL Server 資料類型資料行為目標之參數的有效位數，不大於目標資料行的有效位數。  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳送純文字，而不是傳送加密值所造成的錯誤。

目標加密資料行的任何值，就需要加密再傳送至伺服器。 嘗試對加密資料行插入、修改或以純文字值進行篩選時，會導致發生錯誤。 若要避免這類錯誤，請確定：

- 已啟用 永遠加密 (DSN、 連接字串，在之前連接藉由設定`SQL_COPT_SS_COLUMN_ENCRYPTION`是否有特定的連接，連接屬性或`SQL_SOPT_SS_COLUMN_ENCRYPTION`特定陳述式的陳述式屬性)。

- 您可以使用 SQLBindParameter 傳送以加密資料行為目標的資料。 下列範例顯示對加密資料行 (SSN) 以常值/常數錯誤篩選，而不是以引數將常值傳遞至 SQLBindParameter 的查詢。

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>使用 SQLSetPos 和 SQLMoreResults 時的預防措施

#### <a name="sqlsetpos"></a>SQLSetPos

`SQLSetPos` API 可讓應用程式更新中將使用的緩衝區，已與 SQLBindCol 繫結和先前擷取到哪一個資料列資料的結果集的資料列。 由於加密的固定長度類型的非對稱的填補行為，因此，非預期地修改這些資料行的資料，資料列中的其他資料行上執行更新時項目。 AE，如果值小於緩衝區大小，將會填補固定的長度的字元值。

若要解決這個問題，使用`SQL_COLUMN_IGNORE`忽略將不會更新一部分的資料行的旗標`SQLBulkOperations`以及何時使用`SQLSetPos`以資料指標為基礎的更新。  不會被直接修改應用程式的所有資料行應該忽略，兩者的效能，並避免截斷的資料行繫結至緩衝區*較小*比其實際 (DB) 的大小。 如需詳細資訊，請參閱 < [SQLSetPos 函式參考](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx)。

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

應用程式可能會呼叫[SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx)備妥的陳述式中傳回資料行中繼資料。  啟用永遠加密時，呼叫`SQLMoreResults`*之前*呼叫`SQLDescribeCol`造成[sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)呼叫，這不會正確傳回純文字加密的資料行的中繼資料。 若要避免這個問題，請呼叫`SQLDescribeCol`備妥的陳述式*之前*呼叫`SQLMoreResults`。

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>控制 Always Encrypted 的效能影響

因為 Always Encrypted 是用戶端加密技術，大部分的效能額外負荷是在用戶端觀察到，不是在資料庫觀察到。 除了加密和解密作業成本之外，用戶端其他的效能額外負荷來源如下：

- 額外反覆存取資料庫以擷取查詢參數的中繼資料。

- 呼叫資料行主要金鑰存放區以存取資料行主要金鑰。

本節描述 JDBC Driver for SQL Server 的內建效能最佳化，以及如何控制上述兩個因素對效能的影響。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制反覆存取以擷取查詢參數的中繼資料

如果連線已啟用 Always Encrypted，此驅動程式預設會針對每個參數化查詢呼叫 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)，將查詢陳述式 (不含任何參數值) 傳遞至 SQL Server。 這個預存程序會分析查詢陳述式，若要了解，如果任何參數需要加密，而且如果是的話，傳回每個參數，以允許將其加密驅動程式的加密相關資訊。 上述行為可確保高透明度，用戶端應用程式： 應用程式 （及應用程式開發人員） 不需要留意哪些查詢存取加密的資料行，只要目標為加密資料行值會傳遞至在參數中驅動程式。

### <a name="per-statement-always-encrypted-behavior"></a>每個陳述式 Always Encrypted 行為

若要控制擷取參數化查詢的加密中繼資料的效能影響，您可以變更個別查詢的 Always Encrypted 行為，如果已啟用在連接上。 如此一來，您可以確保`sys.sp_describe_parameter_encryption`只針對查詢，您知道有以加密的資料行為目標的參數時，才會叫用。 不過請注意，如此一來會降低加密的透明度︰如果您將資料庫中的其他資料行加密，您可能需要變更應用程式的程式碼，以配合結構描述的變更。

若要控制永遠加密 行為的陳述式，呼叫設定 SQLSetStmtAttr`SQL_SOPT_SS_COLUMN_ENCRYPTION`陳述式屬性，以下列值之一：

|ReplTest1|Description|
|-|-|
|`SQL_CE_DISABLED` (0)|永遠加密已停用陳述式|
|`SQL_CE_RESULTSETONLY` (1)|僅解密。 系統會解密結果集和傳回值，並不會加密參數|
|`SQL_CE_ENABLED` (3) | 永遠加密已啟用，並使用參數和結果|

使用 永遠加密的連線建立新的陳述式控制代碼啟用至 SQL_CE_ENABLED 的預設值。 從與它的連線建立停用預設為 SQL_CE_DISABLED （而且不可能在其上啟用 「 一律加密）。

如果大部分的用戶端應用程式查詢存取加密資料行，下列建議：

- 將 `ColumnEncryption` 連接字串關鍵字設定為 `Enabled`。

- 設定`SQL_SOPT_SS_COLUMN_ENCRYPTION`屬性設定為`SQL_CE_DISABLED`陳述式不會存取任何加密資料行上。 這會停用這兩個呼叫`sys.sp_describe_parameter_encryption`以及嘗試解密結果中的任何值設定。
    
- 設定`SQL_SOPT_SS_COLUMN_ENCRYPTION`屬性設定為`SQL_CE_RESULTSETONLY`上並沒有任何參數要求加密，但從加密資料行擷取資料的陳述式。 這會停用呼叫`sys.sp_describe_parameter_encryption`和參數加密。 包含加密資料行的結果將會繼續進行解密。

## <a name="always-encrypted-security-settings"></a>Always Encrypted 安全性設定

### <a name="force-column-encryption"></a>強制資料行加密

若要強制加密參數，設定`SQL_CA_SS_FORCE_ENCRYPT`實作參數描述項 (IPD) 欄位透過 SQLSetDescField 函式呼叫。 為非零的值會使驅動程式相關聯的參數不傳回任何加密中繼資料時，傳回錯誤。

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

如果 SQL Server 向驅動程式告知參數不需要加密，使用該參數的查詢就會失敗。 這會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，此類 SQL Server 會將不正確的加密中繼資料提供給用戶端，而可能導致資料洩露。

### <a name="column-encryption-key-caching"></a>資料行加密金鑰快取

若要減少資料行主要金鑰存放區來解密資料行加密金鑰的呼叫數目，此驅動程式會快取在記憶體中的純文字 Cek。 CEK 快取是通用的驅動程式，並不相關聯的任何一個連線。 從接收之後 ECEK 資料庫中繼資料，此驅動程式會先嘗試尋找純文字 CEK 值對應的加密金鑰快取中。 驅動程式會呼叫包含 CMK，只有當快取中找不到對應的純文字 CEK 的金鑰存放區。

> [!NOTE]
> ODBC Driver for SQL Server，在兩個小時逾時之後收回快取中的項目。 這表示針對指定的 ECEK，驅動程式會連絡一次金鑰存放區的應用程式或每隔兩小時的存留期間，兩者中較少。

從 SQL server ODBC 驅動程式 17.1，CEK 快取逾時可以使用來調整`SQL_COPT_SS_CEKCACHETTL`連接屬性，指定的 CEK 會保留在快取的秒數。 由於全域快取，您可以調整這個屬性，從任何連接控制代碼有效驅動程式。 當也收回快取 TTL 會減少，現有的 Cek 會超過新的 TTL。 如果是 0，則會快取沒有 Cek。

### <a name="trusted-key-paths"></a>受信任金鑰路徑

從 SQL server ODBC 驅動程式 17.1`SQL_COPT_SS_TRUSTEDCMKPATHS`連接屬性可讓應用程式需要 Always Encrypted 的作業，只能使用指定的 Cmk，由其索引鍵路徑清單。 根據預設，這個屬性會是 NULL，表示驅動程式會接受任何機碼的路徑。 若要使用這項功能，將`SQL_COPT_SS_TRUSTEDCMKPATHS`指向 null 分隔、 以 null 結束的寬字元字串會列出允許的金鑰路徑。 在加密或解密作業使用連接控制代碼，它會設定---美元的驅動程式會檢查 CMK 路徑所指定的伺服器中繼資料是否區分在此期間，這個屬性所指向的記憶體必須保持有效清單。 如果 CMK 路徑不在清單中，作業將會失敗。 應用程式可以變更這個屬性指向，而不需要設定該屬性一次變更受信任的 Cmk，其清單的記憶體中的內容。

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區

若要加密或解密資料，驅動程式需要取得已針對目標資料行的 CEK。 Cek 會儲存在資料庫中繼資料中的加密形式 (ECEKs)。 每個 CEK 有相對應的 CMK 用來加密。 [資料庫中繼資料](../../t-sql/statements/create-column-master-key-transact-sql.md)不會儲存 CMK 本身; 它只包含名稱的金鑰儲存區和金鑰儲存區可以用來找出 CMK 的資訊。

若要取得 ECEK 的純文字值，此驅動程式會先取得其相對應的 CMK 和 CEK 的相關中繼資料，然後使用此資訊來連絡包含 CMK 的金鑰存放區，並要求它來解密的 ECEK。 驅動程式會與金鑰存放區使用的金鑰儲存區提供者通訊。

### <a name="built-in-keystore-providers"></a>內建金鑰存放區提供者

ODBC Driver for SQL Server 隨附下列的內建金鑰存放區提供者：

| [屬性] | Description | 提供者 （中繼資料） 名稱 |可用性|
|:---|:---|:---|:---|
|Azure 金鑰保存庫 |在 Azure Key Vault 中儲存 Cmk | `AZURE_KEY_VAULT` |Windows、 macOS、 Linux|
|Windows 憑證存放區|本機儲存在 Windows 金鑰儲存區的 Cmk| `MSSQL_CERTIFICATE_STORE`|Windows|

- 您 (或您的 DBA) 需要確認設定在資料行主要金鑰中繼資料的提供者名稱是否正確，且資料行主要金鑰路徑符合指定提供者的金鑰路徑格式。 建議您使用 SQL Server Management Studio 等工具設定金鑰，這樣在發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) 陳述式時，會自動產生有效的提供者名稱和金鑰路徑。

- 您需要確定應用程式可以存取金鑰儲存區中的金鑰。 這可能牽涉到授與應用程式金鑰及/或金鑰儲存區的存取權 (視金鑰儲存區而定)，或執行其他的金鑰儲存區特定設定步驟。 例如，若要存取 Azure Key Vault，您需要提供正確的認證金鑰儲存區。

### <a name="using-the-azure-key-vault-provider"></a>使用 Azure Key Vault 提供者

Azure 金鑰保存庫是存放和管理永遠加密資料行主要金鑰的方便選項 (尤其是當應用程式裝載在 Azure 時)。 ODBC Driver for Linux、 macOS 和 Windows 上的 SQL Server 包含 Azure Key Vault 的內建的資料行主要金鑰存放區提供者。 請參閱[Azure Key Vault-逐步解說](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)，[開始使用 Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)，並[Azure Key Vault 中建立資料行主要金鑰](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2)如需有關設定 Azure 金鑰保存庫永遠加密。

> [!NOTE]
> 在 Linux 和 macOS，驅動程式 17.2 版和更新版本，如`libcurl`，才能使用此提供者，但不明確的相依性，因為其他作業使用驅動程式不需要它。 如果您遇到的錯誤有關`libcurl`，確定它已安裝。

此驅動程式支援使用下列認證類型的 Azure Key Vault 進行驗證：

- 使用者名稱/密碼-使用此方法，認證是在 Azure Active Directory 使用者和其密碼的名稱。

- 用戶端識別碼/密碼-使用此方法，認證是應用程式用戶端識別碼和應用程式祕密。

若要允許使用 AKV 中儲存的資料行加密的 Cmk 驅動程式，請使用下列的只有連接字串關鍵字：

|認證類型| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|使用者名稱/密碼| `KeyVaultPassword`|使用者主體名稱|[密碼]|
|用戶端識別碼/密碼| `KeyVaultClientSecret`|用戶端識別碼|祕密|

#### <a name="example-connection-strings"></a>範例連接字串

下列連接字串示範如何透過兩種認證類型向 Azure Key Vault:

**ClientID/祕密**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**使用者名稱/密碼**

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

任何其他的 ODBC 應用程式變更，不才能使用 AKV 的 CMK 存放區。

### <a name="using-the-windows-certificate-store-provider"></a>使用 Windows 憑證存放區提供者

Windows 上的 SQL Server ODBC 驅動程式包含內建的資料行主要金鑰存放區提供者的 Windows 憑證存放區、 名為`MSSQL_CERTIFICATE_STORE`。 （此提供者無法使用。 在 macOS 或 Linux）與此提供者，CMK 會儲存在本機用戶端電腦上，並由應用程式不需要額外組態，才能使用它來搭配此驅動程式。 不過，應用程式必須存取憑證和私密金鑰存放區中。 如需詳細資訊，請參閱[建立及儲存資料行主要金鑰 (Always Encrypted)](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted)。

### <a name="using-custom-keystore-providers"></a>使用自訂金鑰儲存區提供者

ODBC Driver for SQL Server 也支援使用 CEKeystoreProvider 介面的自訂的協力廠商金鑰儲存區提供者。 這可讓應用程式載入時，查詢，並設定金鑰儲存區提供者，以便供驅動程式來存取加密資料行。 應用程式可能也可以直接互動的金鑰儲存區提供者，以在 SQL Server 中的儲存體加密 Cek，並執行工作存取加密的資料行，使用 ODBC;如需詳細資訊，請參閱 <<c0> [ 自訂金鑰存放區提供者](../../connect/odbc/custom-keystore-providers.md)。

兩個連接屬性用來與自訂金鑰存放區提供者互動。 其中包括：

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

前者用來載入，並列舉已載入的金鑰儲存區提供者，而後者可讓應用程式提供者通訊。 可能在任何時間，使用這些連接屬性之前, 或之後建立連線，因為應用程式提供者互動未牽涉到與 SQL Server 通訊。 不過，因為尚未載入此驅動程式、 設定連接之前取得這些屬性會使其可處理由驅動程式管理員，並可能不會產生預期的結果。

#### <a name="loading-a-keystore-provider"></a>正在載入金鑰儲存區提供者

設定`SQL_COPT_SS_CEKEYSTOREPROVIDER`連接屬性可讓載入提供者程式庫，因此可以使用的金鑰儲存區提供者，其中包含用戶端應用程式。

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| 引數 | Description |
|:---|:---|
|`ConnectionHandle`|[輸入]連接控制代碼。 必須是有效的連接控制代碼，但透過一個連接控制代碼載入提供者會從相同的程序中的任何其他可存取。|
|`Attribute`|[輸入]若要設定的屬性：`SQL_COPT_SS_CEKEYSTOREPROVIDER`常數。|
|`ValuePtr`|[輸入]以 null 結束的字元字串，指定提供者程式庫的檔名的指標。 SQLSetConnectAttrA，這是為 ANSI （多位元組） 的字串。 對於 SQLSetConnectAttrW，這是 Unicode (wchar_t) 字串。|
|`StringLength`|[輸入]SQL_NTS ValuePtr 字串的長度。|

驅動程式嘗試載入使用平台定義動態程式庫載入機制 ValuePtr 參數所識別的程式庫 (`dlopen()`在 Linux 和 macOS 上`LoadLibrary()`在 Windows 上)，並新增任何提供者，其中定義的清單已知的驅動程式提供者。 可能會發生下列錯誤：

| 錯誤 | Description |
|:--|:--|
|`CE203`|無法載入動態程式庫。|
|`CE203`|文件庫中找不到"CEKeyStoreProvider"匯出符號。|
|`CE203`|已載入文件庫中的一或多個提供者。|

`SQLSetConnectAttr` 傳回一般錯誤或成功的值和其他資訊可透過標準的 ODBC 診斷機制發生任何錯誤。

> [!NOTE]
> 應用程式設計人員必須確定任何需要的查詢會透過任何連線傳送之前，會載入任何自訂提供者。 無法執行這項操作時，會導致發生錯誤：

| 錯誤 | Description |
|:--|:--|
|`CE200`|金鑰儲存區提供者 %1 找不到。 請確定已載入適當的金鑰儲存區提供者程式庫。|

> [!NOTE]
> 金鑰儲存區提供者實作項應該避免使用`MSSQL`及其自訂提供者的名稱。 這個詞彙是專用的 Microsoft 保留和與未來的內建提供者可能會造成衝突。 使用這個詞彙的自訂提供者的名稱，可能會導致 ODBC 警告。

#### <a name="getting-the-list-of-loaded-providers"></a>取得載入的提供者清單

取得此連接屬性可讓用戶端應用程式，以判斷目前已載入驅動程式 （包括內建的。） 中的金鑰儲存區提供者這個屬性只能連接之後執行。

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| 引數 | Description |
|:---|:---|
|`ConnectionHandle`|[輸入]連接控制代碼。 必須是有效的連接控制代碼，但透過一個連接控制代碼載入提供者會從相同的程序中的任何其他可存取。|
|`Attribute`|[輸入]若要擷取的屬性：`SQL_COPT_SS_CEKEYSTOREPROVIDER`常數。|
|`ValuePtr`|[輸出]要在其中傳回的下一個載入的提供者名稱的記憶體指標。|
|`BufferLength`|[輸入]ValuePtr 緩衝區的長度。|
|`StringLengthPtr`|[輸出]在其中傳回的總位元組數 （不包括 null 結束字元） 緩衝區的指標可用來傳回中\*ValuePtr。 如果 valueptr 則為 null 指標，則會傳回沒有長度。 如果屬性值是字元字串，而且可用來傳回的位元組數目大於 Columnsize 減去 null 終止的長度字元，在資料\*ValuePtr 就會截斷為 Columnsize 減去的長度null 結束字元，是以 null 終止的驅動程式。|

若要允許擷取整份清單，每個 Get 作業會傳回目前的提供者名稱，並遞增至下一個內部計數器。 一旦此計數器到達清單結尾，空字串 ("") 傳回時，和計數器會重設;後續的 Get 作業則會從清單開頭再繼續。

### <a name="communicating-with-keystore-providers"></a>金鑰儲存區提供者與通訊

`SQL_COPT_SS_CEKEYSTOREDATA`連接屬性可讓用戶端應用程式與載入的金鑰儲存區提供者通訊設定其他參數，設定金鑰材料，依此類推。用戶端應用程式和提供者之間的通訊會遵循簡單的要求-回應通訊協定，以取得和設定可讓您要求使用此連接屬性。 只要用戶端應用程式起始通訊。

> [!NOTE]
> 由於 ODBC 呼叫 CEKeyStoreProvider 的回應 (SQLGet/SetConnectAttr) ODBC 介面唯一支援的連接內容的解析度設定資料。

應用程式會透過驅動程式透過 CEKeystoreData 結構的金鑰儲存區提供者與通訊：

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```
| 引數 | Description |
|:---|:---|
|`name`|[輸入]集合，提供者的名稱時若要將資料傳送。 忽略時取得。 以 null 終止的寬字元字串。|
|`dataSize`|[輸入]下列結構的資料陣列的大小。|
|`data`|[InOut]在集合中，傳送給提供者的資料。 這可能是任意的資料;驅動程式不會嘗試解譯它。 在 Get，要接收資料的緩衝區讀取從提供者。|

#### <a name="writing-data-to-a-provider"></a>將資料寫入至提供者

A`SQLSetConnectAttr`呼叫使用`SQL_COPT_SS_CEKEYSTOREDATA`屬性寫入指定的金鑰儲存區提供者中的 「 封包 」 的資料。
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| 引數 | Description |
|:---|:---|
|`ConnectionHandle`| [輸入]連接控制代碼。 必須是有效的連接控制代碼，但透過一個連接控制代碼載入提供者會從相同的程序中的任何其他可存取。|
|`Attribute`|[輸入]若要設定的屬性：`SQL_COPT_SS_CEKEYSTOREDATA`常數。|
|`ValuePtr`|[輸入]CEKeystoreData 結構指標。 結構的 [名稱] 欄位會識別適用的資料提供者。|
|`StringLength`|[輸入]SQL_IS_POINTER 常數|

透過可取得其他詳細的錯誤資訊[SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)。

> [!NOTE]
> 如果需要提供者可以將寫入的資料與特定的連接，使用連接控制代碼。 這是適合用來實作每個連線設定。 它也可以略過的連接內容，並處理之資料相同不論用來將資料傳送的連接。 請參閱[內容關聯](../../connect/odbc/custom-keystore-providers.md#context-association)如需詳細資訊。

#### <a name="reading-data-from-a-provider"></a>從提供者讀取資料

呼叫`SQLGetConnectAttr`使用`SQL_COPT_SS_CEKEYSTOREDATA`屬性中讀取資料，從 「 封包 」*最後一個寫入-對*提供者。 如果沒有，就會發生函數順序錯誤。 金鑰儲存區提供者實作人員是鼓勵 「 dummy 寫入 」 為 0 的位元組，而不會造成其他副作用，選取讀取作業的提供者，如果適合執行這項操作的方式。

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| 引數 | Description |
|:---|:---|
|`ConnectionHandle`|[輸入]連接控制代碼。 必須是有效的連接控制代碼，但透過一個連接控制代碼載入提供者會從相同的程序中的任何其他可存取。|
|`Attribute`|[輸入]若要擷取的屬性：`SQL_COPT_SS_CEKEYSTOREDATA`常數。|
|`ValuePtr`|[輸出]從提供者讀取的資料位於 CEKeystoreData 結構的指標。|
|`BufferLength`|[輸入]SQL_IS_POINTER 常數|
|`StringLengthPtr`|[輸出]在其中傳回 BufferLength 緩衝區的指標。 如果 * valueptr 則為 null 指標，會傳回任何長度。|

呼叫端必須確保下列 CEKEYSTOREDATA 結構的長度足夠的緩衝區會配置要寫入至提供者。 傳回時，其 dataSize 欄位會更新從提供者讀取資料的實際長度。 透過可取得其他詳細的錯誤資訊[SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)。

這個介面會置於 keystore 提供者和應用程式之間傳輸的資料格式中的任何額外的需求。 每個提供者可以定義自己的通訊協定/資料格式，根據其需求。

如需實作自己的金鑰儲存區提供者的範例，請參閱[自訂金鑰存放區提供者](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>使用永遠加密時，ODBC 驅動程式的限制

### <a name="asynchronous-operations"></a>非同步作業
ODBC 驅動程式會讓使用同時[非同步作業](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md)透過 Always Encrypted，沒有對效能產生影響的作業時啟用 永遠加密。 若要在呼叫`sys.sp_describe_parameter_encryption`若要判斷加密中繼資料的陳述式會封鎖，並會導致驅動程式等候伺服器傳回中繼資料，再傳回`SQL_STILL_EXECUTING`。

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>在使用 SQLGetData 組件中擷取資料
ODBC Driver 17 for SQL Server 加密之前使用 SQLGetData 組件中不能擷取字元和二進位資料行。 可以進行 SQLGetData 只有一個呼叫，以包含整個資料行的資料長度足夠的緩衝區。

### <a name="send-data-in-parts-with-sqlputdata"></a>SQLPutData 使用組件中傳送資料
插入或比較資料無法傳送 SQLPutData 使用組件中。 可以進行 SQLPutData 只有一個呼叫，以包含整個資料的緩衝區。 Long 資料插入加密資料行中，使用 [下一步] 一節所述，使用輸入的資料檔案大量複製 API。

### <a name="encrypted-money-and-smallmoney"></a>加密的 money 和 smallmoney
加密**金錢**或是**smallmoney**參數無法作為資料行的目標，因為沒有不特定 ODBC 資料類型並對應至這些型別，導致運算元類型衝突錯誤。

## <a name="bulk-copy-of-encrypted-columns"></a>大量複製加密的資料行

利用[SQL 大量複製函數](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)並**bcp**公用程式使用 永遠加密自 ODBC Driver 17 for SQL Server 支援。 純文字 （插入上加密和解密上擷取） 和 （逐字傳送） 的加密文字可插入和擷取使用大量複製 （bcp_ *） 的 Api 並**bcp**公用程式。

- 若要擷取 varbinary （max） 格式 （例如為大量載入至不同的資料庫） 的加密文字，請連接，而不`ColumnEncryption`選項 (或將它設定為`Disabled`)，並執行 BCP OUT 作業。

- 插入和擷取純文字，並讓無障礙地執行加密和解密為必要項，設定此驅動程式`ColumnEncryption`至`Enabled`就已足夠。 BCP API 的功能可說是不變。

- 若要插入在 varbinary （max） 的形式 （例如擷取上方） 中的加密文字，請設定`BCPMODIFYENCRYPTED`選項設定為 TRUE，並執行 BCP IN 作業。 如果未產生資料的順序，請確定目的地資料行的 CEK 是原先取得的加密文字相同。

使用時**bcp**公用程式： 控制`ColumnEncryption`設定，請使用-D 選項並指定 DSN，其中包含所要的值。 若要插入的加密文字，請確定`ALLOW_ENCRYPTED_VALUE_MODIFICATIONS`啟用使用者的設定。

下表提供摘要的動作，對加密資料行運作時：

|`ColumnEncryption`|BCP 傳遞方向|Description|
|----------------|-------------|-----------|
|`Disabled`|OUT （以用戶端）|擷取加密文字。 觀察到的資料類型是**varbinary （max)**。|
|`Enabled`|OUT （以用戶端）|擷取純文字。 驅動程式會解密資料行的資料。|
|`Disabled`|在 （伺服器）|將插入的加密文字。 這被要隱含移動加密的資料，而不需要它來進行解密。 作業會失敗，如果`ALLOW_ENCRYPTED_VALUE_MODIFICATIONS`使用者，未設定選項，或連接控制代碼上未設定 BCPMODIFYENCRYPTED。 如需詳細資訊，請參閱下方內容。|
|`Enabled`|在 （伺服器）|插入純文字。 驅動程式會加密資料行的資料。|

### <a name="the-bcpmodifyencrypted-option"></a>BCPMODIFYENCRYPTED 選項

若要避免資料損毀，伺服器通常不允許加密文字直接插入加密資料行，並因此若要這樣做的嘗試將會失敗。不過，對於使用 BCP API、 設定加密的資料大量載入`BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)設為 TRUE 的選項將允許所有直接插入的加密文字，並降低的風險高於設定的損毀加密的資料`ALLOW_ENCRYPTED_VALUE_MODIFICATIONS`的使用者帳戶的選項。 然而，索引鍵必須符合的資料，而且它是個不錯的主意，若要執行某些唯讀狀態的檢查，插入資料，在大量插入之後再進一步使用。

如需詳細資訊，請參閱[移轉透過 Always Encrypted 保護的敏感性資料](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。

## <a name="always-encrypted-api-summary"></a>永遠加密 API 摘要

### <a name="connection-string-keywords"></a>連接字串關鍵字

|[屬性]|Description|  
|----------|-----------------|  
|`ColumnEncryption`|接受的值為`Enabled` / `Disabled`。<br>`Enabled` -- 啟用連線的 Always Encrypted 功能。<br>`Disabled` -- 停用連線的 Always Encrypted 功能。 <br><br>預設值為 `Disabled`。|  
|`KeyStoreAuthentication` | 有效的值：`KeyVaultPassword`、`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | 當`KeyStoreAuthentication`  =  `KeyVaultPassword`，將此值設定為有效的 Azure Active Directory 使用者主體名稱。 <br>當`KeyStoreAuthetication`  =  `KeyVaultClientSecret`將此值設定為有效 Azure Active Directory 應用程式用戶端識別碼 |
|`KeyStoreSecret` | 當`KeyStoreAuthentication`  =  `KeyVaultPassword`將此值設定為對應的使用者名稱的密碼。 <br>當`KeyStoreAuthentication`  =  `KeyVaultClientSecret`將此值設定為有效 Azure Active Directory 應用程式用戶端識別碼相關聯的應用程式祕密|

### <a name="connection-attributes"></a>連接屬性

|[屬性]|類型|Description|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|連線前|`SQL_COLUMN_ENCRYPTION_DISABLE` (0)--停用 Always Encrypted <br>`SQL_COLUMN_ENCRYPTION_ENABLE` (1)--啟用一律加密|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|連線後|[設定]嘗試載入 CEKeystoreProvider<br>[取得]傳回 CEKeystoreProvider 名稱|
|`SQL_COPT_SS_CEKEYSTOREDATA`|連線後|[設定]將資料寫入至 CEKeystoreProvider<br>[取得]從 CEKeystoreProvider 讀取資料|
|`SQL_COPT_SS_CEKCACHETTL`|連線後|[設定]設定 CEK 快取 TTL<br>[取得]取得目前的 CEK 快取 TTL|
|`SQL_COPT_SS_TRUSTEDCMKPATHS`|連線後|[設定]設定受信任的 CMK 路徑指標<br>[取得]取得目前受信任的 CMK 路徑指標|

### <a name="statement-attributes"></a>陳述式屬性

|[屬性]|Description|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED` (0)-for 陳述式會停用 always Encrypted <br>`SQL_CE_RESULTSETONLY` (1)--僅解密。 系統會解密結果集和傳回值，並不會加密參數 <br>`SQL_CE_ENABLED` (3)--永遠加密已啟用，並使用參數和結果|

### <a name="descriptor-fields"></a>描述項欄位

|IPD 欄位|大小/類型|預設值|Description|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD （2 個位元組）|0|當 0 （預設值）： 決定来加密此參數由加密中繼資料的可用性。<br><br>當非零值： 如果加密中繼資料可供此參數，它會加密。 否則，要求會失敗，錯誤 [CE300] [Microsoft] [ODBC Driver 13 for SQL Server] 強制加密已指定為參數，但任何加密中繼資料由伺服器提供。|

### <a name="bcpcontrol-options"></a>bcp_control 選項

|選項名稱|預設值|Description|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|若為 TRUE，允許 varbinary （max） 值插入加密資料行。 若為 FALSE，防止插入提供正確的型別和加密中繼資料。|

## <a name="see-also"></a>另請參閱

- [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [永遠加密部落格](https://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

