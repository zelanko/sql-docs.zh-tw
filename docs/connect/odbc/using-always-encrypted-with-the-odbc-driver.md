---
title: 搭配使用 Always Encrypted 與 ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
ms.author: v-chojas
author: MightyPen
ms.openlocfilehash: bf15831517ebaa8646c1d6f3c080033c3a41405d
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594370"
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>搭配使用 Always Encrypted 與 ODBC Driver for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>適用於

- ODBC Driver 13.1 for SQL Server
- ODBC Driver 17 for SQL Server

### <a name="introduction"></a>簡介

此文章提供有關如何使用 [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 或[具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) 與 [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md) 來開發 ODBC 應用程式的資訊。

[永遠加密] 可讓用戶端應用程式加密敏感性資料，且永遠不會顯示資料或 SQL Server 或 Azure SQL Database 的加密金鑰。 ODBC Driver for SQL Server 等啟用了 Always Encrypted 的驅動程式，以清晰簡明的方式加密與解密用戶端應用程式中的敏感性資料來達成此目的。 驅動程式會自動判斷哪一個查詢參數對應至敏感性資料庫資料行 (使用 [永遠加密] 保護)，然後加密這些參數值後再將資料傳遞至 SQL Server 或 Azure SQL Database。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 「具有安全記憶體保護區的 Always Encrypted」  會延伸此功能以啟用更豐富的敏感性資料功能，同時保持資料的機密性。

如需詳細資訊，請參閱[Always Encrypted （資料庫引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和[使用安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。

### <a name="prerequisites"></a>Prerequisites

在資料庫中設定永遠加密。 這牽涉到佈建永遠加密金鑰，以及設定加密所選資料庫資料行。 如果您的資料庫尚未設定 [永遠加密]，請遵循 [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(永遠加密快速入門) 中的指示操作。 特別是，您的資料庫應該包含下列項目的中繼資料定義：「資料行主要金鑰」(CMK)、「資料行加密金鑰」(CEK)，以及包含一或多個使用該 CEK 來加密之資料行的資料表。

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>在 ODBC 應用程式中啟用 Always Encrypted

若要同時啟用參數加密和結果集加密資料行解密，最簡單的方式是將 `ColumnEncryption` 連接字串關鍵字的值設定為 **Enabled**。 可啟用 Always Encrypted 的連接字串範例如下：

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

您也可以使用相同的金鑰和值 (如果有連接字串設定，則會由此設定覆寫)，或透過程式設計方式使用 `SQL_COPT_SS_COLUMN_ENCRYPTION` 連線前屬性，在 DSN 設定中啟用 Always Encrypted。 以這種方式設定它會覆寫連接字串或 DSN 中設定的值：

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

針對連線啟用 Always Encrypted 之後，便可以針對個別查詢調整其行為。 如需詳細資訊，請參閱下方的[控制 Always Encrypted 的效能影響](#controlling-the-performance-impact-of-always-encrypted)。

請注意，啟用 Always Encrypted 並不足以確保加密或解密成功；您還必須確定：

- 應用程式要有 [檢視任何資料行的主要金鑰定義]  和 [檢視任何資料行的加密金鑰定義]  資料庫權限，才能存取資料庫中永遠加密金鑰的相關中繼資料。 如需詳細資料，請參閱[資料庫權限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。

- 應用程式可以存取保護所查詢加密資料行之 CEK 的 CMK。 這取決於儲存 CMK 的金鑰存放區提供者。 如需詳細資訊，請參閱[使用資料行主要金鑰存放區](#working-with-column-master-key-stores)。

### <a name="enabling-always-encrypted-with-secure-enclaves"></a>啟用具有安全記憶體保護區的 Always Encrypted

從 17.4 版開始，驅動程式支援具有安全記憶體保護區的 Always Encrypted。 若要在連接到 SQL Server 2019 或更新版本時啟用使用記憶體保護區，請將 `ColumnEncryption` DSN、連接字串或連接屬性設定為記憶體保護區類型和證明通訊協定的名稱，以及相關聯的證明資料，並以逗號分隔。 在17.4 版中，只支援以[虛擬化為基礎的安全性](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/)記憶體保護區類型和[主機守護者服務](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server)證明通訊協定（以 `VBS-HGS`表示）;若要使用它，請指定證明伺服器的 URL，例如：

```
Driver=ODBC Driver 17 for SQL Server;Server=yourserver.yourdomain;Trusted_Connection=Yes;ColumnEncryption=VBS-HGS,http://attestationserver.yourdomain/Attestation
```

如果已正確設定伺服器和證明服務，以及所需資料行的記憶體保護區啟用 Cmk 和 Cek，您現在應該能夠執行使用記憶體保護區的查詢，例如就地加密和豐富計算，以及Always Encrypted 提供的現有功能。 如需詳細資訊，請參閱[使用 secure 記憶體保護區設定 Always Encrypted](../../relational-databases/security/encryption/configure-always-encrypted-enclaves.md) 。


### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料

一旦您在連線上啟用 Always Encrypted 之後，就可以使用標準 ODBC Api。 ODBC Api 可以抓取或修改加密資料庫資料行中的資料。 下列檔專案可能會有説明：

- [ODBC 範例程式碼](cpp-code-example-app-connect-access-sql-db.md)
- [ODBC 程式設計人員參考](../../odbc/reference/odbc-programmer-s-reference.md)

您的應用程式必須具有必要的資料庫許可權，而且必須能夠存取資料行主要金鑰。 然後，驅動程式會將以加密資料行為目標的任何查詢參數加密。 驅動程式也會將從加密資料行抓取的資料解密。 驅動程式會執行所有的加密和解密，而不會有原始程式碼的協助。 在您的程式中，就像資料行未加密一樣。

如未啟用 Always Encrypted，使用目標加密資料行參數的查詢就會失敗。 只要查詢沒有以加密資料行為目標的參數，就仍然可以從加密資料行擷取資料。 不過，驅動程式不會嘗試進行任何解密，而應用程式則會收到二進位加密資料 (以位元組陣列的形式)。

下表摘要說明查詢的行為，視 Always Encrypted 是否啟用而定：

|查詢特性 | [永遠加密] 已啟用，且應用程式可以存取金鑰和金鑰中繼資料|[永遠加密] 已啟用，但應用程式不能存取金鑰或金鑰中繼資料 | [永遠加密] 已停用|
|:---|:---|:---|:---|
| 以加密資料行為目標的參數。 | 以清晰簡明的方式加密參數值。 | 錯誤 | 錯誤|
| 從加密的資料行擷取資料，沒有任何以加密資料行為目標的參數。| 以清晰簡明的方式解密來自加密資料行的結果。 應用程式會收到純文字資料行值。 | 錯誤 | 不解密來自加密資料行的結果。 應用程式收到位元組陣列形態的加密值。

以下範例將說明擷取和修改加密資料行中的資料。 這些範例假設的是一個具有下列結構描述的資料表。 請注意，SSN 和 BirthDate 資料行均已加密。

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

- 範例程式碼中沒有任何需要加密的特定項目。 驅動程式會自動偵測並加密以加密資料行為目標之 SSN 與日期參數的值。 這讓加密對應用程式變得透明化。

- 插入至資料庫資料行的值，包括加密的資料行，會傳遞為繫結參數 (請參閱 [SQLBindParameter 函式](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx))。 雖然將值傳送到未加密的資料行時，使用參數是選擇性項目 (還是強烈建議使用，因有利於防止 SQL 插入式攻擊)，但它對以加密資料行為目標的值卻是必要項目。 如果將插入 SSN 或 BirthDate 資料行中的值當作內嵌在查詢陳述式中的常值傳遞，則查詢會失敗，因為驅動程式不會嘗試加密或處理查詢中的常數。 結果，伺服器會因與加密資料行不相容而拒絕它們。

- 插入 SSN 資料行中之參數的 SQL 類型會設定為 SQL_CHAR，這會對應至 **char** SQL Server 資料類型 (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`)。 如果參數類型設定為 SQL_WCHAR (對應至 **nchar**)，則查詢會失敗，因為 Always Encrypted 不支援在伺服器端進行從加密的 nchar 值到加密的 char 值的轉換。 如需有關資料類型對應的資訊，請參閱 [ODBC 程式設計人員參考 -- 附錄 D：資料類型](https://msdn.microsoft.com/library/ms713607.aspx) \(部分機器翻譯\)。

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
> 只有在加密具決定性，或已啟用安全記憶體保護區時，查詢才能在加密資料行上執行相等比較。 如需詳細資訊，請參閱[選取確定性或隨機化加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

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

[永遠加密] 支援極少數的加密資料類型轉換。 如需支援的類型轉換詳細清單，請參閱 [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 為了避免資料類型轉換錯誤，請確定您在使用 SQLBindParameter 搭配以加密資料行為目標的參數時，注意到下列幾點：

- 參數的 SQL 類型與目標資料行的類型完全相同，或是支援從 SQL 類型轉換成資料行的類型。

- 以 `decimal` 和 `numeric` SQL Server 資料類型資料行為目標之參數的有效位數和小數位數，和為目標資料行設定的有效位數和小數位數相同。

- 在修改目標資料行的查詢中，以 `datetime2`、`datetimeoffset` 或 `time` SQL Server 資料類型資料行為目標之參數的有效位數，不大於目標資料行的有效位數。  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳送純文字，而不是傳送加密值所造成的錯誤。

任何以加密資料行為目標的值都必須在傳送至伺服器之前先加密。 嘗試對加密資料行插入、修改或以純文字值進行篩選時，會導致發生錯誤。 若要避免這類錯誤，請確定：

- Always Encrypted 已啟用 (藉由在連線前，於 DSN、連接字串中設定特定連線的 `SQL_COPT_SS_COLUMN_ENCRYPTION` 連線屬性，或特定陳述式的 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 陳述式屬性)。

- 您可以使用 SQLBindParameter 傳送以加密資料行為目標的資料。 下列範例顯示對加密資料行 (SSN) 以常值/常數錯誤篩選，而不是以引數將常值傳遞至 SQLBindParameter 的查詢。

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>使用 SQLSetPos 和 SQLMoreResults 時的預防措施

#### <a name="sqlsetpos"></a>SQLSetPos

`SQLSetPos` API 可讓應用程式使用與 SQLBindCol 繫結的緩衝區來更新資料集內的資料列，並且更新到先前擷取資料列資料的位置中。 由於加密的固定長度類型有非對稱的填補行為，因此有可能在於資料列中的其他資料行上執行更新時，意外地改變資料。 使用 AE 時，如果值小於緩衝區大小，就會填補固定長度字元值。

若要減輕此行為造成的影響，請使用 `SQL_COLUMN_IGNORE` 旗標來忽略不會在 `SQLBulkOperations` 過程中更新的資料行，以及不會在使用 `SQLSetPos` 進行資料指標型更新時更新的資料行。  為了效能考量，以及避免將繫結至比其實際 (DB) 大小「還要小」  之緩衝區的資料行截斷，應該忽略所有不會由應用程式直接修改的資料行。 如需詳細資訊，請參閱 [SQLSetPos 函式參考](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx) \(部分機器翻譯\)。

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults 和 SQLDescribeCol

應用程式可以呼叫 [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) 來傳回準備陳述式中資料行的相關中繼資料。  已啟用 Always Encrypted 時，在呼叫 `SQLDescribeCol`「之前」  先呼叫 `SQLMoreResults` 會導致呼叫 [sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)，這不會正確地傳回加密資料行的純文字中繼資料。 若要避免此問題，請在呼叫 `SQLMoreResults`「之前」  先呼叫 `SQLDescribeCol`。

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>控制 Always Encrypted 的效能影響

因為 Always Encrypted 是用戶端加密技術，大部分的效能額外負荷是在用戶端觀察到，不是在資料庫觀察到。 除了加密和解密作業成本之外，用戶端其他的效能額外負荷來源如下：

- 額外反覆存取資料庫以擷取查詢參數的中繼資料。

- 呼叫資料行主要金鑰存放區以存取資料行主要金鑰。

本節描述 JDBC Driver for SQL Server 的內建效能最佳化，以及如何控制上述兩個因素對效能的影響。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制反覆存取以擷取查詢參數的中繼資料

如果連線已啟用 Always Encrypted，此驅動程式預設會針對每個參數化查詢呼叫 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)，將查詢陳述式 (不含任何參數值) 傳遞至 SQL Server。 這個預存程序會分析查詢陳述式，以查明是否有任何參數需要加密，如果有，便傳回每個參數的加密相關資訊，以便讓驅動程式加密參數。 上述行為可確保讓用戶端應用程式享有高透明度：只要以加密資料行為目標的值會傳遞給參數中的驅動程式，應用程式 (以及應用程式開發人員) 便無須知道哪些查詢會存取加密資料行。

### <a name="per-statement-always-encrypted-behavior"></a>個別陳述式的 Always Encrypted 行為

若要控制擷取參數化查詢之加密中繼資料的效能影響，您可以改變個別查詢的 Always Encrypted 行為 (如果已在連線上啟用此行為)。 如此一來，您便可以確保只有針對已知具有以加密資料行為目標之參數的查詢，才會叫用 `sys.sp_describe_parameter_encryption`。 不過請注意，如此一來會降低加密的透明度︰如果您將資料庫中的其他資料行加密，您可能需要變更應用程式的程式碼，以配合結構描述的變更。

若要控制陳述式的 Always Encrypted 行為，請呼叫 SQLSetStmtAttr 以將 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 陳述式屬性設定為下列其中一個值：

|ReplTest1|Description|
|-|-|
|`SQL_CE_DISABLED` (0)|針對陳述式停用 Always Encrypted|
|`SQL_CE_RESULTSETONLY` (1)|僅解密。 將結果集和傳回值解密，但不將參數解密|
|`SQL_CE_ENABLED` (3) | 同時針對參數和結果啟用並使用 Always Encrypted|

新陳述式控制代碼若是從已啟用 Always Encrypted 的連線所建立，就會預設為 SQL_CE_ENABLED。 若是從已停用 Always Encrypted 的連線所建立，則會預設為 SQL_CE_DISABLED (且無法為它們啟用 Always Encrypted)。

如果用戶端應用程式的大多數查詢都會存取加密資料行，則以下是建議事項：

- 將 `ColumnEncryption` 連接字串關鍵字設定為 `Enabled`。

- 針對不會存取任何加密資料行的陳述式，將 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 屬性設定為 `SQL_CE_DISABLED`。 這會導致無法呼叫 `sys.sp_describe_parameter_encryption`，以及無法嘗試解密結果集內的任何值。
    
- 針對沒有任何需要加密的參數但會從加密資料行擷取資料的陳述式，將 `SQL_SOPT_SS_COLUMN_ENCRYPTION`屬性設定為 `SQL_CE_RESULTSETONLY`。 這會導致無法呼叫 `sys.sp_describe_parameter_encryption` 和進行參數加密。 包含加密資料行的結果將繼續進行解密。

## <a name="always-encrypted-security-settings"></a>Always Encrypted 安全性設定

### <a name="force-column-encryption"></a>強制資料行加密

若要強制將參數加密，請透過呼叫 SQLSetDescField 函式來設定 `SQL_CA_SS_FORCE_ENCRYPT` 實作參數描述項 (IPD) 欄位。 值若不是零，會導致驅動程式在系統未針對相關聯參數傳回任何加密中繼資料時傳回錯誤。

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

如果 SQL Server 向驅動程式告知參數不需要加密，使用該參數的查詢就會失敗。 這會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，此類 SQL Server 會將不正確的加密中繼資料提供給用戶端，而可能導致資料洩露。

### <a name="column-encryption-key-caching"></a>資料行加密金鑰快取

為了將呼叫資料行主要金鑰存放區來解密資料行加密金鑰的次數減少，驅動程式會將純文字 CEK 快取至記憶體中。 CEK 快取對驅動程式而言是全域的，未與任何一個連線相關聯。 從資料庫中繼資料收到 ECEK 之後，驅動程式會先嘗試尋找與快取中加密金鑰值對應的純文字 CEK。 只有在快取中找不到對應的純文字 CEK 時，驅動程式才會呼叫包含 CMK 的金鑰存放區。

> [!NOTE]
> 在 ODBC Driver for SQL Server 中，快取中的項目會在兩小時逾時之後被收回。 這意謂著針對指定的 ECEK，驅動程式在應用程式存留期間或每隔兩小時 (以較短者為準) 會連絡金鑰存放區一次。

從 ODBC Driver 17.1 for SQL Server 開始，即可使用 `SQL_COPT_SS_CEKCACHETTL` 連線屬性來調整 CEK 快取逾時，此屬性會指定 CEK 將在快取中存留的時間 (秒)。 由於快取的全域本質，因此從對驅動程式有效的任何連線控制代碼都可以調整此屬性。 當快取 TTL 減少時，系統會一併收回會超出新 TTL 的現有 CEK。 如果是 0，則不會快取任何 CEK。

### <a name="trusted-key-paths"></a>受信任的金鑰路徑

從 ODBC Driver 17.1 for SQL Server 開始，`SQL_COPT_SS_TRUSTEDCMKPATHS` 連線屬性可讓應用程式要求 Always Encrypted 作業只使用指定的 CMK (以其金鑰路徑識別) 清單。 此屬性預設為 NULL，表示驅動程式會接受任何金鑰路徑。 若要使用此功能，請將 `SQL_COPT_SS_TRUSTEDCMKPATHS`設定成指向以 Null 分隔、以 Null 結尾並列出所允許金鑰路徑的寬字元字串。 此屬性所指向的記憶體必須在加密或解密期間保持有效 (使用已在記憶體上設定的連線控制代碼) --- 驅動程式會對其檢查伺服器中繼資料所指定的 CMK 路徑在此清單中是否不區分大小寫。 如果 CMK 路徑不在清單中，作業就會失敗。 應用程式可以變更此屬性所指向的記憶體內容以變更其受信任的 CMK 清單，而無須重新設定屬性。

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區

若要將資料加密或解密，驅動程式必須取得為目標資料行設定的 CEK。 CEK 會以加密形式 (ECEK) 儲存在資料庫中繼資料中。 每個 CEK 都有一個用來加密它的對應 CMK。 [資料庫中繼資料](../../t-sql/statements/create-column-master-key-transact-sql.md)本身並不儲存 CMK；它只包含金鑰存放區的名稱，以及金鑰存放區可用來尋找 CMK 的資訊。

為了取得 ECEK 的純文字值，驅動程式會先取得 CEK 及其相對應 CMK 的相關中繼資料，然後使用此資訊來聯絡包含 CMK 的金鑰存放區，並要求它將 ECEK 解密。 驅動程式會使用金鑰存放區提供者來與金鑰存放區進行通訊。

### <a name="built-in-keystore-providers"></a>內建的金鑰存放區提供者

ODBC Driver for SQL Server 隨附下列內建的金鑰存放區提供者：

| [屬性] | Description | 提供者 (中繼資料) 名稱 |可用性|
|:---|:---|:---|:---|
|Azure 金鑰保存庫 |將 CMK 儲存在 Azure Key Vault 中 | `AZURE_KEY_VAULT` |Windows、macOS、Linux|
|Windows 憑證存放區|將 CMK 儲存在本機 Windows 金鑰存放區中| `MSSQL_CERTIFICATE_STORE`|Windows|

- 您 (或您的 DBA) 需要確認設定在資料行主要金鑰中繼資料的提供者名稱是否正確，且資料行主要金鑰路徑符合指定提供者的金鑰路徑格式。 建議您使用 SQL Server Management Studio 等工具設定金鑰，這樣在發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) 陳述式時，會自動產生有效的提供者名稱和金鑰路徑。

- 您需要確定應用程式可以存取金鑰儲存區中的金鑰。 這可能牽涉到授與應用程式金鑰及/或金鑰儲存區的存取權 (視金鑰儲存區而定)，或執行其他的金鑰儲存區特定設定步驟。 例如，若要存取 Azure Key Vault，您必須將正確的認證提供給金鑰存放區。

### <a name="using-the-azure-key-vault-provider"></a>使用 Azure Key Vault 提供者

Azure Key Vault (AKV) 是存放和管理 Always Encrypted 資料行主要金鑰的方便選項 (尤其是當應用程式裝載在 Azure 中時)。 Linux、macOS 及 Windows 上的 ODBC Driver for SQL Server 包含 Azure Key Vault 的內建資料行主要金鑰存放區提供者。 如需有關設定適用於 Always Encrypted 之 Azure Key Vault 的詳細資訊，請參閱 [Azure Key Vault - 逐步解說](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) \(英文\)、[金鑰保存庫使用者入門](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)及[在 Azure Key Vault 中建立資料行主要金鑰](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2)。

> [!NOTE]
> ODBC 驅動程式不支援 AKV authentication 的 Active Directory 同盟服務。 如果您使用 Azure Active Directory authentication AKV，而您的 Active Directory 設定包含同盟服務，則驗證可能會失敗。
> 在 Linux 和 macOS 上，針對驅動程式 17.2 版和更新版本，必須要有 `libcurl`，才能使用此提供者，但這不是明確相依性，因為驅動程式的其他作業並不需要它。 如果您遇到有關 `libcurl` 的錯誤，請確定它已安裝。

驅動程式支援使用下列認證類型向 Azure Key Vault 進行驗證：

- 使用者名稱/密碼 - 使用此方法時，認證係指 Azure Active Directory 使用者名稱及其密碼。

- 用戶端識別碼/祕密 - 使用此方法時，認證係指應用程式用戶端識別碼和應用程式祕密。

為了允許驅動程式使用儲存在 AKV 中的 CMK 來進行資料行加密，請使用下列僅限連接字串的關鍵字：

|認證類型| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|使用者名稱/密碼| `KeyVaultPassword`|使用者主體名稱|[密碼]|
|用戶端識別碼/祕密| `KeyVaultClientSecret`|用戶端識別碼|祕密|

#### <a name="example-connection-strings"></a>範例連接字串

下列連接字串顯示如何使用兩種認證類型向 Azure Key Vault 進行驗證：

**用戶端識別碼/祕密**：

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**使用者名稱/密碼**：

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

無須進行其他 ODBC 應用程式變更，即可使用 AKV 來儲存 CMK。

### <a name="using-the-windows-certificate-store-provider"></a>使用 Windows 憑證存放區提供者

Windows 上的 ODBC Driver for SQL Server 包含「Windows 憑證存放區」的內建資料行主要金鑰存放區提供者，名為 `MSSQL_CERTIFICATE_STORE`。 (macOS 或 Linux 上無法使用此提供者)。使用此提供者時，CMK 會儲存在本機用戶端電腦上，應用程式無須進行任何額外設定，即可將它與驅動程式搭配使用。 不過，應用程式必須能夠存取存放區中的憑證及其私密金鑰。 如需詳細資訊，請參閱[建立及儲存資料行主要金鑰 (Always Encrypted)](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted)。

### <a name="using-custom-keystore-providers"></a>使用自訂金鑰儲存區提供者

ODBC Driver for SQL Server 也支援使用 CEKeystoreProvider 介面來自訂協力廠商金鑰存放區提供者。 這可讓應用程式載入、查詢及設定金鑰存放區提供者，以便供驅動程式用來存取加密資料行。 應用程式也可以直接與金鑰存放區提供者進行互動，來加密 CEK 以儲存在 SQL Server 中，以及執行以 ODBC 存取加密資料行以外的工作；如需詳細資訊，請參閱[自訂金鑰存放區提供者](../../connect/odbc/custom-keystore-providers.md)。

有兩個連線屬性會用來與自訂金鑰存放區提供者進行互動。 其中包括：

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

前者可用來載入和列舉已載入的金鑰存放區提供者，後者則可啟用應用程式提供者通訊。 這些連線屬性隨時都可使用，不論是在建立連線之前還是之後，因為應用程式提供者互動並未牽涉到與 SQL Server 進行通訊。 不過，由於尚未載入驅動程式，因此在連線前設定和取得這些屬性將促使「驅動程式管理員」處理它們，而可能不會產生預期的結果。

#### <a name="loading-a-keystore-provider"></a>載入金鑰存放區提供者

設定 `SQL_COPT_SS_CEKEYSTOREPROVIDER` 連線屬性可讓用戶端應用程式載入提供者程式庫，讓其中所含的金鑰存放區提供者變成可供使用。

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| 引數 | Description |
|:---|:---|
|`ConnectionHandle`|[輸入] 連線控制代碼。 必須是有效的連線控制代碼，但提供者若是透過一個連線控制代碼載入的，則從相同處理序中的任何其他提供者都可存取這些提供者。|
|`Attribute`|[輸入] 要設定的屬性：`SQL_COPT_SS_CEKEYSTOREPROVIDER` 常數。|
|`ValuePtr`|[輸入] 以 Null 結尾之字元字串的指標，這是指定提供者程式庫之檔案名稱的字元字串。 就 SQLSetConnectAttrA 而言，這會是 ANSI (多位元組) 字串。 就 SQLSetConnectAttrW 而言，這會是 Unicode (wchar_t) 字串。|
|`StringLength`|[輸入] 輸入 ValuePtr 字串或 SQL_NTS 的長度。|

驅動程式會使用平台定義的動態程式庫載入機制 (在 Linux 和 macOS 上是 `dlopen()`，在 Windows 上是 `LoadLibrary()`) 來嘗試載入 ValuePtr 參數所識別的程式庫，然後將該處定義的任何提供者新增至驅動程式已知的提供者清單。 以下是可能發生的錯誤：

| 錯誤 | Description |
|:--|:--|
|`CE203`|無法載入動態程式庫。|
|`CE203`|在程式庫中找不到 "CEKeyStoreProvider" 匯出的符號。|
|`CE203`|已經載入程式庫中的一或多個提供者。|

`SQLSetConnectAttr` 會傳回一般錯誤或成功值，且針對任何已發生的錯誤，都會透過標準 ODBC 診斷機制提供額外的資訊。

> [!NOTE]
> 應用程式程式設計人員必須確保在透過任何連線傳送需要任何自訂提供者的任何查詢之前，先載入這些提供者。 無法執行這項操作時，會導致發生錯誤：

| 錯誤 | Description |
|:--|:--|
|`CE200`|找不到金鑰存放區提供者 %1。 請確定已載入適當的金鑰存放區提供者程式庫。|

> [!NOTE]
> 金鑰存放區提供者實施者應該避免在其自訂提供者的名稱中使用 `MSSQL`。 這個詞彙是專門保留給 Microsoft 使用，而可能造成與未來的內建提供者發生衝突。 在自訂提供者的名稱中使用這個詞彙可能會造成 ODBC 警告。

#### <a name="getting-the-list-of-loaded-providers"></a>取得載入的提供者清單

取得此連線屬性可讓用戶端應用程式判斷目前在驅動程式中載入的金鑰存放區提供者 (包括內建的提供者)。此操作只能在連線後執行。

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| 引數 | Description |
|:---|:---|
|`ConnectionHandle`|[輸入] 連線控制代碼。 必須是有效的連線控制代碼，但提供者若是透過一個連線控制代碼載入的，則從相同處理序中的任何其他提供者都可存取這些提供者。|
|`Attribute`|[輸入] 要擷取的屬性：`SQL_COPT_SS_CEKEYSTOREPROVIDER` 常數。|
|`ValuePtr`|[輸出] 記憶體的指標，這是其中要傳回下一個所載入提供者名稱的記憶體。|
|`BufferLength`|[輸入] 緩衝區 ValuePtr 的長度。|
|`StringLengthPtr`|[輸出] 緩衝區的指標，這是其中要傳回可供在 \*ValuePtr 中傳回之位元組總數 (不包括以 Null 結尾的字元) 的緩衝區。 如果 ValuePtr 是 Null 指標，則不會傳回任何長度。 如果屬性值是字元字串，且可供傳回的位元組數大於 BufferLength 減去以 Null 結尾之字元長度所得的數目，則 \*ValuePtr 中的資料會依據 BufferLength 減去以 Null 結尾之字元長度所得的數目截斷，並由驅動程式以 Null 結尾。|

為了允許擷取整個清單，每個 Get 作業都會傳回目前提供者的名稱，並讓內部計數器在到下一個提供者時遞增。 當此計數器到達清單結尾時，就會傳回空字串 ("")，然後計數器會重設；後續的 Get 作業會接著再次從清單開頭繼續進行。

### <a name="communicating-with-keystore-providers"></a>與金鑰存放區提供者進行通訊

`SQL_COPT_SS_CEKEYSTOREDATA` 連線屬性可讓用戶端應用程式與已載入的金鑰存放區提供者進行通訊，以設定額外的參數、金鑰產製原料等。用戶端應用程式與提供者之間的通訊會根據使用此連線屬性的 Get 和 Set 要求，依循簡單的「要求-回應」通訊協定。 通訊只會由用戶端應用程式起始。

> [!NOTE]
> 由於 ODBC 的本質是會呼叫 CEKeyStoreProvider 對 (SQLGet/SetConnectAttr) 的回應，因此 ODBC 介面僅支援在解析連線內容時設定資料。

應用程式會透過驅動程式、經由 CEKeystoreData 結構與金鑰存放區提供者進行通訊：

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```

| 引數 | Description |
|:---|:---|
|`name`|[輸入] 進行 Set 時，要作為資料傳送對象的提供者名稱。 進行 Get 時會忽略。 以 Null 結尾的寬字元字串。|
|`dataSize`|[輸入] 接在結構之後的資料陣列大小。|
|`data`|[InOut] 進行 Set 時，要傳送給提供者的資料。 這可以是任意資料；驅動程式不會嘗試解譯它。 進行 Get 時，要接收從提供者讀取之資料的緩衝區。|

#### <a name="writing-data-to-a-provider"></a>將資料寫入至提供者

使用 `SQL_COPT_SS_CEKEYSTOREDATA` 屬性的 `SQLSetConnectAttr` 呼叫會將資料「封包」寫入至指定的金鑰存放區提供者。
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| 引數 | Description |
|:---|:---|
|`ConnectionHandle`| [輸入] 連線控制代碼。 必須是有效的連線控制代碼，但提供者若是透過一個連線控制代碼載入的，則從相同處理序中的任何其他提供者都可存取這些提供者。|
|`Attribute`|[輸入] 要設定的屬性：`SQL_COPT_SS_CEKEYSTOREDATA` 常數。|
|`ValuePtr`|[輸入] CEKeystoreData 結構的指標。 結構的名稱欄位會識別要作為資料適用對象的提供者。|
|`StringLength`|[輸入] SQL_IS_POINTER 常數|

額外的詳細錯誤資訊可透過 [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx) 取得。

> [!NOTE]
> 如果需要，提供者可以使用連線控制代碼將寫入的資料與特定連線建立關聯。 這對於實作個別連線設定來說，相當實用。 它也可以忽略連線內容，而不論用來傳送資料的連線為何，都以一致的方式處理資料。 如需詳細資訊，請參閱[內容關聯](../../connect/odbc/custom-keystore-providers.md#context-association)。

#### <a name="reading-data-from-a-provider"></a>從提供者讀取資料

使用 `SQL_COPT_SS_CEKEYSTOREDATA` 屬性的 `SQLGetConnectAttr` 呼叫會從「上次寫入的」  提供者讀取資料「封包」。 如果沒有任何提供者，就會發生「函數順序錯誤」。 建議金鑰存放區提供者實施者支援使用 0 位元組的「虛擬寫入」作為一種選取讀取作業之提供者而不會造成其他副作用的方式 (如果這麼做有意義的話)。

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| 引數 | Description |
|:---|:---|
|`ConnectionHandle`|[輸入] 連線控制代碼。 必須是有效的連線控制代碼，但提供者若是透過一個連線控制代碼載入的，則從相同處理序中的任何其他提供者都可存取這些提供者。|
|`Attribute`|[輸入] 要擷取的屬性：`SQL_COPT_SS_CEKEYSTOREDATA` 常數。|
|`ValuePtr`|[輸出] CEKeystoreData 結構的指標，這是其中放置從提供者讀取之資料的結構。|
|`BufferLength`|[輸入] SQL_IS_POINTER 常數|
|`StringLengthPtr`|[輸出] 緩衝區的指標，這是其中要傳回 BufferLength 的緩衝區。 如果 *ValuePtr 是 Null 指標，則不會傳回任何長度。|

呼叫端必須確保在 CEKEYSTOREDATA 結構之後配置長度足夠的緩衝區以供提供者寫入。 傳回時，其 dataSize 欄位中會填入從提供者讀取之資料的實際長度。 額外的詳細錯誤資訊可透過 [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx) 取得。

此介面對於在應用程式與金鑰存放區提供者之間傳輸的資料格式沒有任何額外需求。 每個提供者都可以依據其需求，定義自己的通訊協定/資料格式。

如需有關實作您自己金鑰存放區提供者的範例，請參閱[自訂金鑰存放區提供者](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>使用 Always Encrypted 時的 ODBC 驅動程式限制

### <a name="asynchronous-operations"></a>非同步作業
雖然 ODBC 驅動程式會允許搭配 Always Encrypted 使用[非同步作業](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md)，但在啟用 Always Encrypted 的情況下，會影響作業效能。 用以判斷陳述式之加密中繼資料的 `sys.sp_describe_parameter_encryption` 呼叫會封鎖驅動程式，並造成驅動程式會先等候伺服器傳回中繼資料，然後才傳回 `SQL_STILL_EXECUTING`。

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>使用 SQLGetData 來分段擷取資料
在 ODBC Driver 17 for SQL Server 之前，無法使用 SQLGetData 來分段擷取加密字元和二進位資料行。 只能搭配長度足以包含整個資料行之資料的緩衝區，對 SQLGetData 進行一次呼叫。

### <a name="send-data-in-parts-with-sqlputdata"></a>使用 SQLPutData 來分段傳送資料
在 ODBC Driver 17.3 for SQL Server 之前，無法使用 SQLPutData 來分段傳送用於插入或比較的資料。 只能搭配包含整個資料的緩衝區，對 SQLPutData 進行一次呼叫。 若要將長資料插入至加密資料行，請使用「大量複製 API」(下一節會提供說明) 搭配輸入資料檔。

### <a name="encrypted-money-and-smallmoney"></a>加密的 money 和 smallmoney
加密的 **money** 或 **smallmoney** 資料行無法作為參數目標，因為沒有與這些類型對應的特定 ODBC 資料類型，所以會導致發生「運算元類型衝突」錯誤。

## <a name="bulk-copy-of-encrypted-columns"></a>大量複製加密資料行

從 ODBC Driver 17 for SQL Server 開始，便支援搭配 Always Encrypted 使用 [SQL 大量複製函式](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)和 **bcp** 公用程式。 不論是純文字 (在插入時加密，然後在擷取時解密) 還是加密文字 (逐字傳輸)，您都可以使用「大量複製 (bcp_&#42;) API」和 **bcp** 公用程式來插入和擷取。

- 若要擷取 varbinary(max) 形式的加密文字 (例如，用於大量載入至不同的資料庫)，請在不使用 `ColumnEncryption` 選項 (若將其設定為 `Disabled`) 的情況下連線，然後執行 BCP OUT 作業。

- 若要插入和擷取純文字，並讓驅動程式視需要在背景中自動執行加密和解密，則將 `ColumnEncryption` 設定為 `Enabled` 即已足夠。 除此之外，BCP API 的功能則不變。

- 若要插入 varbinary(max) 形式的加密文字 (例如，如上述所擷取)，請將 `BCPMODIFYENCRYPTED` 選項設定為 TRUE，然後執行 BCP IN 作業。 為了讓產生的資料可供解密，請確定目的地資料行的 CEK 與原先取得加密文字時的來源 CEK 相同。

使用 **bcp** 公用程式時：若要控制 `ColumnEncryption` 設定，請使用 -D 選項並指定包含所需值的 DSN。 若要插入加密文字，請確定已啟用使用者的 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 設定。

下表提供在加密資料行上操作時的動作摘要：

|`ColumnEncryption`|BCP 方向|Description|
|----------------|-------------|-----------|
|`Disabled`|OUT (至用戶端)|擷取加密文字。 觀察到的資料類型是 **varbinary(max)** 。|
|`Enabled`|OUT (至用戶端)|擷取純文字。 驅動程式會將資料行資料解密。|
|`Disabled`|IN (至伺服器)|插入加密文字。 這是用來以隱含方式移動加密資料，而不要求將其解密。 如果未在使用者上設定 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 選項，或未在連線控制代碼上設定 BCPMODIFYENCRYPTED，此作業就會失敗。 如需詳細資訊，請參閱下方內容。|
|`Enabled`|IN (至伺服器)|插入純文字。 驅動程式會將資料行資料加密。|

### <a name="the-bcpmodifyencrypted-option"></a>BCPMODIFYENCRYPTED 選項

為了防止資料損毀，伺服器通常不允許將加密文字直接插入至加密資料行，因此嘗試這麼做會失敗；不過，若是使用 BCP API 來大量載入加密資料，則將 `BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 選項設定為 TRUE 將可允許直接插入加密文字，而降低有關在使用者帳戶上設定 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 選項所造成的損毀加密資料風險。 不過，金鑰必須與資料相符，而理想的做法是在進行大量插入後及在進一步使用之前，對插入的資料執行一些唯讀檢查。

如需詳細資訊，請參閱[移轉透過 Always Encrypted 保護的敏感性資料](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。

## <a name="always-encrypted-api-summary"></a>Always Encrypted API 摘要

### <a name="connection-string-keywords"></a>連接字串關鍵字

|[屬性]|Description|  
|----------|-----------------|  
|`ColumnEncryption`|接受的值為 `Enabled`/`Disabled`。<br>`Enabled` -- 啟用連線的 Always Encrypted 功能。<br>`Disabled` -- 停用連線的 Always Encrypted 功能。<br>*類型*、*資料*--（17.4 版和更新版本）可讓 Always Encrypted 具有安全記憶體保護區和證明通訊協定*類型*，以及相關聯的證明資料*資料*。 <br><br>預設值為 `Disabled`。|
|`KeyStoreAuthentication` | 有效的值：`KeyVaultPassword`、`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | 當 `KeyStoreAuthentication` = `KeyVaultPassword` 時，請將此值設定為有效的「Azure Active Directory 使用者主體名稱」。 <br>當 `KeyStoreAuthetication` = `KeyVaultClientSecret` 時，請將此值設定為有效的「Azure Active Directory 應用程式用戶端識別碼」 |
|`KeyStoreSecret` | 當 `KeyStoreAuthentication` = `KeyVaultPassword` 時，請將此值設定為相對應使用者名稱的密碼。 <br>當 `KeyStoreAuthentication` = `KeyVaultClientSecret` 時，請將此值設定為與有效「Azure Active Directory 應用程式用戶端識別碼」相關聯的「應用程式祕密」 |


### <a name="connection-attributes"></a>連接屬性

|[屬性]|類型|Description|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|連線前|`SQL_COLUMN_ENCRYPTION_DISABLE` (0) -- 停用 Always Encrypted <br>`SQL_COLUMN_ENCRYPTION_ENABLE` (1) -- 啟用 Always Encrypted<br> *類型*的指標，*資料*字串--（版本17.4 和更新版本）啟用安全記憶體保護區|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|連線後|[Set] 嘗試載入 CEKeystoreProvider<br>[Get] 傳回 CEKeystoreProvider 名稱|
|`SQL_COPT_SS_CEKEYSTOREDATA`|連線後|[Set] 將資料寫入至 CEKeystoreProvider<br>[Get] 從 CEKeystoreProvider 讀取資料|
|`SQL_COPT_SS_CEKCACHETTL`|連線後|[Set] 設定 CEK 快取 TTL<br>[Get] 取得目前的 CEK 快取 TTL|
|`SQL_COPT_SS_TRUSTEDCMKPATHS`|連線後|[Set] 設定受信任的 CMK 路徑指標<br>[Get] 取得目前的受信任 CMK 路徑指標|

### <a name="statement-attributes"></a>陳述式屬性

|[屬性]|Description|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED` (0) -- 針對陳述式停用 Always Encrypted <br>`SQL_CE_RESULTSETONLY` (1) -- 僅解密。 將結果集和傳回值解密，但不將參數解密 <br>`SQL_CE_ENABLED` (3) -- 同時針對參數和結果啟用並使用 Always Encrypted|

### <a name="descriptor-fields"></a>描述項欄位

|IPD 欄位|大小/類型|預設值|Description|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 個位元組)|0|若為 0 (預設)：加密此參數的決定會取決於加密中繼資料的可用性。<br><br>若不為 0：如果有加密中繼資料可供此參數使用，就會加密。 否則，要求會因以下錯誤而失敗：[CE300] [Microsoft][ODBC Driver 13 for SQL Server]已為參數指定了強制加密，但伺服器沒有提供任何加密中繼資料。|

### <a name="bcp_control-options"></a>bcp_control 選項

|選項名稱|預設值|Description|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|若為 TRUE，允許將 varbinary(max) 值插入至加密資料行。 若為 FALSE，除非提供正確的類型和加密中繼資料，否則會防止插入。|

## <a name="see-also"></a>另請參閱

- [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)
- [永遠加密部落格](https://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)
