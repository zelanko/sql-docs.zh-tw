---
title: 搭配 PHP Drivers 且具有安全記憶體保護區的 Always Encrypted
description: 了解如何搭配 Microsoft Drivers for PHP for SQL Server 使用具有安全記憶體保護區的 Always Encrypted。
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: ''
ms.author: v-daenge
author: David-Engel
ms.openlocfilehash: f407cae7fe7d53a7522e64f0bb26961ebeb4276f
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632088"
---
# <a name="using-always-encrypted-with-secure-enclaves-with-the-php-drivers-for-sql-server"></a>搭配 PHP Drivers for SQL Server 使用具有安全記憶體保護區的 Always Encrypted
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>適用於
 -   Microsoft Drivers 5.8.0 for PHP for SQL Server
 
## <a name="introduction"></a>簡介

[具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) 是適用於 SQL Server 之 Always Encrypted 功能的第二個反覆項目。 具有安全記憶體保護區的 Always Encrypted 可讓使用者透過建立安全記憶體保護區來針對加密資料執行豐富的計算；安全記憶體保護區是伺服器上記憶體的一部分區域，系統會在其中將資料庫中的加密資料解密以便執行計算。 支援的作業包含搭配 `LIKE` 子句進行比較和模式比對。

## <a name="enabling-always-encrypted-with-secure-enclaves"></a>啟用具有安全記憶體保護區的 Always Encrypted

從 PHP Drivers for SQL Server 5.8.0 版開始，便支援具有安全記憶體保護區的 Always Encrypted。 具有安全記憶體保護區的 Always Encrypted 需要 SQL Server 2019 或更新版本，以及 ODBC 驅動程式 17.4 版及更新版本。 [這裡](using-always-encrypted-php-drivers.md)提供搭配 PHP Drivers for SQL Server 使用 Always Encrypted 之一般需求的詳細資料。

具有安全記憶體保護區的 Always Encrypted 能透過對記憶體保護區進行證明來確保加密資料的安全性，也就是針對外部證明服務驗證記憶體保護區。 若要使用安全記憶體保護區，`ColumnEncryption` 關鍵字必須識別證明類型及通訊協定，以及相關聯的證明資料 (以逗號分隔)。 ODBC 驅動程式的 17.4 版針對記憶體保護區類型及通訊協定，僅支援虛擬化型安全性 (VBS) 及主機守護者服務 (HGS) 通訊協定。 相關聯的證明資料是證明伺服器的 URL。 因此，會將下列項目新增至連接字串：

```
ColumnEncryption=VBS-HGS,http://attestationserver.mydomain/Attestation
```
如果通訊協定不正確，驅動程式將無法加以辨識，連線將會失敗，並傳回錯誤。 如果只有證明 URL 是不正確的，連線將會成功，但會在嘗試進行啟用記憶體保護區的計算時擲回錯誤，不過其餘行為將會與原始的 Always Encrypted 行為相同。 將 `ColumnEncryption` 設定為 `enabled` 將會提供一般 Always Encrypted 功能，但嘗試進行啟用記憶體保護區的作業將會傳回錯誤。

設定環境以支援具有安全記憶體保護區的 Always Encrypted 的完整詳細資料，包括設定主機守護者服務並建立必要的加密金鑰，可以在[這裡](../../relational-databases/security/encryption/configure-always-encrypted-enclaves.md)找到。

## <a name="examples"></a>範例

下列兩個範例 (分別適用於 SQLSRV 和 PDO_SQLSRV) 會搭配數個純文字的資料類型建立資料表，然後在加以加密之後進行比較和模式比對。 請注意：

- 搭配 `ALTER TABLE` 對資料表進行加密時，每次呼叫 `ALTER TABLE` 時只能對單一資料行進行加密，因此需要進行多次呼叫才能將多個資料行加密。
- 以參數形式傳遞比較閾值來比較 char 和 nchar 類型時，必須在對應的 `SQLSRV_SQLTYPE_*` 中指定資料行寬度，否則將會傳回 `HY104`、`Invalid precision value`錯誤。
- 針對模式比對，必須使用 `COLLATE` 子句將定序指定為 `Latin1_General_BIN2`。
- 以參數形式傳遞模式比對字串來比對 char 和 nchar 類型時，傳遞至 `sqlsrv_query` 或 `sqlsrv_prepare` 的 `SQLSRV_SQLTYPE_*` 應該指定要比對的字串長度，而非資料行的大小，因為 char 和 nchar 類型會在字串結尾處填補空格。 例如，針對 char(10) 資料行比對字串 `%abc%` 時，請指定 `SQLSRV_SQLTYPE_CHAR(5)`。 如果您改為指定 `SQLSRV_SQLTYPE_CHAR(10)`，查詢將會比對 `%abc%     ` (具有附加的五個空格)，而資料行中具有少於五個附加空格的任何資料都不會相符 (因此 `abcdef` 將不會符合 `%abc%`，因為其具有四個空格的填補)。 針對 Unicode 字串，請使用 `mb_strlen` 或 `iconv_strlen` 函式來取得字元數目。
- PDO 介面不允許指定參數的長度。 相反地，請指定 0 的長度，或在 `PDOStatement::bindParam` 中指定 `null`。 如果長度已明確設定為另一個數字，系統會將參數視為輸出參數。
- 在 Always Encrypted 中，模式比對無法針對非字串類型運作。
- 為了清楚起見，已排除錯誤檢查。 

以下是這兩個範例的常見資料：
```php
<?php
// Data for testing - integer, datetime2, char, nchar, varchar, and nvarchar
// String data is random, showing that we can match or compare anything
$testValues = array(array(1, "2019-12-31 01:00:00", "abcd", "㬚㔈♠既", "abcd", "㬚㔈♠既"),
                    array(-100, "1753-01-31 14:25:25.25", "#e@?q&zy+", "ઔܛ᎓Ե⅜", "#e@?q&zy+", "ઔܛ᎓Ե⅜"),
                    array(100, "2112-03-15 23:40:10.1594", "zyxwv", "㶋㘚ᐋꗡ", "zyxwv", "㶋㘚ᐋꗡ"),
                    array(0, "8888-08-08 08:08:08.08", "7t", "㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ", "7t", "㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ"),
                    );

// Queries to create the table and insert data
$createTable = "DROP TABLE IF EXISTS $myTable; 
                CREATE TABLE $myTable (c_integer int NULL, 
                                       c_datetime2 datetime2(7) NULL, 
                                       c_char char(32) NULL, 
                                       c_nchar nchar(32) NULL, 
                                       c_varchar varchar(32) NULL, 
                                       c_nvarchar nvarchar(32) NULL);";
$insertData = "INSERT INTO $myTable (c_integer, c_datetime2, c_char, c_nchar, c_varchar, c_nvarchar) VALUES (?, ?, ?, ?, ?, ?)";

// This is the query that encrypts the table in place
$encryptQuery = " ALTER TABLE $myTable
                      ALTER COLUMN [c_integer] integer
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER TABLE $myTable
                      ALTER COLUMN [c_datetime2] datetime2(7)
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER TABLE $myTable
                      ALTER COLUMN [c_char] char(32) COLLATE Latin1_General_BIN2
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER TABLE $myTable
                      ALTER COLUMN [c_nchar] nchar(32) COLLATE Latin1_General_BIN2
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER TABLE $myTable
                      ALTER COLUMN [c_varchar] varchar(32) COLLATE Latin1_General_BIN2
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER TABLE $myTable
                      ALTER COLUMN [c_nvarchar] nvarchar(32) COLLATE Latin1_General_BIN2
                      ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK-enclave], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
                      WITH (ONLINE = ON);
                  ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;";
?>
```
### <a name="sqlsrv"></a>SQLSRV
```php
<?php
// Specify Azure Key Vault credentials using the KeyStoreAuthentication, KeyStorePrincipalId, and KeyStoreSecret keywords
// Otherwise, the local Windows Certificate Store will be used
$options = array('database'=>$myDatabase,
                 'uid'=>$myUsername,
                 'pwd'=>$myPassword,
                 'CharacterSet'=>'UTF-8',
                 'ReturnDatesAsStrings'=>true,
                 'ColumnEncryption'=>"VBS-HGS,http://myattestationserver.mydomain/Attestation",
                 );
                 
$conn = sqlsrv_connect($myServer, $options);

// Create the table and insert the test data
$stmt = sqlsrv_query($conn, $createTable);

foreach ($testValues as $values) {
    $stmt = sqlsrv_prepare($conn, $insertData, $values);
    sqlsrv_execute($stmt);
}

// Encrypt the table in place
$stmt = sqlsrv_query($conn, $encryptQuery);

// Test comparison and pattern matching on the encrypted table
echo "Test comparisons:\n";

$intThreshold = 0;
$testGreater = "SELECT c_integer FROM $myTable WHERE c_integer > ?";
$param = array($intThreshold, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_INT);
$stmt = sqlsrv_prepare($conn, $testGreater, array($param));
getResults($stmt);
// Expect:
// 1
// 100

$datetimeThreshold = "3000-01-01 00:00:00.0";
$testLess = "SELECT c_datetime2 FROM $myTable WHERE c_datetime2 < ?";
$param = array($datetimeThreshold, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_DATETIME2);
$stmt = sqlsrv_prepare($conn, $testLess, array($param));
getResults($stmt);
// Expect:
// 2019-12-31 01:00:00.0000000
// 1753-01-31 14:25:25.2500000
// 2112-03-15 23:40:10.1594000

$charThreshold = "abcd";
$ncharThreshold = "㬚㔈♠既";

$testGreaterEqual = "SELECT c_char FROM $myTable WHERE c_char >= ?";
$param = array($charThreshold, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_CHAR(32));
$stmt = sqlsrv_prepare($conn, $testGreaterEqual, array($param));
getResults($stmt);
// Expect:
// abcd                            
// zyxwv                           

$testLessEqual = "SELECT c_nchar FROM $myTable WHERE c_nchar <= ?";
$param = array($ncharThreshold, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING('UTF-8'), SQLSRV_SQLTYPE_NCHAR(32));
$stmt = sqlsrv_prepare($conn, $testLessEqual, array($param));
getResults($stmt);
// Expect:
// 㬚㔈♠既                            
// ઔܛ᎓Ե⅜                           
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    

$testNotGreater = "SELECT c_varchar FROM $myTable WHERE c_varchar !> ?";
$param = array($charThreshold, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_VARCHAR);
$stmt = sqlsrv_prepare($conn, $testNotGreater, array($param));
getResults($stmt);
// Expect:
// abcd
// #e@?q&zy+
// 7t

$testNotLess = "SELECT c_nvarchar FROM $myTable WHERE c_nvarchar !< ?";
$param = array($ncharThreshold, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING('UTF-8'), SQLSRV_SQLTYPE_NVARCHAR);
$stmt = sqlsrv_prepare($conn, $testNotLess, array($param));
getResults($stmt);
// Expect:
// 㬚㔈♠既
// 㶋㘚ᐋꗡ

echo "\nTest pattern matching:\n";

$charMatch = "%zy%";
$ncharMatch = "%㔈♠既%";

$param = array($charMatch, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_CHAR(strlen($charMatch)));
$testCharMatch = "SELECT c_char FROM $myTable WHERE c_char LIKE ? COLLATE Latin1_General_BIN2";
$stmt = sqlsrv_prepare($conn, $testCharMatch, array($param));
getResults($stmt);
// Expect:
// #e@?q&zy+                       
// zyxwv                           

$param = array($ncharMatch, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING("UTF-8"), SQLSRV_SQLTYPE_NCHAR(iconv_strlen($ncharMatch)));
$testNCharMatch = "SELECT c_nchar FROM $myTable WHERE c_nchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = sqlsrv_prepare($conn, $testNCharMatch, array($param));
getResults($stmt);
// Expect:
// 㬚㔈♠既                            
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    

$param = array($charMatch, SQLSRV_PARAM_IN, null, SQLSRV_SQLTYPE_VARCHAR(strlen($charMatch)));
$testVarcharMatch = "SELECT c_varchar FROM $myTable WHERE c_varchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = sqlsrv_prepare($conn, $testVarcharMatch, array($param));
getResults($stmt);
// Expect:
// #e@?q&zy+
// zyxwv

$param = array($ncharMatch, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING("UTF-8"), SQLSRV_SQLTYPE_NVARCHAR(iconv_strlen($ncharMatch)));
$testNVarcharMatch = "SELECT c_nvarchar FROM $myTable WHERE c_nvarchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = sqlsrv_prepare($conn, $testNVarcharMatch, array($param));
getResults($stmt);
// Expect:
// 㬚㔈♠既
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ

function getResults($stmt)
{
    sqlsrv_execute($stmt);
    while ($res = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_NUMERIC)) {
        print_r($res[0]);
        echo "\n";
    }
}
?>
```

### <a name="pdo_sqlsrv"></a>PDO_SQLSRV
```php
<?php
// Specify Azure Key Vault credentials using the KeyStoreAuthentication, KeyStorePrincipalId, and KeyStoreSecret keywords
// Otherwise, the local Windows Certificate Store will be used
$options = "sqlsrv:server=$myServer;database=$myDatabase;driver={ODBC Driver 17 for SQL Server};";
$options .= "ColumnEncryption=VBS-HGS,http://myattestationserver.mydomain/Attestation",

$conn = new PDO($options, $myUsername, $myPassword);

// Create the table and insert the test data
$stmt = $conn->query($createTable);

foreach ($testValues as $values) {
    $stmt = $conn->prepare($insertData);
    $stmt->execute($values);
}

// Encrypt the table in place
$stmt = $conn->query($encryptQuery);

// Test comparison and pattern matching on the encrypted table
echo "Test comparisons:\n";

$intThreshold = 0;
$testGreater = "SELECT c_integer FROM $myTable WHERE c_integer > ?";
$stmt = $conn->prepare($testGreater);
$stmt->bindParam(1, $intThreshold, PDO::PARAM_INT);
getResults($stmt);
// Expect:
// 1
// 100

$datetimeThreshold = "3000-01-01 00:00:00.0";
$testLess = "SELECT c_datetime2 FROM $myTable WHERE c_datetime2 < ?";
$stmt = $conn->prepare($testLess);
$stmt->bindParam(1, $datetimeThreshold, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// 2019-12-31 01:00:00.0000000
// 1753-01-31 14:25:25.2500000
// 2112-03-15 23:40:10.1594000

$charThreshold = "abcd";
$ncharThreshold = "㬚㔈♠既";

$testGreaterEqual = "SELECT c_char FROM $myTable WHERE c_char >= ?";
$stmt = $conn->prepare($testGreaterEqual);
$stmt->bindParam(1, $charThreshold, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// abcd                            
// zyxwv                           

$testLessEqual = "SELECT c_nchar FROM $myTable WHERE c_nchar <= ?";
$stmt = $conn->prepare($testLessEqual);
$stmt->bindParam(1, $ncharThreshold, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// 㬚㔈♠既                            
// ઔܛ᎓Ե⅜                           
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    

$testNotGreater = "SELECT c_varchar FROM $myTable WHERE c_varchar !> ?";
$stmt = $conn->prepare($testNotGreater);
$stmt->bindParam(1, $charThreshold, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// abcd
// #e@?q&zy+
// 7t

$testNotLess = "SELECT c_nvarchar FROM $myTable WHERE c_nvarchar !< ?";
$stmt = $conn->prepare($testNotLess);
$stmt->bindParam(1, $ncharThreshold, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// 㬚㔈♠既
// 㶋㘚ᐋꗡ

echo "\nTest pattern matching:\n";

$charMatch = "%zy%";
$ncharMatch = "%㔈♠既%";

$testCharMatch = "SELECT c_char FROM $myTable WHERE c_char LIKE ? COLLATE Latin1_General_BIN2";
$stmt = $conn->prepare($testCharMatch);
$stmt->bindParam(1, $charMatch, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// #e@?q&zy+                       
// zyxwv                           

$testNCharMatch = "SELECT c_nchar FROM $myTable WHERE c_nchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = $conn->prepare($testNCharMatch);
$stmt->bindParam(1, $ncharMatch, PDO::PARAM_STR,null,PDO::SQLSRV_ENCODING_UTF8);
getResults($stmt);
// Expect:
// 㬚㔈♠既                            
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    

$testVarcharMatch = "SELECT c_varchar FROM $myTable WHERE c_varchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = $conn->prepare($testVarcharMatch);
$stmt->bindParam(1, $charMatch, PDO::PARAM_STR);
getResults($stmt);
// Expect:
// #e@?q&zy+
// zyxwv

$testNVarcharMatch = "SELECT c_nvarchar FROM $myTable WHERE c_nvarchar LIKE ? COLLATE Latin1_General_BIN2";
$stmt = $conn->prepare($testNVarcharMatch);
$stmt->bindParam(1, $ncharMatch, PDO::PARAM_STR,null,PDO::SQLSRV_ENCODING_UTF8);
getResults($stmt);
// Expect:
// 㬚㔈♠既
// 㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ

function getResults($stmt)
{
    $stmt->execute();
    while($res = $stmt->fetch(PDO::FETCH_NUM)) {
        print_r($res[0]);
        echo "\n";
    }
}
?>
```
輸出：
```
Test comparisons:
1
100
2019-12-31 01:00:00.0000000
1753-01-31 14:25:25.2500000
2112-03-15 23:40:10.1594000
abcd                            
zyxwv                           
㬚㔈♠既                            
ઔܛ᎓Ե⅜                           
㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    
abcd
#e@?q&zy+
7t
㬚㔈♠既
㶋㘚ᐋꗡ

Test pattern matching:
#e@?q&zy+                       
zyxwv                           
㬚㔈♠既                            
㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ                    
#e@?q&zy+
zyxwv
㬚㔈♠既
㛜ꆶ㕸㔈♠既ꁺꖁ㓫ޘ갧ᛄ
```
## <a name="see-also"></a>另請參閱  
[PHP SQL 驅動程式程式設計指南](programming-guide-for-php-sql-driver.md)  
[SQLSRV 驅動程式 API 參考](sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 驅動程式 API 參考](pdo-sqlsrv-driver-reference.md)  
[搭配 PHP Drivers for SQL Server 使用 Always Encrypted](using-always-encrypted-php-drivers.md)
  
