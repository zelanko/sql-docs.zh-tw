---
title: 如何： 傳送和擷取 ASCII 資料在 Linux 和 macOS (SQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: mbarwin
ms.openlocfilehash: 32599ca0facc7a35877f6d59573b27209ce68d31
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307677"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>如何： 傳送和擷取 ASCII 資料在 Linux 和 macOS 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本文章假設已產生或安裝在 Linux 或 macOS 系統中的 ASCII (非-utf-8) 地區設定。 

若要傳送或擷取至伺服器的 ASCII 字元集：  

1.  如果想要的地區設定不是您的系統環境中的預設值，請確定您叫用`setlocale(LC_ALL, $locale)`之前建立的第一個連接。 PHP setlocale() 函式變更地區設定只針對目前的指令碼中，且如果叫用第一個連接後，它可能被忽略。
 
2.  當使用 SQLSRV 驅動程式，您可能會指定`'CharacterSet' => SQLSRV_ENC_CHAR`做為連接選項，但此步驟是選擇性因為它是預設編碼方式。

3.  當使用 PDO_SQLSRV 驅動程式，有兩種方式。 首先，在連線時，設定`PDO::SQLSRV_ATTR_ENCODING`至`PDO::SQLSRV_ENCODING_SYSTEM`(如需設定連接選項的範例，請參閱[pdo:: __construct](../../connect/php/pdo-construct.md))。 或者，在連接成功後，新增這行 `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
當您指定的連接資源 （在 SQLSRV) 或連接物件 (PDO_SQLSRV) 編碼方式時，驅動程式會假設其他連接選項字串使用該相同的編碼方式。 此外也會假設伺服器名稱和查詢字串使用相同的字元集。  
  
預設編碼方式 PDO_SQLSRV 驅動程式是 utf-8 (pdo:: SQLSRV_ENCODING_UTF8)，不同於 SQLSRV 驅動程式。 如需有關這些常數的詳細資訊，請參閱[常數&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。 
  
## <a name="example"></a>範例  
下列範例會示範如何傳送和擷取 ASCII 資料藉由指定特定地區設定進行連接之前，使用 for SQL Server 的 PHP 驅動程式。 在各種 Linux 平台的地區設定的名稱可能不同從 macOS 中相同的地區設定。 例如，美國 iso-8859-1 (拉丁文 1) 地區設定是`en_US.ISO-8859-1`linux 時名稱就是 macOS `en_US.ISO8859-1`。
  
範例假設[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]安裝在伺服器上。 從瀏覽器執行範例時，所有輸出都會都寫入至瀏覽器。  
  
```  
<?php  
  
// SQLSRV Example
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';
$connectionInfo = array('Database'=>'Test', 'UID'=>$uid, 'PWD'=>$pwd);
$conn = sqlsrv_connect($serverName, $connectionInfo);
  
if ($conn === false) {
    echo "Could not connect.<br>";  
    die(print_r(sqlsrv_errors(), true));
}  
  
// Set up the Transact-SQL query to create a test table
//   
$stmt = sqlsrv_query($conn, "CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");

// Insert data using a parameter array 
//
$tsql = "INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (?, ?)";
  
// Execute the query, $value being some ASCII string
//   
$stmt = sqlsrv_query($conn, $tsql, array(1, array($value, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))));
  
if ($stmt === false) {
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
else {  
    echo "The insertion was successfully executed.<br>";  
}  
  
// Retrieve the newly inserted data
//   
$stmt = sqlsrv_query($conn, "SELECT * FROM Table1");
$outValue = null;  
if ($stmt === false) {  
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data
//   
if (sqlsrv_fetch($stmt)) {  
    $outValue = sqlsrv_get_field($stmt, 1, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    echo "Value: " . $outValue . "<br>";
    if ($value !== $outValue) {
        echo "Data retrieved, \'$outValue\', is unexpected!<br>";
    }
}  
else {  
    echo "Error in fetching data.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Free statement and connection resources
//   
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
```
<?php  
  
// PDO_SQLSRV Example:
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';

try {
    $conn = new PDO("sqlsrv:Server=$serverName;Database=$database;", $uid, $pwd);
    $conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);
    
    // Set up the Transact-SQL query to create a test table
    //   
    $stmt = $conn->query("CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");
    
    // Insert data using parameters, $value being some ASCII string
    //
    $stmt = $conn->prepare("INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (:var1, :var2)");
    $stmt->bindValue(1, 1);
    $stmt->bindParam(2, $value);
    $stmt->execute();
    
    // Retrieve and display the data
    //
    $stmt = $conn->query("SELECT * FROM [Table1]");
    $outValue = null;
    if ($row = $stmt->fetch()) {
        $outValue = $row[1];
        echo "Value: " . $outValue . "<br>";
        if ($value !== $outValue) {
            echo "Data retrieved, \'$outValue\', is unexpected!<br>";
        }
    }
} catch (PDOException $e) {
    echo $e->getMessage() . "<br>";
} finally {
    // Free statement and connection resources
    //
    unset($stmt);
    unset($conn);
}

?>  
```  

## <a name="see-also"></a>另請參閱  
[擷取資料](../../connect/php/retrieving-data.md)  
[使用 utf-8 資料](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[更新資料&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[範例應用程式 &#40;SQLSRV 驅動程式&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
