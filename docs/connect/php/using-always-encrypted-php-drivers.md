---
title: 搭配 PHP Drivers for SQL Server 使用 Always Encrypted | Microsoft Docs
ms.date: 01/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.openlocfilehash: 5c82c32922712b377fd732b6745b1761e9f32a82
ms.sourcegitcommit: afc0c3e46a5fec6759fe3616e2d4ba10196c06d1
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2019
ms.locfileid: "55889999"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>搭配 PHP Drivers for SQL Server 使用 Always Encrypted
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>適用於
 -   Microsoft Drivers 5.2 for PHP for SQL Server
 
## <a name="introduction"></a>簡介

本文章提供有關如何開發 PHP 應用程式使用的資訊[Always Encrypted （資料庫引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)並[PHP Driver for SQL Server](../../connect/php/Microsoft-php-driver-for-sql-server.md)。

[永遠加密] 可讓用戶端應用程式加密敏感性資料，且永遠不會顯示資料或 SQL Server 或 Azure SQL Database 的加密金鑰。 ODBC Driver for SQL Server 等已啟用 Always Encrypted 的驅動程式，以清晰簡明的方式加密與解密用戶端應用程式中的敏感性資料。 驅動程式會自動判斷哪一個查詢參數對應至敏感性資料庫資料行 (使用 [永遠加密] 保護)，然後加密這些參數值後再將資料傳遞至 SQL Server 或 Azure SQL Database。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 如需詳細資訊，請參閱 [一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 PHP Driver for SQL Server 使用 ODBC Driver for SQL Server 加密機密資料。

## <a name="prerequisites"></a>Prerequisites

 -   在資料庫中設定永遠加密。 此設定需要佈建 Always Encrypted 金鑰，並為選取的資料庫資料行設定加密。 如果您的資料庫尚未設定 [永遠加密]，請遵循 [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(永遠加密快速入門) 中的指示操作。 特別是，您的資料庫應該包含資料行主要金鑰 (CMK)、 資料行加密金鑰 (CEK) 和資料表，其中包含一或多個使用該 CEK 加密的資料行的中繼資料定義。
 -   請確定您的開發電腦上已安裝的 ODBC Driver for SQL Server 17 或更高的版本。 如需詳細資訊，請參閱 < [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。

## <a name="enabling-always-encrypted-in-a-php-application"></a>啟用 永遠加密中的 PHP 應用程式

若要對以加密資料行為目標的參數進行加密，以及對查詢結果進行解密，最簡單的方式是將 `ColumnEncryption`連接字串關鍵字的值設定為 `Enabled`。 SQLSRV 和 PDO_SQLSRV 驅動程式中啟用 永遠加密的範例如下︰

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

啟用 永遠加密不足，無法加密或解密成功;您也需要確定：
 -   應用程式要有 [檢視任何資料行的主要金鑰定義] 和 [檢視任何資料行的加密金鑰定義] 資料庫權限，才能存取資料庫中 Always Encrypted 金鑰的相關中繼資料。 如需詳細資訊，請參閱 <<c0> [ 資料庫的權限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。
 -   應用程式可以存取保護查詢加密資料行的 Cek CMK。 這項需求是依據儲存 CMK 的金鑰存放區提供者。 如需詳細資訊，請參閱 <<c0> [ 使用 資料行主要金鑰存放區](#working-with-column-master-key-stores)。

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料

一旦您啟用 「 一律加密的連接上，您可以使用標準 SQLSRV Api (請參閱[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)) 或 PDO_SQLSRV Api (請參閱[PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)) 來擷取或修改資料在加密的資料庫資料行。 假設您的應用程式具有必要的資料庫權限，而且可以存取資料行主要金鑰，驅動程式會加密任何查詢參數的目標加密資料行，以及解密擷取自加密資料行，以透明的方式為其運作方式的資料應用程式，如同未加密的資料行。

如未啟用 Always Encrypted，使用以加密資料行為目標的參數查詢就會失敗。 只要查詢沒有以加密資料行為目標的參數，就仍然可以從加密資料行擷取資料。 不過，此驅動程式不會嘗試任何解密，而且應用程式收到二進位的加密的資料 （以位元組陣列）。

下表摘要說明查詢的行為，視 Always Encrypted 是否啟用而定：

|查詢特性|[永遠加密] 已啟用，且應用程式可以存取金鑰和金鑰中繼資料|[永遠加密] 已啟用，但應用程式不能存取金鑰或金鑰中繼資料|[永遠加密] 已停用|
|---|---|---|---|
|以加密的資料行為目標的參數。|以清晰簡明的方式加密參數值。|錯誤|錯誤|
|從加密的資料行擷取資料，沒有任何以加密資料行為目標的參數。|以清晰簡明的方式解密來自加密資料行的結果。 應用程式收到純文字資料行的值。 |錯誤|不解密來自加密資料行的結果。 應用程式收到位元組陣列形態的加密值。|
 
以下範例將說明擷取和修改加密資料行中的資料。 此範例假設具有下列結構描述的資料表。 SSN 和 BirthDate 資料行均已加密。
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

下列範例示範如何使用 SQLSRV 和 PDO_SQLSRV 驅動程式將資料列插入病患資料表。 請注意下列幾點：
 -   範例程式碼中沒有任何需要加密的特定項目。 驅動程式會自動偵測並加密的 SSN 和 BirthDate 參數，其目標為加密的資料行的值。 此機制讓加密對應用程式變得透明化。
 -   插入至資料庫資料行的值，包括加密的資料行，會傳遞為繫結參數。 雖然將值傳送到未加密的資料行時，使用參數是選擇性項目 (還是強烈建議使用，因有利於防止 SQL 插入式攻擊)，但它對以加密資料行為目標的值卻是必要項目。 如果插入 SSN 或 BirthDate 資料行中的值傳遞做為內嵌在查詢陳述式中的常值，則查詢會失敗，因為驅動程式不會嘗試加密，或處理查詢中的常值。 結果，伺服器會因與加密資料行不相容而拒絕它們。
 -   插入時使用繫結參數的值，與目標資料行的資料型別完全相同，或其轉換成目標資料行的資料類型支援的 SQL 類型必須傳遞至資料庫。 此需求是因為 Always Encrypted 支援一些型別轉換 (如需詳細資訊，請參閱 < [Always Encrypted （資料庫引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md))。 兩個 PHP drivers SQLSRV 和 PDO_SQLSRV，每個都有一個機制來協助使用者決定值的 SQL 類型。 因此，使用者不必明確提供的 SQL 型別。
  -   SQLSRV 驅動程式時，使用者會有兩個選項：
   -   如果需要依賴的 PHP 驅動程式，以判斷及設定正確的 SQL 類型。 在此情況下，使用者必須使用`sqlsrv_prepare`和`sqlsrv_execute`執行參數化的查詢。
   -   明確設定的 SQL 型別。
  -   PDO_SQLSRV 驅動程式，使用者並沒有明確設定參數的 SQL 類型的選項。 PDO_SQLSRV 驅動程式會自動可協助使用者決定 SQL 型別，繫結參數時。
 -   Typ dotazu SQL 驅動程式，某些限制適用於：
  -   SQLSRV 驅動程式：
   -   如果使用者想要判斷已加密的資料行的 SQL 類型的驅動程式，則使用者必須使用`sqlsrv_prepare`和`sqlsrv_execute`。
   -   如果`sqlsrv_query`是偏好選項，使用者會負責指定所有參數的 SQL 類型。 字串類型的字串長度和小數位數和有效位數 decimal 類型，必須包含指定的 SQL 型別。
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

下列範例會示範根據加密的值，以及擷取純文字資料，從使用 SQLSRV 和 PDO_SQLSRV 驅動程式的加密資料行篩選資料。 請注意下列幾點：
 -   在 WHERE 子句中用來篩選 SSN 資料行的值，需要使用繫結參數傳遞，如此驅動程式可以清晰簡明的方式加密它，再將它傳送至伺服器。
 -   執行具有繫結參數的查詢，PHP 驅動程式除非使用者明確指定的 SQL 型別，使用 SQLSRV 驅動程式時，會自動判斷使用者的 SQL 類型。
 -   程式列印的所有值都是純文字格式，因為驅動程式會以清晰簡明方式來解密從 SSN 和 BirthDate 資料行擷取的資料。
 
注意：查詢可以加密資料行上執行相等比較，只有具決定性加密。 如需詳細資訊，請參閱[選取確定性或隨機化加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

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

### <a name="ciphertext-data-retrieval-example"></a>密碼文字資料擷取範例

如未啟用 [永遠加密]，只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。

下列範例說明從使用 SQLSRV 和 PDO_SQLSRV 驅動程式的加密資料行擷取二進位的加密的資料。 請注意下列幾點：
 -   因為連接字串未啟用 Always Encrypted，所以查詢會以位元組陣列 (程式會將值轉換為字串) 傳回加密的 SSN 和 BirthDate 值。
 -   從加密資料行擷取資料但停用 [永遠加密] 的查詢可以有參數，只要沒有任何參數以加密資料行為目標。 下列查詢依 LastName 篩選，在資料庫中未加密。 如果依 SSN 或 BirthDate 篩選查詢，查詢會失敗。
 
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

本節說明從 PHP 應用程式查詢加密資料行時常見的錯誤類別，以及如何避免的一些方針。

#### <a name="unsupported-data-type-conversion-errors"></a>不支援的資料類型轉換錯誤

[永遠加密] 支援極少數的加密資料類型轉換。 如需支援的類型轉換詳細清單，請參閱 [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 請執行下列作業以免發生資料型別轉換錯誤︰
 -   當使用 SQLSRV 驅動程式與`sqlsrv_prepare`和`sqlsrv_execute`SQL 類型，以及資料行大小和小數位數的參數數目自動決定。
 -   當使用 PDO_SQLSRV 驅動程式來執行查詢時，也會自動決定資料行大小和數目的小數位數參數的 SQL 型別
 -   當使用 SQLSRV 驅動程式與`sqlsrv_query`執行查詢：
  -   參數的 SQL 型別正是可以做為目標的資料行的類型相同，或支援從 SQL 類型轉換成資料行的類型。
  -   以 `decimal` 和 `numeric` SQL Server 資料類型資料行為目標之參數的有效位數和小數位數，和為目標資料行設定的有效位數和小數位數相同。
  -   在修改目標資料行的查詢中，以 `datetime2`、`datetimeoffset` 或 `time` SQL Server 資料類型資料行為目標之參數的有效位數，不大於目標資料行的有效位數。
 -   請勿使用 PDO_SQLSRV 陳述式屬性`PDO::SQLSRV_ATTR_DIRECT_QUERY`或`PDO::ATTR_EMULATE_PREPARES`中參數化查詢
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳送純文字，而不是傳送加密值所造成的錯誤。

目標加密資料行的任何值，就需要加密再傳送至伺服器。 嘗試對加密資料行插入、修改或以純文字值進行篩選時，會導致發生錯誤。 若要避免這類錯誤，請確定：
 -   已啟用 永遠加密 (在連接字串中，設定`ColumnEncryption`關鍵字來`Enabled`)。
 -   您可以使用繫結參數傳送以加密資料行為目標的資料。 下列範例會示範加密資料行 (SSN) 以常值/常數錯誤篩選的查詢：
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>控制永遠加密的影響效能

因為 Always Encrypted 是用戶端加密技術，大部分的效能額外負荷是在用戶端觀察到，不是在資料庫觀察到。 除了加密和解密作業成本之外，用戶端其他的效能額外負荷來源如下：
 -   額外反覆存取資料庫以擷取查詢參數的中繼資料。
 -   呼叫資料行主要金鑰存放區以存取資料行主要金鑰。
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>反覆存取以擷取查詢參數的中繼資料

如果連接已啟用 Always Encrypted，ODBC 驅動程式預設會針對每個參數化查詢呼叫 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)，將查詢陳述式 (不含任何參數值) 傳遞至 SQL Server。 這個預存程序會分析查詢陳述式，若要了解，如果任何參數需要加密，而且如果是的話，傳回每個參數，以允許將其加密驅動程式的加密相關資訊。

由於的 PHP 驅動程式可讓使用者將參數繫結在備妥的陳述式，而不需提供 SQL 輸入，PHP 驅動程式時將參數繫結中啟用 永遠加密的連接，呼叫[SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md)上若要取得 SQL 型別、 資料行大小和小數位數的參數。 中繼資料則用來呼叫[SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md)。 這些額外`SQLDescribeParam`呼叫因為不需要額外的往返通訊資料庫 ODBC 驅動程式已有儲存在用戶端的資訊時`sys.sp_describe_parameter_encryption`呼叫。

上述行為可確保較高的用戶端應用程式 （以及應用程式開發人員） 的透明度層級不需要留意哪些查詢存取加密的資料行，只要以加密的資料行為目標的值會傳遞至驅動程式參數。

不同於適用於 SQL Server ODBC 驅動程式，在陳述式/查詢層級中啟用 永遠加密尚未支援 PHP 驅動程式中。 

### <a name="column-encryption-key-caching"></a>資料行加密金鑰快取

若要減少資料行主要金鑰存放區來解密資料行加密金鑰 (CEK) 的呼叫數目，此驅動程式會快取在記憶體中的純文字 Cek。 從資料庫中繼資料中接收加密的 CEK (ECEK) 之後, 的 ODBC 驅動程式會先嘗試尋找純文字 CEK 值對應的加密金鑰快取中。 驅動程式會呼叫包含 CMK，只有當快取中找不到對應的純文字 CEK 的金鑰存放區。

注意：ODBC Driver for SQL Server，在兩小時逾時之後收回快取中的項目。 這個行為表示，針對給定的 ECEK，驅動程式會連絡一次金鑰存放區的應用程式或每隔兩小時的存留期間，兩者中較少。

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區

若要加密或解密資料，驅動程式需要取得已針對目標資料行的 CEK。 Cek 會儲存在資料庫中繼資料中的加密形式 (ECEKs)。 每個 CEK 有相對應的 CMK 用來加密。 [資料庫中繼資料](../../t-sql/statements/create-column-master-key-transact-sql.md)不會儲存 CMK 本身; 它只包含名稱的金鑰存放區和金鑰存放區可用來尋找 CMK 的資訊。

若要取得 ECEK 的純文字值，此驅動程式會先取得其相對應的 CMK 和 CEK 的相關中繼資料，然後使用此資訊來連絡包含 CMK 的金鑰存放區，並要求它來解密的 ECEK。 驅動程式會使用金鑰存放區提供者的金鑰存放區與通訊。

Microsoft driver 5.3.0 for PHP for SQL Server，只有 「 Windows 憑證存放區提供者 」 和 「 Azure 金鑰保存庫支援。 不支援 ODBC 驅動程式 （自訂金鑰存放區提供者） 所支援其他金鑰儲存區提供者。

### <a name="using-the-windows-certificate-store-provider"></a>使用 Windows 憑證存放區提供者

Windows 上的 SQL Server ODBC 驅動程式包含內建的資料行主要金鑰存放區提供者的 Windows 憑證存放區、 名為`MSSQL_CERTIFICATE_STORE`。 （此提供者無法使用。 在 macOS 或 Linux）與此提供者，CMK 會儲存在本機用戶端電腦上，並由應用程式不需要額外組態，才能使用它來搭配此驅動程式。 不過，應用程式必須存取憑證和私密金鑰存放區中。 如需詳細資訊，請參閱 [建立及儲存資料行主要金鑰 (永遠加密)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

### <a name="using-azure-key-vault"></a>使用 Azure Key Vault

Azure 金鑰保存庫會提供方法來儲存加密金鑰、 密碼和其他祕密，使用 Azure，而且可用來儲存 Always encrypted 的金鑰。 ODBC Driver for SQL Server （17 和更高版本） 包含 Azure Key Vault 的內建的主要金鑰存放區提供者。 下列連接選項處理 Azure Key Vault 設定： `KeyStoreAuthentication`， `KeyStorePrincipalId`，和`KeyStoreSecret`。 
 -   `KeyStoreAuthentication` 可以採用兩個可能的字串值的其中一個：`KeyVaultPassword`和`KeyVaultClientSecret`。 這些值會控制與其他兩個關鍵字搭配使用何種驗證認證。
 -   `KeyStorePrincipalId` 接受字串，表示想要存取 Azure Key Vault 的帳戶識別碼。 
     -   如果`KeyStoreAuthentication`設定為`KeyVaultPassword`，然後`KeyStorePrincipalId`必須是 Azure active Directory 使用者的名稱。
     -   如果`KeyStoreAuthentication`設定為`KeyVaultClientSecret`，然後`KeyStorePrincipalId`必須是應用程式用戶端識別碼。
 -   `KeyStoreSecret` 接受字串，表示認證的密碼。 
     -   如果`KeyStoreAuthentication`設定為`KeyVaultPassword`，然後`KeyStoreSecret`必須是使用者的密碼。 
     -   如果`KeyStoreAuthentication`設定為`KeyVaultClientSecret`，然後`KeyStoreSecret`必須與應用程式的用戶端識別碼。 相關聯的應用程式祕密

所有的三個選項中必須要有連接字串以使用 Azure Key Vault。 颾魤 ㄛ`ColumnEncryption`必須設為`Enabled`。 如果`ColumnEncryption`設為`Disabled`但 Azure 金鑰保存庫選項有，指令碼會繼續執行，而且未發生錯誤但未加密將會執行。

下列範例會示範如何連接到 SQL Server 使用 Azure Key Vault。

SQLSRV:

使用 Azure Active Directory 帳戶：
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultPassword", "KeyStorePrincipalId"=>$AADUsername, "KeyStoreSecret"=>$AADPassword);
$conn = sqlsrv_connect($server, $connectionInfo);
```
使用 Azure 應用程式用戶端識別碼和祕密：
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultClientSecret", "KeyStorePrincipalId"=>$applicationClientID, "KeyStoreSecret"=>$applicationClientSecret);
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:使用 Azure Active Directory 帳戶：
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultPassword; KeyStorePrincipalId = $AADUsername; KeyStoreSecret = $AADPassword;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```
使用 Azure 應用程式用戶端識別碼和祕密：
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultClientSecret; KeyStorePrincipalId = $applicationClientID; KeyStoreSecret = $applicationClientSecret;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>使用永遠加密時的 PHP 驅動程式的限制

SQLSRV 和 PDO_SQLSRV:
 -   Linux/macOS 不支援 Windows 憑證存放區提供者
 -   強制參數加密
 -   啟用 永遠加密陳述式層級 
 -   當使用 Always Encrypted 功能和非 UTF8 地區設定 Linux 和 macOS （例如"en_US。ISO-8859-1")，除非您的系統上已安裝字碼頁 1252年插入加密的 char （n） 資料行中的資料為 null 或空字串可能無法運作
 
SQLSRV 只有：
 -   使用`sqlsrv_query`繫結參數，但未指定的 SQL 類型
 -   使用`sqlsrv_prepare`的繫結 SQL 陳述式的批次中的參數  
 
只有 PDO_SQLSRV:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` 參數化查詢中指定的陳述式屬性
 -   `PDO::ATTR_EMULATE_PREPARE` 參數化查詢中指定的陳述式屬性
 -   繫結 SQL 陳述式的批次中的參數
 
PHP 驅動程式也會繼承 ODBC Driver for SQL Server 和資料庫加諸的限制。 請參閱[限制的 ODBC 驅動程式時使用 Always Encrypted](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)並[一律加密功能詳細資料](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details)。  
  
## <a name="see-also"></a>另請參閱  
[PHP SQL 驅動程式程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 驅動程式 API 參考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
