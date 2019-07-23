---
title: '如何: 在 Linux 和 macOS 中傳送和取出 ASCII 資料 (SQL) |Microsoft Docs'
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 9edd73f5ef01d1d3f22db78400cc3c204efe1379
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68251899"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>如何：傳送及擷取 Linux 與 macOS 中的 ASCII 資料 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本文假設您的 Linux 或 macOS 系統中已產生或安裝 ASCII (非 UTF-8) 地區設定。 

若要將 ASCII 字元集傳送或取出至伺服器:  

1.  如果您的系統內容中所需的地區設定不是預設值, 請`setlocale(LC_ALL, $locale)`確定您在進行第一次連接之前先叫用。 PHP setlocale () 函數只會變更目前腳本的地區設定, 而且如果在進行第一次連接之後叫用, 則可能會被忽略。
 
2.  使用 SQLSRV 驅動程式時, 您可以將`'CharacterSet' => SQLSRV_ENC_CHAR`指定為連接選項, 但這個步驟是選擇性的, 因為它是預設的編碼方式。

3.  使用 PDO_SQLSRV 驅動程式時, 有兩種方式。 首先, 在建立連接時, 將`PDO::SQLSRV_ATTR_ENCODING`設定`PDO::SQLSRV_ENCODING_SYSTEM`為 (如需設定連線選項的範例, 請參閱[PDO:: __construct](../../connect/php/pdo-construct.md))。 或者, 在成功連線之後, 新增這一行`$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
當您指定連接資源 (SQLSRV) 或連線物件 (PDO_SQLSRV) 的編碼方式時, 驅動程式會假設其他連接選項字串使用相同的編碼方式。 此外也會假設伺服器名稱和查詢字串使用相同的字元集。  
  
PDO_SQLSRV 驅動程式的預設編碼方式為 UTF-8 (PDO:: SQLSRV_ENCODING_UTF8), 與 SQLSRV 驅動程式不同。 如需這些常數的詳細資訊，請參閱[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。 
  
## <a name="example"></a>範例  
下列範例示範如何在進行連接之前指定特定地區設定, 以使用 PHP 驅動程式來傳送和抓取 ASCII 資料, 以進行 SQL Server。 不同 Linux 平臺的地區設定可能會以不同于 macOS 中相同地區設定的方式命名。 例如, 當 macOS 中的名稱是`en_US.ISO-8859-1` `en_US.ISO8859-1`時, 美國 ISO-8859-1 (拉丁 1) 地區設定是在 Linux 中。
  
這些範例假設[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已安裝在伺服器上。 從瀏覽器執行範例時，所有輸出都會寫入至瀏覽器。  
  
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
[更新資料&#40;適用于 PHP 的 Microsoft 驅動程式 SQL Server&#41; ](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[範例應用程式 &#40;SQLSRV 驅動程式&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
