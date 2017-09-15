---
title: "使用 SQLSRV 驅動程式以資料流形式擷取字元資料 |Microsoft 文件"
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
- retrieving data, as a character stream
- streaming data
ms.assetid: 3c0dbca4-abfc-4449-b133-66c819681840
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 30d0b0884b258d494ffadcb3d44b76f197a445a5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驅動程式以資料流的形式擷取字元資料
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

資料流只能用於 SQLSRV 驅動程式的形式擷取資料[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，並不適用於 PDO_SQLSRV 驅動程式。  
  
SQLSRV 驅動程式會利用 PHP 資料流，從伺服器擷取大量的資料。 本主題中的範例會示範如何以資料流的形式擷取字元資料。  
  
## <a name="example"></a>範例  
下列範例會從 AdventureWorks 資料庫的 *Production.ProductReview* 資料表中擷取資料列。 傳回資料列的 [註解] 欄位會以資料流的形式擷取，並使用 PHP [fpassthru](http://go.microsoft.com/fwlink/?LinkId=217496) 函數來顯示。  
  
使用 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) 和 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) 搭配指定為字元資料流的傳回類型，可完成以資料流的形式擷取資料的作業。 使用常數指定傳回類型**SQLSRV_PHPTYPE_STREAM**。 如需有關資訊**sqlsrv**常數，請參閱[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
此範例假設本機電腦上已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
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
$tsql = "SELECT ReviewerName,   
               CONVERT(varchar(32), ReviewDate, 107) AS [ReviewDate],  
               Rating,   
               Comments   
         FROM Production.ProductReview   
         WHERE ProductReviewID = ? ";  
  
/* Set the parameter value. */  
$productReviewID = 1;  
$params = array( $productReviewID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first three fields are retrieved  
as strings and the fourth as a stream with character encoding. */  
if(sqlsrv_fetch( $stmt ) === false )  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
echo "Date: ".sqlsrv_get_field( $stmt, 1 )."\n";  
echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
echo "Comments: ";  
$comments = sqlsrv_get_field( $stmt, 3,   
                             SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
fpassthru($comments);  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
由於未指定前三個欄位的 PHP 傳回類型，因此會根據其預設 PHP 類型傳回每個欄位。 如需有關預設 PHP 資料類型的詳細資訊，請參閱 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。 如需有關如何指定 PHP 傳回類型的詳細資訊，請參閱 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
## <a name="see-also"></a>另請參閱  
[擷取資料](../../connect/php/retrieving-data.md)  
[使用 SQLSRV 驅動程式以資料流形式擷取資料](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)  
[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  
  

