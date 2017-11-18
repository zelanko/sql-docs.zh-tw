---
title: "sqlsrv_fetch_object |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_fetch_object
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_object
- API Reference, sqlsrv_fetch_object
- retrieving data, as an object
ms.assetid: 4ce2df2c-083a-4a4d-a1e2-e866e63707d5
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0c2caedf7b6bb6e0e4a996c885144b219798ab1d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvfetchobject"></a>sqlsrv_fetch_object
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

將下一個資料列擷取為 PHP 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_fetch_object( resource $stmt [, string $className [, array $ctorParams[, row[, ]offset]]])  
```  
  
#### <a name="parameters"></a>參數  
*$stmt*：對應至執行之陳述式的陳述式資源。  
  
*$className* [選用]: 指定要具現化類別名稱的字串。 如果未指定 *$className* 參數的值，則會具現化 PHP **stdClass** 的執行個體。  
  
*$ctorParams* [選用]: 包含值的陣列傳遞至具有指定之類別的建構函式*$className*參數。 如果指定類別的建構函式接受參數值，則在呼叫 *$ctorParams* object **sqlsrv_fetch_object**參數。  
  
*資料列*[選用]: 下列的值，指定要在使用可捲動資料指標結果集內存取的資料列的其中一個。 (如果*列*指定，則*$className*和*$ctorParams*必須明確指定，即使您必須指定 null *$className*和*$ctorParams*。)  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
如需這些值的詳細資訊，請參閱 [指定資料指標類型及選取資料列](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)。  
  
*位移*[選用]: 與 SQLSRV_SCROLL_ABSOLUTE 和 sqlsrv_scroll_relative 搭配使用，用於指定要擷取的資料列。 結果集內的第一個記錄為 0。  
  
## <a name="return-value"></a>傳回值  
有屬性對應至結果集欄位名稱的 PHP 物件。 屬性值會以對應的結果集欄位值填入。 如果沒有以選用 *$className* 參數指定的類別存在，或是沒有與指定的陳述式相關聯的作用中結果集，則會傳回 **false** 。 如果沒有更多資料列可擷取，則會傳回 **null** 。  
  
傳回之物件中的資料類型值，將是預設的 PHP 資料類型。 如需預設 PHP 資料類型的相關資訊，請參閱 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。  
  
## <a name="remarks"></a>備註  
如果類別名稱是以選用 *$className* 參數指定的，則會具現化此類別類型的物件。 如果此類別具有名稱符合結果集欄位名稱的屬性，則會將對應的結果集值套用至屬性。 如果結果集欄位名稱不符合類別屬性，則會將具有結果集欄位名稱的屬性加入至物件，並將結果集值套用至屬性。  
  
以 *$className* 參數指定類別時，適用下列規則：  
  
-   比對會區分大小寫。 例如，屬性名稱 CustomerId 不符合欄位名稱 CustomerID。 在此情況下，CustomerID 屬性會加入至物件，且 CustomerID 欄位的值會提供給 CustomerID 屬性。  
  
-   無論存取修飾詞為何，都會進行比對。 例如，如果指定的類別具有名稱符合結果集欄位名稱的私用屬性，則會將結果集欄位中的值套用至屬性。  
  
-   類別屬性資料類型會被忽略。 如果結果集內的 "CustomerID" 欄位是字串，但類別的 "CustomerID" 屬性是整數，則會將結果集內的字串值寫入至 "CustomerID" 屬性。  
  
-   如果指定的類別不存在，則函數會傳回 **false** ，並將錯誤加入至錯誤集合。 如需擷取錯誤資訊的相關資訊，請參閱 [sqlsrv_errors](../../connect/php/sqlsrv-errors.md)。  
  
如果傳回沒有名稱的欄位，則 **sqlsrv_fetch_object** 會捨棄欄位值，並發出警告。 例如，請考量下列將值插入資料庫資料表中，並擷取伺服器產生之主索引鍵的 Transact-SQL 陳述式：  
  
<pre>INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()</pre>  
  
如果以 **sqlsrv_fetch_object**擷取此查詢所傳回的結果， `SELECT SCOPE_IDENTITY()` 所傳回的值將會被捨棄，並且會發出警告。 若要避免此狀況，您可以在 Transact-SQL 陳述式中為傳回的欄位指定名稱。 以下是在 Transact-SQL 中指定資料行名稱的方式之一：  
  
`SELECT SCOPE_IDENTITY() AS PictureID`  
  
## <a name="example"></a>範例  
下列範例會以 PHP 物件的形式，擷取結果集的每個資料列。 此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
  
/* Set up and execute the query. */  
$tsql = "SELECT FirstName, LastName  
         FROM Person.Contact  
         WHERE LastName='Alan'";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as a PHP object and display the results.*/  
while( $obj = sqlsrv_fetch_object( $stmt))  
{  
      echo $obj->LastName.", ".$obj->FirstName."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>範例  
下列範例會以指令碼中定義之 *Product* 類別的執行個體形式，擷取結果集的每個資料列。 此範例會擷取產品資訊*Purchasing.PurchaseOrderDetail*和*Production.Product*資料表的 AdventureWorks 資料庫具有指定的產品的到期日 (*DueDate*)，以及存貨的數量 (*StockQty*) 小於指定的值。 此範例強調在對 **sqlsrv_fetch_object**的呼叫中指定類別時所套用的某些規則：  
  
-   *$product* 變數是 *Product* 類別的執行個體，因為「產品」是以 *$className* 參數指定的，且 *Product* 類別存在。  
  
-   *Name* 屬性會加入至 *$product* 執行個體，因為現有的 *name* 屬性不相符。  
  
-   *Color* 屬性會加入至 *$product* 執行個體，因為沒有相符的屬性。  
  
-   私用屬性 *UnitPrice* 會以填入 *UnitPrice* 欄位的值填入。  
  
此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
```  
<?php  
/* Define the Product class. */  
class Product  
{  
     /* Constructor */  
     public function Product($ID)  
     {  
          $this->objID = $ID;  
     }  
     public $objID;  
     public $name;  
     public $StockedQty;  
     public $SafetyStockLevel;  
     private $UnitPrice;  
     function getPrice()  
     {  
          return $this->UnitPrice;  
     }  
}  
  
/* Connect to the local server using Windows Authentication, and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Define the query. */  
$tsql = "SELECT Name,  
                SafetyStockLevel,  
                StockedQty,  
                UnitPrice,  
                Color  
         FROM Purchasing.PurchaseOrderDetail AS pdo  
         JOIN Production.Product AS p  
         ON pdo.ProductID = p.ProductID  
         WHERE pdo.StockedQty < ?  
         AND pdo.DueDate= ?";  
  
/* Set the parameter values. */  
$params = array(3, '2002-01-29');  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql, $params);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set, printing a row of data upon each  
 iteration. Note the following:  
     1) $product is an instance of the Product class.  
     2) The $ctorParams parameter is required in the call to  
        sqlsrv_fetch_object, because the Product class constructor is  
        explicity defined and requires parameter values.  
     3) The "Name" property is added to the $product instance because  
        the existing "name" property does not match.  
     4) The "Color" property is added to the $product instance  
        because there is no matching property.  
     5) The private property "UnitPrice" is populated with the value  
        of the "UnitPrice" field.*/  
$i=0; //Used as the $objID in the Product class constructor.  
while( $product = sqlsrv_fetch_object( $stmt, "Product", array($i)))  
{  
     echo "Object ID: ".$product->objID."\n";  
     echo "Product Name: ".$product->Name."\n";  
     echo "Stocked Qty: ".$product->StockedQty."\n";  
     echo "Safety Stock Level: ".$product->SafetyStockLevel."\n";  
     echo "Product Color: ".$product->Color."\n";  
     echo "Unit Price: ".$product->getPrice()."\n";  
     echo "-----------------\n";  
     $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
**Sqlsrv_fetch_object**函式一律會傳回根據資料[預設 PHP 資料類型](../../connect/php/default-php-data-types.md)。 如需如何指定 PHP 資料類型的相關資訊，請參閱 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
如果傳回沒有名稱的欄位，則 **sqlsrv_fetch_object** 會捨棄欄位值，並發出警告。 例如，請考量下列將值插入資料庫資料表中，並擷取伺服器產生之主索引鍵的 Transact-SQL 陳述式：  
  
<pre>INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()</pre>  
  
如果以 **sqlsrv_fetch_object**擷取此查詢所傳回的結果， `SELECT SCOPE_IDENTITY()` 所傳回的值將會被捨棄，並且會發出警告。 若要避免此狀況，您可以在 Transact-SQL 陳述式中為傳回的欄位指定名稱。 以下是在 Transact-SQL 中指定資料行名稱的方式之一：  
  
`SELECT SCOPE_IDENTITY() AS PictureID`  
  
## <a name="see-also"></a>另請參閱  
[擷取資料](../../connect/php/retrieving-data.md)  
[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  
  

