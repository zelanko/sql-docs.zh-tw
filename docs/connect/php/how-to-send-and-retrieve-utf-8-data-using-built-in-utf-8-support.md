---
title: 如何：使用內建的 UTF-8 支援傳送及擷取 UTF-8 資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/23/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, UTF-8 encoded data
- converting data types
- updating data
ms.assetid: 366c57cf-352f-4202-8074-6ddce44880d1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db9f2758c2df5585a4d9034df7b309ae4547e52c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633936"
---
# <a name="how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support"></a>如何：使用內建的 UTF-8 支援傳送及接收 UTF-8 資料
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

如果您使用 PDO_SQLSRV 驅動程式，您可以指定具有 PDO::SQLSRV_ATTR_ENCODING 屬性的編碼。 如需詳細資訊，請參閱 [常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。  
  
本主題的其餘部分將討論 SQLSRV 驅動程式的編碼功能。  
  
若要將 UTF-8 編碼資料傳送或擷取至伺服器：  
  
1.  確定來源或目的地資料行屬於 **nchar** 或 **nvarchar**類型。  
  
2.  將 PHP 類型指定為參數陣列中的 `SQLSRV_PHPTYPE_STRING('UTF-8')` 。 或者，將 `"CharacterSet" => "UTF-8"` 指定為連接選項。  
  
    當您將字元集指定為連接選項的一部分時，驅動程式會假設其他連接選項字串使用這個相同的字元集。 此外也會假設伺服器名稱和查詢字串使用相同的字元集。  
  
您可以將 UTF-8 或 SQLSRV_ENC_CHAR 傳遞至 **CharacterSet**，但您無法傳遞 SQLSRV_ENC_BINARY。 預設編碼為 SQLSRV_ENC_CHAR。  
  
## <a name="example"></a>範例  
下列範例在建立連接時，如何藉由指定 UTF-8 字元集來傳送及擷取 UTF-8 編碼資料。 此範例會更新 Production.ProductReview 資料表中指定的檢閱識別碼的「註解」資料行。 此範例也會擷取新的更新資料，並加以顯示。 請注意，「註解」資料行屬於 **nvarchar(3850)** 類型。 同時請注意，資料在傳送到伺服器之前，會使用 PHP **utf8_encode** 函式轉換成 UTF-8 編碼。 此作業僅供示範使用。 在實際的應用程式案例中，您會從 UTF-8 編碼資料著手。  
  
此範例假設本機電腦上已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫。 從瀏覽器執行範例時，所有輸出都會寫入至瀏覽器。  
  
```  
<?php  
  
// Connect to the local server using Windows Authentication and  
// specify the AdventureWorks database as the database in use.   
//   
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", "CharacterSet" => "UTF-8");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Set up the Transact-SQL query.  
//   
$tsql1 = "UPDATE Production.ProductReview  
          SET Comments = ?  
          WHERE ProductReviewID = ?";  
  
// Set the parameter values and put them in an array. Note that  
// $comments is converted to UTF-8 encoding with the PHP function  
// utf8_encode to simulate an application that uses UTF-8 encoded data.   
//   
$reviewID = 3;  
$comments = utf8_encode("testing 1, 2, 3, 4.  Testing.");  
$params1 = array(  
                  array( $comments, null ),  
                  array( $reviewID, null )  
                );  
  
// Execute the query.  
//   
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
  
if ( $stmt1 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
else {  
   echo "The update was successfully executed.<br>";  
}  
  
// Retrieve the newly updated data.  
//   
$tsql2 = "SELECT Comments   
          FROM Production.ProductReview   
          WHERE ProductReviewID = ?";  
  
// Set up the parameter array.  
//   
$params2 = array($reviewID);  
  
// Execute the query.  
//   
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if ( $stmt2 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data.   
//   
if ( sqlsrv_fetch($stmt2) ) {  
   echo "Comments: ";  
   $data = sqlsrv_get_field( $stmt2, 0 );  
   echo $data."<br>";  
}  
else {  
   echo "Error in fetching data.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Free statement and connection resources.  
//   
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_close( $conn);  
?>  
```  
  
如需儲存 Unicode 資料的資訊，請參閱 [使用 Unicode 資料](https://msdn.microsoft.com/library/ms175180.aspx)。  
  
## <a name="example"></a>範例  
下列範例類似於第一個範例，但此範例不會在連接上指定 UTF-8 字元集，而會說明如何在資料行上指定 UTF-8 字元集。  
  
```  
<?php  
  
// Connect to the local server using Windows Authentication and  
// specify the AdventureWorks database as the database in use.   
//   
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Set up the Transact-SQL query.  
//   
$tsql1 = "UPDATE Production.ProductReview  
          SET Comments = ?  
          WHERE ProductReviewID = ?";  
  
// Set the parameter values and put them in an array. Note that  
// $comments is converted to UTF-8 encoding with the PHP function  
// utf8_encode to simulate an application that uses UTF-8 encoded data.   
//   
$reviewID = 3;  
$comments = utf8_encode("testing");  
$params1 = array(  
                  array($comments,  
                        SQLSRV_PARAM_IN,  
                        SQLSRV_PHPTYPE_STRING('UTF-8')  
                  ),  
                  array($reviewID)  
                );  
  
// Execute the query.  
//   
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
  
if ( $stmt1 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
else {  
   echo "The update was successfully executed.<br>";  
}  
  
// Retrieve the newly updated data.  
//   
$tsql2 = "SELECT Comments   
          FROM Production.ProductReview   
          WHERE ProductReviewID = ?";  
  
// Set up the parameter array.  
//   
$params2 = array($reviewID);  
  
// Execute the query.  
//   
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if ( $stmt2 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data.   
//   
if ( sqlsrv_fetch($stmt2) ) {  
   echo "Comments: ";  
   $data = sqlsrv_get_field($stmt2,   
                            0,   
                            SQLSRV_PHPTYPE_STRING('UTF-8')  
                           );  
   echo $data."<br>";  
}  
else {  
   echo "Error in fetching data.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Free statement and connection resources.  
//   
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[擷取資料](../../connect/php/retrieving-data.md)

[使用 在非 Windows 的 ASCII 資料](../../connect/php/how-to-send-and-retrieve-ascii-data-in-linux-mac.md)

[更新資料 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[範例應用程式 &#40;SQLSRV 驅動程式&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
