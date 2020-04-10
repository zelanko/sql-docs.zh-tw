---
title: 搭配 PHP Drivers for SQL Server 使用 Always Encrypted | Microsoft Docs
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-kaywon
ms.author: v-daenge
author: David-Engel
manager: v-mabarw
ms.openlocfilehash: 81119187f1f00814e5b50dc97e41a506fe94131e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926827"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>搭配 PHP Drivers for SQL Server 使用 Always Encrypted
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>適用於
 -   Microsoft Drivers 5.2 for PHP for SQL Server
 
## <a name="introduction"></a>簡介

本文提供有關如何使用 [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 和 [PHP Drivers for SQL Server](../../connect/php/Microsoft-php-driver-for-sql-server.md) 來開發 PHP 應用程式的資訊。

[永遠加密] 可讓用戶端應用程式加密敏感性資料，且永遠不會顯示資料或 SQL Server 或 Azure SQL Database 的加密金鑰。 ODBC Driver for SQL Server 等已啟用 Always Encrypted 的驅動程式，以清晰簡明的方式加密與解密用戶端應用程式中的敏感性資料。 驅動程式會自動判斷哪一個查詢參數對應至敏感性資料庫資料行 (使用 [永遠加密] 保護)，然後加密這些參數值後再將資料傳遞至 SQL Server 或 Azure SQL Database。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 如需詳細資訊，請參閱 [一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 PHP Drivers for SQL Server 會利用 ODBC Driver for SQL Server，以加密敏感性資料。

## <a name="prerequisites"></a>Prerequisites

 -   在資料庫中設定永遠加密。 此設定需要佈建 Always Encrypted 金鑰，並為選取的資料庫資料行設定加密。 如果您的資料庫尚未設定 [永遠加密]，請遵循 [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(永遠加密快速入門) 中的指示操作。 特別是，您的資料庫應該包含下列項目的中繼資料定義：「資料行主要金鑰」(CMK)、「資料行加密金鑰」(CEK)，以及包含一或多個使用該 CEK 來加密之資料行的資料表。
 -   請確定已在您的開發電腦上安裝 ODBC Driver for SQL Server version 17 或更高版本。 如需詳細資訊，請參閱 [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。

## <a name="enabling-always-encrypted-in-a-php-application"></a>在 PHP 應用程式中啟用 Always Encrypted

若要對以加密資料行為目標的參數進行加密，以及對查詢結果進行解密，最簡單的方式是將 `ColumnEncryption`連接字串關鍵字的值設定為 `Enabled`。 下列是在 SQLSRV 與 PDO_SQLSRV 驅動程式中啟用 Always Encrypted 的範例：

SQLSRV：
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled");
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV：
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

啟用 Always Encrypted 並不足以確保加密或解密成功；您還必須確定：
 -   應用程式要有 [檢視任何資料行的主要金鑰定義] 和 [檢視任何資料行的加密金鑰定義] 資料庫權限，才能存取資料庫中 Always Encrypted 金鑰的相關中繼資料。 如需詳細資料，請參閱[資料庫權限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。
 -   應用程式可以存取保護所查詢加密資料行之 CEK 的 CMK。 此需求取決於儲存 CMK 的金鑰儲存區提供者。 如需詳細資訊，請參閱[使用資料行主要金鑰存放區](#working-with-column-master-key-stores)。

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料

在您於連線上啟用 Always Encrypted 之後，您便可以使用標準 SQLSRV API (請參閱 [SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)) 或 PDO_SQLSRV API (請參閱 [PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)) 來擷取或修改加密資料庫資料行中的資料。 假設您的應用程式具有必要的資料庫權限，而且能夠存取資料行主要金鑰，則驅動程式會加密所有以加密資料行為目標的查詢參數，並將擷取自加密資料行的資料解密，此行為對應用程式而言是在背景中自動執行，彷彿資料行未經加密一樣。

如未啟用 Always Encrypted，使用以加密資料行為目標的參數查詢就會失敗。 只要查詢沒有以加密資料行為目標的參數，就仍然可以從加密資料行擷取資料。 不過，驅動程式不會嘗試進行任何解密，而應用程式會收到二進位加密資料 (以位元組陣列的形式)。

下表摘要說明查詢的行為，視 Always Encrypted 是否啟用而定：

|查詢特性|[永遠加密] 已啟用，且應用程式可以存取金鑰和金鑰中繼資料|[永遠加密] 已啟用，但應用程式不能存取金鑰或金鑰中繼資料|[永遠加密] 已停用|
|---|---|---|---|
|以加密資料行為目標的參數。|以清晰簡明的方式加密參數值。|錯誤|錯誤|
|從加密的資料行擷取資料，沒有任何以加密資料行為目標的參數。|以清晰簡明的方式解密來自加密資料行的結果。 應用程式會收到純文字資料行值。 |錯誤|不解密來自加密資料行的結果。 應用程式收到位元組陣列形態的加密值。|
 
以下範例將說明擷取和修改加密資料行中的資料。 這些範例假設的是一個具有下列結構描述的資料表。 SSN 和 BirthDate 資料行均已加密。
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
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="data-insertion-example"></a>資料插入範例

下列範例示範如何使用 SQLSRV 和 PDO_SQLSRV 驅動程式，在患者資料表中插入資料列。 請注意下列幾點：
 -   範例程式碼中沒有任何需要加密的特定項目。 驅動程式會自動偵測並加密以加密資料行為目標之 SSN 與 BirthDate 參數的值。 此機制讓加密對應用程式變得透明化。
 -   插入至資料庫資料行的值，包括加密的資料行，會傳遞為繫結參數。 雖然將值傳送到未加密的資料行時，使用參數是選擇性項目 (還是強烈建議使用，因有利於防止 SQL 插入式攻擊)，但它對以加密資料行為目標的值卻是必要項目。 如果將插入 SSN 或 BirthDate 資料行中的值當作內嵌在查詢陳述式中的常值傳遞，則查詢會失敗，因為驅動程式不會嘗試加密或處理查詢中的常數。 結果，伺服器會因與加密資料行不相容而拒絕它們。
 -   使用繫結參數插入值時，必須將與目標資料行之資料類型完全相同，或支援將其轉換成目標資料行之資料類型的 SQL 類型傳遞至資料庫。 這項需求是因為 Always Encrypted 支援幾種類型轉換 (如需詳細資訊，請參閱 [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md))。 SQLSRV 和 PDO_SQLSRV 這兩個 PHP 驅動程式都有一個機制，可協助使用者判斷值的 SQL 類型。 因此，使用者不需要明確地提供 SQL 類型。
  -   若為 SQLSRV 驅動程式，使用者有兩個選項：
   -   依賴 PHP 驅動程式來判斷及設定正確的 SQL 類型。 在此情況下，使用者必須使用 `sqlsrv_prepare` 和 `sqlsrv_execute` 來執行參數化查詢。
   -   明確設定 SQL 類型。
  -   針對 PDO_SQLSRV 驅動程式，使用者沒有明確設定參數之 SQL 類型的選項。 PDO_SQLSRV 驅動程式會在繫結參數時，自動協助使用者判斷 SQL 類型。
 -   為了讓驅動程式判斷 SQL 類型，存在一些限制：
  -   SQLSRV 驅動程式：
   -   如果使用者想要驅動程式判斷加密資料行的 SQL 類型，使用者必須使用 `sqlsrv_prepare` 和 `sqlsrv_execute`。
   -   如果偏好 `sqlsrv_query`，使用者得負責指定所有參數的 SQL 類型。 指定的 SQL 類型必須包含字串類型的字串長度，以及十進位類型的小數位數與精確度。
  -   PDO_SQLSRV 驅動程式：
   -   參數化查詢中不支援陳述式屬性 `PDO::SQLSRV_ATTR_DIRECT_QUERY`。
   -   參數化查詢中不支援陳述式屬性 `PDO::ATTR_EMULATE_PREPARES`。
   
SQLSRV 驅動程式與 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)：
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel;
$birthDate = "1996-10-19";
$params = array($ssn, $firstName, $lastName, $birthDate);
// during sqlsrv_prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = sqlsrv_prepare($conn, $query, $params);
sqlsrv_execute($stmt);
```

SQLSRV 驅動程式與 [sqlsrv_query](../../connect/php/sqlsrv-query.md)：
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel";
$birthDate = "1996-10-19";
// need to provide the SQL types for ALL parameters  
// note the SQL types (including the string length) have to be the same at the column definition
$params = array(array(&$ssn, null, null, SQLSRV_SQLTYPE_CHAR(11)),
                array(&$firstName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$lastName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$birthDate, null, null, SQLSRV_SQLTYPE_DATE));
sqlsrv_query($conn, $query, $params);
```

PDO_SQLSRV 驅動程式與 [PDO::prepare](../../connect/php/pdo-prepare.md)：
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Able";
$birthDate = "1996-10-19";
// during PDO::prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
$stmt->bindParam(2, $firstName);
$stmt->bindParam(3, $lastName);
$stmt->bindParam(4, $birthDate);
$stmt->execute();
```

### <a name="plaintext-data-retrieval-example"></a>純文字資料擷取範例

下列範例會示範根據加密值篩選資料，以及使用 SQLSRV 和 PDO_SQLSRV 驅動程式從加密資料行擷取純文字資料。 請注意下列幾點：
 -   在 WHERE 子句中用來篩選 SSN 資料行的值，需要使用繫結參數傳遞，如此驅動程式可以清晰簡明的方式加密它，再將它傳送至伺服器。
 -   執行具有繫結參數的查詢時，除非使用者在使用 SQLSRV 驅動程式時明確指定 SQL 類型，否則 PHP 驅動程式會針對使用者自動判斷 SQL 類型。
 -   程式列印的所有值都是純文字格式，因為驅動程式會以清晰簡明方式來解密從 SSN 和 BirthDate 資料行擷取的資料。
 
注意:只有當加密具確定性時，查詢才能在加密資料行上執行相等比較。 如需詳細資訊，請參閱[選取確定性或隨機化加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

SQLSRV：
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = sqlsrv_prepare($conn, $query, array(&$ssn));
// during sqlsrv_execute, the driver encrypts the ssn value and passes it to the database
sqlsrv_execute($stmt);
// fetch like usual
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV：
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
// during PDOStatement::execute, the driver encrypts the ssn value and passes it to the database
$stmt->execute();
// fetch like usual
$row = $stmt->fetch();
```

### <a name="ciphertext-data-retrieval-example"></a>加密文字資料擷取範例

如未啟用 [永遠加密]，只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。

下列範例會示範使用 SQLSRV 和 PDO_SQLSRV 驅動程式從加密資料行擷取二進位的加密資料。 請注意下列幾點：
 -   因為連接字串未啟用 Always Encrypted，所以查詢會以位元組陣列 (程式會將值轉換為字串) 傳回加密的 SSN 和 BirthDate 值。
 -   從加密資料行擷取資料但停用 [永遠加密] 的查詢可以有參數，只要沒有任何參數以加密資料行為目標。 下列查詢依 LastName 篩選，在資料庫中未加密。 如果依 SSN 或 BirthDate 篩選查詢，查詢會失敗。
 
SQLSRV：
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = sqlsrv_prepare($conn, $query, array(&$lastName));
sqlsrv_execute($stmt);
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV：
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $lastName);
$stmt->execute();
$row = $stmt->fetch();
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>避免常見的加密資料行查詢問題

本節說明從 PHP 應用程式查詢加密資料行時常見的錯誤類別，以及如何避免的一些方針。

#### <a name="unsupported-data-type-conversion-errors"></a>不支援的資料類型轉換錯誤

[永遠加密] 支援極少數的加密資料類型轉換。 如需支援的類型轉換詳細清單，請參閱 [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 請執行下列作業以免發生資料型別轉換錯誤︰
 -   當搭配 `sqlsrv_prepare` 和 `sqlsrv_execute` SQL 類型使用 SQLSRV 驅動程式時，會自動判斷參數的資料行大小和十進位數。
 -   使用 PDO_SQLSRV 驅動程式執行查詢時，也會自動判斷具有資料行大小和參數之十進位數的 SQL 類型
 -   搭配 `sqlsrv_query` 使用 SQLSRV 驅動程式來執行查詢時：
  -   參數的 SQL 類型與目標資料行的類型完全相同，或是支援從 SQL 類型轉換成資料行的類型。
  -   以 `decimal` 和 `numeric` SQL Server 資料類型資料行為目標之參數的有效位數和小數位數，和為目標資料行設定的有效位數和小數位數相同。
  -   在修改目標資料行的查詢中，以 `datetime2`、`datetimeoffset` 或 `time` SQL Server 資料類型資料行為目標之參數的有效位數，不大於目標資料行的有效位數。
 -   請勿在參數化查詢中使用 PDO_SQLSRV 陳述式屬性 `PDO::SQLSRV_ATTR_DIRECT_QUERY` 或 `PDO::ATTR_EMULATE_PREPARES`
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳送純文字，而不是傳送加密值所造成的錯誤。

任何以加密資料行為目標的值都必須在傳送至伺服器之前先加密。 嘗試對加密資料行插入、修改或以純文字值進行篩選時，會導致發生錯誤。 若要避免這類錯誤，請確定：
 -   Always Encrypted 已啟用 (在連接字串中，將 `ColumnEncryption` 關鍵字設定為 `Enabled`)。
 -   您可以使用繫結參數傳送以加密資料行為目標的資料。 下列範例示範對加密資料行 (SSN) 以常值/常數錯誤篩選：
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>控制永遠加密的影響效能

因為 Always Encrypted 是用戶端加密技術，大部分的效能額外負荷是在用戶端觀察到，不是在資料庫觀察到。 除了加密和解密作業成本之外，用戶端其他的效能額外負荷來源如下：
 -   額外反覆存取資料庫以擷取查詢參數的中繼資料。
 -   呼叫資料行主要金鑰存放區以存取資料行主要金鑰。
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>反覆存取以擷取查詢參數的中繼資料

如果連接已啟用 Always Encrypted，ODBC 驅動程式預設會針對每個參數化查詢呼叫 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)，將查詢陳述式 (不含任何參數值) 傳遞至 SQL Server。 這個預存程序會分析查詢陳述式，以查明是否有任何參數需要加密，如果有，便傳回每個參數的加密相關資訊，以便讓驅動程式加密參數。

由於 PHP 驅動程式可讓使用者不需要提供 SQL 類型就可在備妥的陳述式中繫結參數，因此在啟用 Always Encrypted 的連線中繫結參數時，PHP 驅動程式會在參數上呼叫 [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md) 來取得 SQL 類型、資料行大小和十進位數。 然後，中繼資料會用來呼叫 [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md)。 這些額外的 `SQLDescribeParam` 呼叫不需要額外的資料庫來回行程，因為 ODBC 驅動程式已在呼叫 `sys.sp_describe_parameter_encryption` 時，將資訊儲存在用戶端上。

上述行為可確保讓用戶端應用程式享有高透明度 (且應用程式開發人員) 無須知道哪些查詢會存取加密資料行，只要以加密資料行為目標的值會傳遞給參數中的驅動程式即可。

不同於 ODBC Driver for SQL Server，PHP 驅動程式尚不支援在陳述式/查詢層級啟用 Always Encrypted。 

### <a name="column-encryption-key-caching"></a>資料行加密金鑰快取

為了將呼叫資料行主要金鑰存放區來解密資料行加密金鑰 (CEK) 的次數減少，驅動程式會將純文字 CEK 快取至記憶體中。 從資料庫中繼資料收到加密 CEK (ECEK) 之後，ODBC 驅動程式會先嘗試尋找與快取中加密金鑰值對應的純文字 CEK。 只有在快取中找不到對應的純文字 CEK 時，驅動程式才會呼叫包含 CMK 的金鑰存放區。

注意:在 ODBC Driver for SQL Server 中，快取中的項目會在兩小時逾時之後被收回。 此行為意謂著針對指定的 ECEK，驅動程式在應用程式存留期間或每隔兩小時 (以較短者為準) 會連絡金鑰存放區一次。

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區

若要將資料加密或解密，驅動程式必須取得為目標資料行設定的 CEK。 CEK 會以加密形式 (ECEK) 儲存在資料庫中繼資料中。 每個 CEK 都有一個用來加密它的對應 CMK。 [資料庫中繼資料](../../t-sql/statements/create-column-master-key-transact-sql.md)本身並不儲存 CMK；它只包含金鑰存放區的名稱，以及金鑰存放區可用來尋找 CMK 的資訊。

為了取得 ECEK 的純文字值，驅動程式會先取得 CEK 及其相對應 CMK 的相關中繼資料，然後使用此資訊來聯絡包含 CMK 的金鑰存放區，並要求它將 ECEK 解密。 驅動程式會使用金鑰存放區提供者來與金鑰存放區進行通訊。

針對 Microsoft Driver 5.3.0 for PHP for SQL Server，只支援 Windows 憑證存放區提供者和 Azure Key Vault。 尚不支援 ODBC 驅動程式所支援的其他金鑰儲存區提供者 (自訂金鑰儲存區提供者)。

### <a name="using-the-windows-certificate-store-provider"></a>使用 Windows 憑證存放區提供者

Windows 上的 ODBC Driver for SQL Server 包含「Windows 憑證存放區」的內建資料行主要金鑰存放區提供者，名為 `MSSQL_CERTIFICATE_STORE`。 (macOS 或 Linux 上無法使用此提供者)。使用此提供者時，CMK 會儲存在本機用戶端電腦上，應用程式無須進行任何額外設定，即可將它與驅動程式搭配使用。 不過，應用程式必須能夠存取存放區中的憑證及其私密金鑰。 如需詳細資訊，請參閱 [建立及儲存資料行主要金鑰 (永遠加密)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

### <a name="using-azure-key-vault"></a>使用 Azure Key Vault

Azure Key Vault 提供使用 Azure 儲存加密金鑰、密碼和其他祕密的方法，並可用於儲存 Always Encrypted 的金鑰。 ODBC Driver for SQL Server (17 版及更高版本) 包含 Azure Key Vault 的內建主要金鑰存放區提供者。 下列連線選項會處理 Azure Key Vault 設定：`KeyStoreAuthentication`、`KeyStorePrincipalId` 和 `KeyStoreSecret`。 
 -   `KeyStoreAuthentication` 可以接受兩個可能字串值的其中一個：`KeyVaultPassword` 和 `KeyVaultClientSecret`。 這些值會控制與其他兩個關鍵字搭配使用的驗證認證類型。
 -   `KeyStorePrincipalId` 會取得字串，該字串代表要存取 Azure Key Vault 之帳戶的識別碼。 
     -   如果 `KeyStoreAuthentication` 設定為 `KeyVaultPassword`，則 `KeyStorePrincipalId` 必須是 Azure Active Directory 使用者的名稱。
     -   如果 `KeyStoreAuthentication` 設定為 `KeyVaultClientSecret`，則 `KeyStorePrincipalId` 必須是應用程式用戶端識別碼。
 -   `KeyStoreSecret` 會取得代表認證密碼的字串。 
     -   如果 `KeyStoreAuthentication` 設定為 `KeyVaultPassword`，則 `KeyStoreSecret` 必須是使用者的密碼。 
     -   如果 `KeyStoreAuthentication` 設定為 `KeyVaultClientSecret`，則 `KeyStoreSecret` 必須是與應用程式用戶端識別碼相關聯的應用程式密碼。

這三個選項都必須存在於連接字串中，才能使用 Azure Key Vault。 此外，`ColumnEncryption` 必須設定為 `Enabled`。 如果 `ColumnEncryption` 設定為 `Disabled` 但有 Azure Key Vault 選項，則指令碼會繼續執行而不會發生錯誤，但不會執行任何加密。

下列範例示範如何使用 Azure Key Vault 連接到 SQL Server。

SQLSRV：

使用 Azure Active Directory 帳戶：
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultPassword", "KeyStorePrincipalId"=>$AADUsername, "KeyStoreSecret"=>$AADPassword);
$conn = sqlsrv_connect($server, $connectionInfo);
```
使用 Azure 應用程式用戶端識別碼和密碼：
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultClientSecret", "KeyStorePrincipalId"=>$applicationClientID, "KeyStoreSecret"=>$applicationClientSecret);
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV：使用 Azure Active Directory 帳戶：
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultPassword; KeyStorePrincipalId = $AADUsername; KeyStoreSecret = $AADPassword;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```
使用 Azure 應用程式用戶端識別碼和密碼：
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultClientSecret; KeyStorePrincipalId = $applicationClientID; KeyStoreSecret = $applicationClientSecret;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>使用 Always Encrypted 時的 PHP 驅動程式限制

SQLSRV 和 PDO_SQLSRV：
 -   Linux/macOS 不支援 Windows 憑證存放區提供者
 -   強制參數加密
 -   在陳述式層級啟用 Always Encrypted 
 -   在 Linux 和 macOS 上使用 Always Encrypted 功能和非 UTF8 地區設定時 (例如"en_US.ISO-8859-1")，除非您的系統上已安裝字碼頁 1252，否則將 null 資料或空字串插入至加密的 char(n) 資料行可能無法使用
 
僅限 SQLSRV：
 -   在不指定 SQL 類型的情況下，使用 `sqlsrv_query` 來繫結參數
 -   在 SQL 陳述式的批次中使用 `sqlsrv_prepare` 來繫結參數  
 
僅限 PDO_SQLSRV：
 -   參數化查詢中指定的 `PDO::SQLSRV_ATTR_DIRECT_QUERY` 陳述式屬性
 -   參數化查詢中指定的 `PDO::ATTR_EMULATE_PREPARE` 陳述式屬性
 -   在 SQL 陳述式的批次中繫結參數
 
PHP 驅動程式也會繼承 ODBC Driver for SQL Server 和資料庫所加諸的限制。 請參閱[使用 Always Encrypted 時的 ODBC 驅動程式限制](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)和 [Always Encrypted 功能詳細資料](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details)。  
  
## <a name="see-also"></a>另請參閱  
[PHP SQL 驅動程式程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  

[PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
