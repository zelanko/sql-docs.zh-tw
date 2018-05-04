---
title: 使用 SQL Server 的一律加密的 PHP 驅動程式與 |Microsoft 文件
ms.date: 01/08/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.openlocfilehash: cc5ccc20d4a1a4324933ea64b9126f10df66dd26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>使用 SQL Server 的一律加密與 PHP 驅動程式
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>適用於
 -   Microsoft Drivers for PHP for SQL Server 5.2
 
## <a name="introduction"></a>簡介

本文提供有關如何開發 PHP 應用程式使用資訊[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和[for SQL Server 的 PHP 驅動程式](../../connect/php/Microsoft-php-driver-for-sql-server.md)。

[永遠加密] 可讓用戶端應用程式加密敏感性資料，且永遠不會顯示資料或 SQL Server 或 Azure SQL Database 的加密金鑰。 啟用 永遠加密驅動程式，例如 ODBC Driver for SQL Server，以透明的方式來加密和解密用戶端應用程式中的機密資料。 驅動程式會自動判斷哪一個查詢參數對應至敏感性資料庫資料行 (使用 [永遠加密] 保護)，然後加密這些參數值後再將資料傳遞至 SQL Server 或 Azure SQL Database。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 如需詳細資訊，請參閱 [一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 SQL Server 的 PHP 驅動程式利用 ODBC Driver for SQL Server，來加密機密資料。

## <a name="prerequisites"></a>필수 구성 요소

 -   在資料庫中設定永遠加密。 這項設定包括佈建永遠加密金鑰，並設定選取的資料庫資料行加密。 如果您的資料庫尚未設定 [永遠加密]，請遵循 [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(永遠加密快速入門) 中的指示操作。 特別是，您的資料庫應該包含資料行主要金鑰 (CMK)、 資料行加密金鑰 (CEK) 和資料表包含一個或多個使用該 CEK 加密的資料行的中繼資料定義。
 -   請確定您的開發電腦上已安裝 ODBC Driver for SQL Server 17 或更高版本。 如需詳細資訊，請參閱[ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。

## <a name="enabling-always-encrypted-in-a-php-application"></a>PHP 應用程式中啟用永遠加密

若要啟用的目標加密資料行及解密的查詢結果的參數加密最簡單方式是藉由設定的值`ColumnEncryption`連接字串關鍵字設`Enabled`。 SQLSRV 與 PDO_SQLSRV 驅動程式中啟用 永遠加密的範例如下：

SQLSRV:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled");
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

啟用 永遠加密不足，無法加密或解密才能成功;您也需要確定：
 -   應用程式具有 VIEW ANY COLUMN MASTER KEY DEFINITION 和 VIEW ANY COLUMN ENCRYPTION KEY DEFINITION 資料庫權限，才能存取資料庫中的永遠加密金鑰的相關中繼資料。 如需詳細資訊，請參閱[Database 權限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。
 -   應用程式可以存取保護查詢加密資料行的 Cek CMK。 這項需求會視儲存 CMK 的金鑰存放區提供者。 如需詳細資訊，請參閱[使用資料行主要金鑰存放區](#working-with-column-master-key-stores)。

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料

一旦您啟用 永遠加密的連接上，您可以使用標準 SQLSRV Api (請參閱[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)) 或 PDO_SQLSRV Api (請參閱[PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)) 擷取或修改資料在加密的資料庫資料行。 假設您的應用程式具有必要的資料庫權限，而且可以存取資料行主要金鑰，驅動程式會加密目標加密資料行和解密來自加密資料行，其運作方式會明確地為擷取資料的任何查詢參數應用程式，如同未加密的資料行。

如果未啟用永遠加密，使用參數的目標加密資料行的查詢將會失敗。 資料仍擷取從加密的資料行，只要查詢沒有任何以加密的資料行為目標的參數。 不過，驅動程式不會嘗試任何解密，而且應用程式收到二進位的加密的資料 （以位元組陣列）。

下表摘要說明查詢，根據是否啟用 永遠加密與否的行為：

|查詢特性 |永遠加密] 已啟用，而且應用程式可以存取的索引鍵和索引鍵的中繼資料 |已啟用 [永遠加密和金鑰或金鑰中繼資料，無法存取應用程式 |永遠加密已停用 | |加密的資料行為目標的參數。 |參數值會以透明的方式進行加密。 |錯誤 |錯誤 | |擷取資料自加密資料行，而不加密的資料行為目標的參數。 |從加密資料行的結果是明確地進行解密。 應用程式收到純文字資料行值。 |錯誤 |不會解密來自加密資料行的結果。 應用程式接收加密的值做為位元組陣列。 |
 
以下範例將說明擷取和修改加密資料行中的資料。 這些範例假設具有下列結構描述的資料表。 加密的 SSN 和 BirthDate 資料行。
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

下列範例會示範如何使用 SQLSRV 和 PDO_SQLSRV 驅動程式將資料列插入病患資料表。 請注意下列重點：
 -   範例程式碼中沒有任何需要加密的特定項目。 驅動程式會自動偵測並加密的 SSN 和 BirthDate 參數，目標加密資料行的值。 這個機制可讓加密透明應用程式。
 -   插入至資料庫資料行，包括加密的資料行的值會當做繫結參數傳遞。 雖然使用參數是選擇性的值傳送至非加密的資料行 （不過強烈建議因有利於防止 SQL 資料隱碼） 時，就需要加密的資料行為目標的值。 如果插入 SSN 或 BirthDate 資料行中的值傳遞做為內嵌在查詢陳述式中的常值，則查詢會失敗，因為驅動程式不會嘗試加密或處理查詢中的常值。 結果，伺服器會因與加密資料行不相容而拒絕它們。
 -   插入時使用繫結參數的值，與目標資料行的資料類型完全相同，或其轉換成目標資料行的資料類型支援的 SQL 類型必須傳遞至資料庫。 這是因為永遠加密支援一些型別轉換 (如需詳細資訊，請參閱[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md))。 兩個 PHP 驅動程式，SQLSRV 和 PDO_SQLSRV，各有一個機制，協助使用者決定值的 SQL 型別。 因此，使用者不必明確地提供的 SQL 型別。
  -   SQLSRV 驅動程式時，使用者會有兩個選項：
   -   依賴 PHP 驅動程式，來決定並設定正確的 SQL 類型。 在此情況下，使用者必須使用`sqlsrv_prepare`和`sqlsrv_execute`執行參數化的查詢。
   -   明確設定的 SQL 型別。
  -   PDO_SQLSRV 驅動程式的使用者沒有以明確地設定參數的 SQL 類型的選項。 PDO_SQLSRV 驅動程式會自動在協助使用者決定 SQL 型別時將參數繫結。
 -   若要判斷 SQL 類型的驅動程式，某些限制適用於：
  -   SQLSRV 驅動程式：
   -   如果使用者想要判斷已加密的資料行的 SQL 類型的驅動程式，則使用者必須使用`sqlsrv_prepare`和`sqlsrv_execute`。
   -   如果`sqlsrv_query`是慣用，使用者必須負責指定對所有參數的 SQL 類型。 指定的 SQL 類型必須包含字串類型的字串長度和小數位數和有效位數十進位型別。
  -   PDO_SQLSRV 驅動程式：
   -   陳述式屬性`PDO::SQLSRV_ATTR_DIRECT_QUERY`不支援參數化查詢。
   -   陳述式屬性`PDO::ATTR_EMULATE_PREPARES`不支援參數化查詢。
   
SQLSRV 驅動程式和[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md):
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

SQLSRV 驅動程式和[sqlsrv_query](../../connect/php/sqlsrv-query.md):
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

PDO_SQLSRV 驅動程式和[pdo:: prepare](../../connect/php/pdo-prepare.md):
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

下列範例會示範根據加密的值和擷取自加密資料行使用的 SQLSRV 與 PDO_SQLSRV 驅動程式的純文字資料的篩選資料。 請注意下列重點：
 -   要傳遞使用繫結參數，讓驅動程式可以以透明的方式加密它傳送到伺服器之前，先用在 WHERE 子句來篩選 SSN 資料行需要的值。
 -   執行具有繫結參數的查詢，PHP 驅動程式除非使用者明確指定的 SQL 型別使用 SQLSRV 驅動程式時，會自動判斷使用者的 SQL 類型。
 -   列印程式的所有值都會以純文字，因為驅動程式以透明的方式解密從 SSN 和 BirthDate 資料行擷取的資料。
 
注意： 只有加密是具決定性，查詢就可以加密的資料行上執行相等比較作業。 如需詳細資訊，請參閱[選取具確定性或隨機化加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

SQLSRV:
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

PDO_SQLSRV:
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

下列範例說明從加密的資料行使用的 SQLSRV 與 PDO_SQLSRV 驅動程式擷取二進位的加密的資料。 請注意下列重點：
 -   因為永遠加密的連接字串中未啟用，則查詢會傳回加密的 SSN 和 BirthDate 值做為位元組陣列 （程式會將值轉換為字串）。
 -   從加密資料行擷取資料但停用 [永遠加密] 的查詢可以有參數，只要沒有任何參數以加密資料行為目標。 下列查詢依 LastName 篩選的未加密的資料庫中。 如果依 SSN 或 BirthDate 篩選查詢，則查詢會失敗。
 
SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = sqlsrv_prepare($conn, $query, array(&$lastName));
sqlsrv_execute($stmt);
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $lastName);
$stmt->execute();
$row = $stmt->fetch();
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>避免常見的加密資料行查詢問題

本章節描述常見的錯誤類別，當查詢加密資料行，從 PHP 應用程式和如何加以避免的一些指導方針。

#### <a name="unsupported-data-type-conversion-errors"></a>不支援的資料類型轉換錯誤

[永遠加密] 支援極少數的加密資料類型轉換。 請參閱[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)支援的類型轉換詳細清單。 請執行下列作業以免發生資料型別轉換錯誤︰
 -   當使用 SQLSRV 驅動程式搭配`sqlsrv_prepare`和`sqlsrv_execute`SQL 類型，以及資料行大小和小數位數參數的數目自動決定。
 -   當使用 PDO_SQLSRV 驅動程式來執行查詢時，也會自動決定 SQL 類型與資料行大小和小數位數參數的數目
 -   當使用 SQLSRV 驅動程式搭配`sqlsrv_query`執行查詢：
  -   參數的 SQL 型別也可以完全相同的目標資料行中，類型或支援從 SQL 類型轉換成資料行的類型。
  -   有效位數和小數位數的資料行為目標的參數`decimal`和`numeric`SQL Server 資料類型為相同的有效位數和小數位數設定為目標資料行。
  -   參數為目標的資料行的有效位數`datetime2`， `datetimeoffset`，或`time`SQL Server 資料類型不是大於目標資料行，修改目標資料行的查詢中的有效位數。
 -   請勿使用 PDO_SQLSRV 陳述式屬性`PDO::SQLSRV_ATTR_DIRECT_QUERY`或`PDO::ATTR_EMULATE_PREPARES`中參數化查詢
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳送純文字，而不是傳送加密值所造成的錯誤。

任何目標加密資料行的值必須加密再傳送至伺服器。 嘗試插入、 修改或篩選在導致錯誤加密的資料行上以純文字值。 若要避免這類錯誤，請確認：
 -   永遠加密 已啟用 (在連接字串中，設定`ColumnEncryption`關鍵字`Enabled`)。
 -   您可以使用繫結參數來傳送加密的資料行為目標的資料。 下列範例會示範加密資料行 (SSN) 常值/常數錯誤篩選的查詢：
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>控制永遠加密的影響效能

因為永遠加密 」 是用戶端加密技術，大部分的效能負擔是在用戶端，不是在資料庫觀察到。 除了加密和解密作業成本，效能負擔的用戶端的其他來源如下：
 -   資料庫以擷取查詢參數的中繼資料的額外往返。
 -   呼叫資料行主要金鑰存放區以存取資料行主要金鑰。
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>反覆存取以擷取中繼資料的查詢參數

如果連接啟用一律加密時，ODBC 驅動程式會根據預設，呼叫[sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)每個參數化查詢，將查詢陳述式 （不含任何參數值） 傳遞至 SQL Server. 這個預存程序會分析查詢陳述式，以找出，如果任何參數需要加密，而且如果是，傳回每個參數，以允許驅動程式才能將其加密的加密相關資訊。

由於 PHP 驅動程式可讓使用者將參數繫結已備妥的陳述式，而不需提供 SQL 中輸入，PHP 驅動程式時將參數繫結中啟用 永遠加密的連接，呼叫[SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md)上參數，以取得 SQL 型別、 資料行大小和小數位數。 中繼資料會接著用來呼叫[SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md)。 這些額外`SQLDescribeParam`呼叫因為不需要額外反覆存取資料庫 ODBC 驅動程式已有在用戶端上儲存資訊時`sys.sp_describe_parameter_encryption`呼叫。

上述行為可確保高透明度，用戶端應用程式 （及應用程式開發人員） 的層級不需要留意哪些查詢存取加密資料行，只要以加密的資料行為目標的值會傳遞至驅動程式參數。

不同於適用於 SQL Server ODBC 驅動程式，在陳述式/查詢層級中啟用 永遠加密尚未支援的 PHP 驅動程式中。 

### <a name="column-encryption-key-caching"></a>快取的資料行加密金鑰

若要減少資料行主要金鑰存放區來解密資料行加密金鑰 (CEK) 的呼叫次數，此驅動程式會快取在記憶體中的純文字 Cek。 從資料庫中繼資料中接收加密 CEK (ECEK) 之後, 的 ODBC 驅動程式會先嘗試尋找的純文字 CEK 值對應的加密金鑰快取中。 驅動程式會呼叫金鑰存放區包含 CMK，只有當快取中找不到對應的純文字 CEK。

注意： 在 SQL server ODBC 驅動程式，快取中的項目會收回兩小時逾時後。 這個行為表示給定 ECEK，為驅動程式的應用程式或每隔兩小時的存留期間會連絡一次金鑰存放區、 少者為準。

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區

若要加密或解密資料，驅動程式必須取得 CEK 目標資料行的設定。 Cek 會儲存在資料庫中繼資料中的加密形式 (ECEKs)。 每個 CEK 都有對應的 CMK 用來加密它。 [資料庫中繼資料](../../t-sql/statements/create-column-master-key-transact-sql.md)不會儲存 CMK 本身; 它只包含金鑰存放區和金鑰存放區可以用來找出 CMK 資訊的名稱。

若要取得的 ECEK 純文字值，驅動程式會先取得有關其對應的 CMK 和 CEK 的中繼資料，然後使用此資訊來連絡包含 CMK 的金鑰存放區，並要求它解密 ECEK。 驅動程式會使用金鑰存放區提供者的金鑰存放區與通訊。

Microsoft driver 5.2.0 for PHP for SQL Server，只有 Windows 憑證存放區提供者支援。 尚不支援兩個其他金鑰存放區提供者支援的 ODBC 驅動程式 （Azure 金鑰保存庫及自訂金鑰存放區提供者）。

### <a name="using-the-windows-certificate-store-provider"></a>使用 Windows 憑證存放區提供者

ODBC Driver for SQL Server on Windows 包含內建的資料行主要金鑰存放區提供者的 Windows 憑證存放區，名為`MSSQL_CERTIFICATE_STORE`。 （此提供者並不適用於 macOS 或 Linux）。與此提供者，CMK 儲存在本機用戶端電腦上，且不需要額外的組態，應用程式所使用的驅動程式所需。 不過，應用程式必須存取憑證和私密金鑰存放區中。 如需詳細資訊，請參閱 [建立及儲存資料行主要金鑰 (永遠加密)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>使用永遠加密時的 PHP 驅動程式的限制

SQLSRV 和 PDO_SQLSRV:
 -   Linux/MacOS 支援
  -   Linux/MacOS 不支援 Windows 憑證存放區提供者，也就是唯一的金鑰存放區提供者目前支援的 PHP 驅動程式
 -   強制加密參數
 -   啟用 永遠加密陳述式層級 
 
只有 SQLSRV:
 -   使用`sqlsrv_query`繫結參數，但未指定的 SQL 型別
 -   使用`sqlsrv_prepare`來繫結 SQL 陳述式的批次中的參數  
 
只有 PDO_SQLSRV:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` 參數化查詢中指定的陳述式屬性
 -   `PDO::ATTR_EMULATE_PREPARE` 參數化查詢中指定的陳述式屬性
 -   繫結 SQL 陳述式的批次中的參數
 
PHP 驅動程式也會繼承 SQL Server 和資料庫的 ODBC 驅動程式所加諸的限制。 請參閱[的 ODBC 驅動程式使用永遠加密時的限制](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)和[一律加密功能詳細資料](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details)。  
  
## <a name="see-also"></a>另請參閱  
[PHP SQL 驅動程式程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
