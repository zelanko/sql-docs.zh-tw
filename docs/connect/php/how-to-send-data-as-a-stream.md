---
title: "如何： 將資料傳送資料流的形式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data
- streaming data
ms.assetid: ab6b95d6-b6e6-4bd7-a18c-50f2918f7532
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26f92ed23a77fc4cf670f8184a9cf1b1de78ba20
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-send-data-as-a-stream"></a>如何：以資料流的形式傳送資料
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會利用 PHP 資料流將大型物件傳送至伺服器。 本主題中的範例會示範如何以資料流的形式傳送資料。 第一個範例會使用 SQLSRV 驅動程式示範預設行為，也就是在查詢執行時傳送所有的資料流資料。 第二個範例會使用 SQLSRV 驅動程式示範如何將最多 8K 的資料流資料同時傳送至伺服器。  
  
第三個範例說明如何使用 PDO_SQLSRV 驅動程式將資料流資料傳送至伺服器。  
  
## <a name="example"></a>範例  
下列範例會在 AdventureWorks 資料庫的 *Production.ProductReview* 資料表中插入資料列。 客戶意見 (*$comments*) 會透過 PHP 資料流的形式開啟[fopen](http://php.net/manual/en/function.fopen.php)函式，並接著串流處理至伺服器在執行查詢時。  
  
此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 資料庫。 所有輸出都會寫入至主控台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,  
                                               ReviewDate,  
                                               EmailAddress,  
                                               Rating,  
                                               Comments)  
         VALUES (?, ?, ?, ?, ?, ?)";  
  
/* Set the parameter values and put them in an array.  
Note that $comments is opened as a stream. */  
$productID = '709';  
$name = 'Customer Name';  
$date = date("Y-m-d");  
$email = 'customer@name.com';  
$rating = 3;  
$comments = fopen( "data://text/plain,[ Insert lengthy comment here.]",  
                  "r");  
$params = array($productID, $name, $date, $email, $rating, $comments);  
  
/* Execute the query. All stream data is sent upon execution.*/  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
else  
{  
     echo "The query was successfully executed.";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>範例  
下一個範例與上述範例相同，但關閉了在執行時傳送所有資料流資料的預設行為。 此範例會使用 [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md) 將資料流資料傳送至伺服器。 最多 8 kb (8k) 的資料會傳送每次呼叫**sqlsrv_send_stream_data**。 指令碼會計算 **sqlsrv_send_stream_data** 所發出的呼叫數，並將此計數顯示到主控台。  
  
此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 資料庫。 所有輸出都會寫入至主控台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,  
                                               ReviewDate,  
                                               EmailAddress,  
                                               Rating,  
                                               Comments)  
         VALUES (?, ?, ?, ?, ?, ?)";  
  
/* Set the parameter values and put them in an array.  
Note that $comments is opened as a stream. */  
$productID = '709';  
$name = 'Customer Name';  
$date = date("Y-m-d");  
$email = 'customer@name.com';  
$rating = 3;  
$comments = fopen( "data://text/plain,[ Insert lengthy comment here.]",  
                  "r");  
$params = array($productID, $name, $date, $email, $rating, $comments);  
  
/* Turn off the default behavior of sending all stream data at  
execution. */  
$options = array("SendStreamParamsAtExec" => 0);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params, $options);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Send up to 8K of parameter data to the server with each call to  
sqlsrv_send_stream_data. Count the calls. */  
$i = 1;  
while( sqlsrv_send_stream_data( $stmt))   
{  
     echo "$i call(s) made.\n";  
     $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
本主題中的範例傳送至伺服器的是字元資料，但實際上任何格式的資料都可用資料流的形式傳送。 例如，您也可以使用本主題中示範的技術，以資料流傳送二進位格式的映像。  
  
## <a name="example"></a>範例  
  
```  
<?php  
   $server = "(local)";   
   $database = "Test";  
   $conn = new PDO( "sqlsrv:server=$server;Database = $database", "", "");  
  
   $binary_source = fopen( "data://text/plain,", "r");  
  
   $stmt = $conn->prepare("insert into binaries (imagedata) values (?)");  
   $stmt->bindParam(1, $binary_source, PDO::PARAM_LOB);   
  
   $conn->beginTransaction();  
   $stmt->execute();  
   $conn->commit();  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[更新資料 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[使用 SQLSRV 驅動程式以資料流形式擷取資料](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)  
[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  
  

