---
title: 如何： 指定 PHP 資料類型 |Microsoft 文件
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
- converting data types
- streaming data
ms.assetid: fee6e6b8-aad9-496b-84a2-18d2950470a4
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d41612ee46f791ef5a130e82d7f75b7afecea3a9
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307597"
---
# <a name="how-to-specify-php-data-types"></a>如何：指定 PHP 資料類型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

使用 PDO_SQLSRV 驅動程式時，您可以在從伺服器擷取資料時，透過 PDOStatement::bindColumn 和 PDOStatement::bindParam 來指定 PHP 資料類型。 如需詳細資訊，請參閱＜ [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) ＞和＜ [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md) ＞。  
  
下列步驟概述如何在從伺服器擷取資料時使用 SQLSRV 驅動程式指定 PHP 資料類型：  
  
1.  設定及執行的 TRANSACT-SQL 查詢[sqlsrv_query](../../connect/php/sqlsrv-query.md)或結合[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)。  
  
2.  讓某個資料列可透過 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)來讀取。  
  
3.  使用 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) ，並將所需的 PHP 資料類型指定為選用的第三個參數，以從傳回的資料列中擷取欄位資料。 如果未指定選擇性的第三個參數，則會根據預設 PHP 類型傳回資料。 如需預設 PHP 傳回類型的相關資訊，請參閱 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。  
  
    用來指定 PHP 資料類型之常數的相關資訊，請參閱 phptype 」 一節的[常數&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。  
  
## <a name="example"></a>範例  
下列範例會從 AdventureWorks 資料庫的 *Production.ProductReview* 資料表中擷取資料列。 每個傳回的資料列中*ReviewDate*欄位會擷取為字串而*註解*欄位會擷取為資料流。 串流資料可使用 PHP [fpassthru](http://php.net/manual/en/function.fpassthru.php) 函數來顯示。  
  
此範例假設 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)資料庫安裝在本機電腦上。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. */  
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
                ReviewDate,  
                Rating,   
                Comments   
         FROM Production.ProductReview   
         WHERE ProductID = ?   
         ORDER BY ReviewDate DESC";  
  
/* Set the parameter value. */  
$productID = 709;  
$params = array( $productID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first and third fields are  
retrieved according to their default types, strings. The second field  
is retrieved as a string with 8-bit character encoding. The fourth  
field is retrieved as a stream with 8-bit character encoding.*/  
while ( sqlsrv_fetch( $stmt))  
{  
   echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
   echo "Date: ".sqlsrv_get_field( $stmt, 1,   
                       SQLSRV_PHPTYPE_STRING( SQLSRV_ENC_CHAR))."\n";  
   echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
   echo "Comments: ";  
   $comments = sqlsrv_get_field( $stmt, 3,   
                            SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
   fpassthru( $comments);  
   echo "\n";   
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
在範例中，擷取第二個欄位 (*ReviewDate*) 為字串，可保留 SQL Server DATETIME 資料類型的毫秒精確度。 根據預設，SQL Server DATETIME 資料類型會擷取為 PHP DateTime 物件，因而失去毫秒精確度。  
  
擷取第四個欄位 (*註解*) 為資料流是為了示範之用。 根據預設，SQL Server 資料類型 nvarchar(3850) 會擷取為字串，這在大多數的情況下是可接受的。  
  
> [!NOTE]  
> [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) 函數可用來在執行查詢之前取得欄位資訊，包括類型資訊。  
  
## <a name="see-also"></a>另請參閱  
[擷取資料](../../connect/php/retrieving-data.md)

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)

[如何：使用 SQLSRV 驅動程式擷取輸出參數](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
