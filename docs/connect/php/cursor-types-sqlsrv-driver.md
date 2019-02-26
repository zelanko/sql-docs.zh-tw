---
title: 資料指標類型 （SQLSRV 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f435b3f2308557654259395e296c07956a2c337
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676136"
---
# <a name="cursor-types-sqlsrv-driver"></a>資料指標類型 (SQLSRV 驅動程式)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQLSRV 驅動程式可讓您根據資料指標類型，建立能夠以任何順序存取資料列的結果集。  本主題將討論用戶端 （緩衝） 和伺服器端 （無緩衝） 資料指標。  
  
## <a name="cursor-types"></a>資料指標類型  
當您建立結果集[sqlsrv_query](../../connect/php/sqlsrv-query.md)或使用[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)，您可以指定資料指標的類型。 根據預設，會使用順向資料指標，可讓您開始第一列的結果集，直到您到達結果集的結尾一次移動一個資料列。  
  
您可以建立含有可讓您存取任何資料列在結果集中，以任何順序可捲動資料指標的結果集。 下表列出的值，可以傳遞至**可捲動**sqlsrv_query sqlsrv_prepare 中的選項。  
  
|選項|Description|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|可讓您開始第一列的結果集，直到您到達結果集的結尾一次移動一個資料列。<br /><br />這是預設資料指標類型。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)會傳回與此資料指標類型所建立的結果集的錯誤。<br /><br />**向前**是 SQLSRV_CURSOR_FORWARD 縮寫的形式。|  
|SQLSRV_CURSOR_STATIC|可讓您以任何順序存取資料列，但將不會反映資料庫中的變更。<br /><br />**靜態**是 SQLSRV_CURSOR_STATIC 縮寫的形式。|  
|SQLSRV_CURSOR_DYNAMIC|可讓您以任何順序存取資料列，並將會反映資料庫中的變更。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)會傳回與此資料指標類型所建立的結果集的錯誤。<br /><br />**動態**是 SQLSRV_CURSOR_DYNAMIC 縮寫的形式。|  
|SQLSRV_CURSOR_KEYSET|可讓您存取任何順序中的資料列。 不過，如果資料列已從資料表中刪除，則索引鍵集資料指標不會更新資料列計數 (已刪除的資料列傳回時不會有值)。<br /><br />**索引鍵集**是 SQLSRV_CURSOR_KEYSET 縮寫的形式。|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|可讓您存取任何順序中的資料列。 建立用戶端資料指標查詢。<br /><br />**緩衝處理**是 SQLSRV_CURSOR_CLIENT_BUFFERED 縮寫的形式。|  
  
查詢會產生多個結果集，如果**可捲動**選項會套用至所有結果集。  
  
## <a name="selecting-rows-in-a-result-set"></a>在結果集中選取的資料列  
建立結果集之後，您可以使用[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)， [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)，或[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)指定的資料列。  
  
下表描述您可以在指定的值*資料列*參數。  
  
|參數|Description|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|指定下一個資料列。 這是預設值，如果您未指定*資料列*可捲動的結果集的參數。|  
|SQLSRV_SCROLL_PRIOR|指定目前的資料列之前的資料列。|  
|SQLSRV_SCROLL_FIRST|指定結果集中的第一個資料列。|  
|SQLSRV_SCROLL_LAST|指定結果集中的最後一個資料列。|  
|SQLSRV_SCROLL_ABSOLUTE|指定使用指定的資料列*位移*參數。|  
|SQLSRV_SCROLL_RELATIVE|指定使用指定的資料列*位移*目前資料列的參數。|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>伺服器端資料指標和 SQLSRV 驅動程式  
下列範例顯示各種不同的資料指標的效果。 在範例中的一行 33，您會看到三個指定不同的資料指標的查詢陳述式的第一個。  兩個查詢陳述式會標記為註解。 每次執行程式，會使用不同的資料指標類型來查看第 47 行上的資料庫更新的影響。  
  
```  
<?php  
$server = "server_name";  
$conn = sqlsrv_connect( $server, array( 'Database' => 'test' ));  
if ( $conn === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "DROP TABLE dbo.ScrollTest" );  
if ( $stmt !== false ) {   
   sqlsrv_free_stmt( $stmt );   
}  
  
$stmt = sqlsrv_query( $conn, "CREATE TABLE ScrollTest (id int, value char(10))" );  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 1, "Row 1" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 2, "Row 2" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 3, "Row 3" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'keyset' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'dynamic' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'static' ));  
  
$rows = sqlsrv_has_rows( $stmt );  
if ( $rows != true ) {  
   die( "Should have rows" );  
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
$stmt2 = sqlsrv_query( $conn, "delete from ScrollTest where id = 3" );  
// or  
// $stmt2 = sqlsrv_query( $conn, "UPDATE ScrollTest SET id = 4 WHERE id = 3" );  
if ( $stmt2 !== false ) {   
   sqlsrv_free_stmt( $stmt2 );   
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>用戶端資料指標和 SQLSRV 驅動程式  
用戶端資料指標是 3.0 版中新增的功能[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，可讓您快取的整個結果集在記憶體中。 使用用戶端資料指標時，會執行查詢之後，可以使用資料列計數。  
  
用戶端資料指標應該用於小型到中型-大小的結果集。 使用伺服端資料指標的大型結果集。  
  
查詢會傳回 false，如果緩衝區不夠大，無法容納整個結果集。 您可以增加到 PHP 記憶體限制的緩衝區大小。  
  
使用 SQLSRV 驅動程式，您可以設定保留的結果集的 ClientBufferMaxKBSize 設定緩衝區的大小[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)。 [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)傳回 ClientBufferMaxKBSize 的值。 您也可以在 php.ini 檔案中以 sqlsrv 設定緩衝區大小上限。ClientBufferMaxKBSize (比方說，sqlsrv。ClientBufferMaxKBSize = 1024年)。  
  
下列範例會示範：  
  
-   資料列計數一定會是適用於用戶端資料指標。  
  
-   使用用戶端資料指標和批次陳述式。  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Department";  
  
// Execute the query with client-side cursor.  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// row count is always available with a client-side cursor  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count = $row_count\n";  
  
// Move to a specific row in the result set.  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_LAST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
?>  
```  
  
下列範例會示範用戶端資料指標，使用[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)和不同的用戶端緩衝區大小。
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Employee";  
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable" => SQLSRV_CURSOR_CLIENT_BUFFERED, "ClientBufferMaxKBSize" => 51200));
  
if (! $stmt ) {  
   echo "Statement could not be prepared.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_execute( $stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
if ($row_count)  
   echo "\nRow count = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
if ($row ) {  
   $EmployeeID = sqlsrv_get_field( $stmt, 0);  
   echo "Employee ID = $EmployeeID \n";  
}  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[指定資料指標類型及選取資料列](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
