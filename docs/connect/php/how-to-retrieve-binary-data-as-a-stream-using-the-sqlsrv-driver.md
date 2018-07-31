---
title: 如何：使用 SQLSRV 驅動程式以資料流形式擷取二進位資料 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, as a binary stream
- streaming data
ms.assetid: cd8d6382-abe6-48ee-9d10-4e6c52c0cb9a
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d10cc259971d2a81177ee8e04844a54b26cf147c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979835"
---
# <a name="how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驅動程式以資料流形式擷取二進位資料
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

以資料流形式擷取資料僅適用於 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 SQLSRV 驅動程式，而不適用於 PDO_SQLSRV 驅動程式。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會利用 PHP 資料流從伺服器擷取大量的二進位資料。 本主題示範如何以資料流形式擷取資料。  
  
使用資料流來擷取二進位資料 (例如影像)，可避免使用大量的指令碼記憶體，其作法是擷取資料區塊，而非將整個物件載入指令碼記憶體中。  
  
## <a name="example"></a>範例  
下列範例會從 AdventureWorks 資料庫的 *Production.ProductPhoto* 資料表擷取二進位資料 (在此案例中是影像)。 影像會擷取為資料流並顯示在瀏覽器中。  
  
使用 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) 和 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) 搭配指定為二進位資料流的傳回類型，即可完成以資料流形式擷取影像資料。 使用常數 **SQLSRV_PHPTYPE_STREAM** 可指定傳回型別。 如需 **sqlsrv** 常數的資訊，請參閱[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。  
  
此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫。 從瀏覽器執行範例時，所有輸出都會寫入至瀏覽器。  
  
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
$tsql = "SELECT LargePhoto   
         FROM Production.ProductPhoto   
         WHERE ProductPhotoID = ?";  
  
/* Set the parameter values and put them in an array. */  
$productPhotoID = 70;  
$params = array( $productPhotoID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data.  
The return data is retrieved as a binary stream. */  
if ( sqlsrv_fetch( $stmt ) )  
{  
   $image = sqlsrv_get_field( $stmt, 0,   
                      SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_BINARY));  
   header("Content-Type: image/jpg");  
   fpassthru($image);  
}  
else  
{  
     echo "Error in retrieving data.</br>";  
     die(print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
在範例中指定傳回類型，可示範如何將 PHP 傳回類型指定為二進位資料流。 技術上來說，不一定要在範例中，因為 *LargePhoto* 欄位具有 SQL Server 類型 varbinary(max)，因此預設會以二進位資料流形式傳回。 如需有關預設 PHP 資料類型的詳細資訊，請參閱 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。 如需有關如何指定 PHP 傳回類型的詳細資訊，請參閱 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
## <a name="see-also"></a>另請參閱  
[擷取資料](../../connect/php/retrieving-data.md)

[使用 SQLSRV 驅動程式以資料流形式擷取資料](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  
  
