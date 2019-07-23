---
title: 資料指標類型 (SQLSRV 驅動程式) | Microsoft Docs
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
ms.openlocfilehash: ac090ad8831397bf31c0911ab8a8db21486528db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015110"
---
# <a name="cursor-types-sqlsrv-driver"></a>資料指標類型 (SQLSRV 驅動程式)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQLSRV 驅動程式可讓您根據資料指標類型，建立能夠以任何順序存取資料列的結果集。  本主題將討論用戶端 (緩衝) 和伺服器端 (無緩衝) 的資料指標。  
  
## <a name="cursor-types"></a>資料指標類型  
當您使用[sqlsrv_query](../../connect/php/sqlsrv-query.md)或[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)來建立結果集時, 可以指定資料指標的類型。 根據預設, 會使用順向資料指標, 這可讓您從結果集的第一個資料列開始, 一次移動一個資料列, 直到達到結果集的結尾為止。  
  
您可以使用可滾動的資料指標來建立結果集, 讓您以任何順序存取結果集中的任何資料列。 下表列出可以傳遞至 sqlsrv_query 或 sqlsrv_prepare 中可**滾動**選項的值。  
  
|選項|Description|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|讓您從結果集的第一個資料列開始, 一次移動一個資料列, 直到達到結果集的結尾為止。<br /><br />這是預設的資料指標類型。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)會針對使用此資料指標類型所建立的結果集傳回錯誤。<br /><br />**forward**是 SQLSRV_CURSOR_FORWARD 的縮寫格式。|  
|SQLSRV_CURSOR_STATIC|可讓您以任何順序存取資料列, 但不會反映資料庫中的變更。<br /><br />**靜態**是 SQLSRV_CURSOR_STATIC 的縮寫格式。|  
|SQLSRV_CURSOR_DYNAMIC|可讓您依任何順序存取資料列, 而且會反映資料庫中的變更。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)會針對使用此資料指標類型所建立的結果集傳回錯誤。<br /><br />**dynamic**是 SQLSRV_CURSOR_DYNAMIC 的縮寫格式。|  
|SQLSRV_CURSOR_KEYSET|可讓您依任何順序存取資料列。 不過，如果資料列已從資料表中刪除，則索引鍵集資料指標不會更新資料列計數 (已刪除的資料列傳回時不會有值)。<br /><br />索引**鍵集**是 SQLSRV_CURSOR_KEYSET 的縮寫格式。|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|可讓您依任何順序存取資料列。 建立用戶端資料指標查詢。<br /><br />**緩衝**處理是 SQLSRV_CURSOR_CLIENT_BUFFERED 的縮寫格式。|  
  
如果查詢產生多個結果集, 則可**滾動**選項會套用至所有結果集。  
  
## <a name="selecting-rows-in-a-result-set"></a>選取結果集中的資料列  
建立結果集之後, 您可以使用[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)、 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)或[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)來指定資料列。  
  
下表描述您可以在*row*參數中指定的值。  
  
|參數|Description|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|指定下一個資料列。 如果您未指定可滾動結果集的資料*列*參數, 這就是預設值。|  
|SQLSRV_SCROLL_PRIOR|指定目前資料列之前的資料列。|  
|SQLSRV_SCROLL_FIRST|指定結果集中的第一個資料列。|  
|SQLSRV_SCROLL_LAST|指定結果集中的最後一個資料列。|  
|SQLSRV_SCROLL_ABSOLUTE|指定以*offset*參數指定的資料列。|  
|SQLSRV_SCROLL_RELATIVE|使用目前資料列中的*offset*參數指定指定的資料列。|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>伺服器端資料指標和 SQLSRV 驅動程式  
下列範例顯示各種資料指標的效果。 在範例的第33行中, 您會看到指定不同資料指標的三個查詢語句中的第一個。  其中兩個查詢語句會加上批註。 每次執行程式時, 請使用不同的游標類型, 以查看資料庫更新在第47行的效果。  
  
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
用戶端資料指標是 3.0 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]版中新增的功能, 可讓您在記憶體中快取整個結果集。 使用用戶端資料指標執行查詢後, 可以使用資料列計數。  
  
用戶端資料指標應該用於小型到中型的結果集。 針對大型結果集使用伺服器端資料指標。  
  
如果緩衝區不夠大, 無法保存整個結果集, 則查詢會傳回 false。 您可以將緩衝區大小上限提高到 PHP 記憶體限制。  
  
使用 SQLSRV 驅動程式, 您可以使用[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)的 ClientBufferMaxKBSize 設定來設定保存結果集的緩衝區大小。 [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)會傳回 ClientBufferMaxKBSize 的值。 您也可以使用 sqlsrv 來設定 php .ini 檔案中的緩衝區大小上限。ClientBufferMaxKBSize (例如, sqlsrv。ClientBufferMaxKBSize = 1024)。  
  
下列範例顯示:  
  
-   用戶端資料指標一律可使用資料列計數。  
  
-   用戶端資料指標和批次語句的使用。  
  
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
  
下列範例顯示使用[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)和不同用戶端緩衝區大小的用戶端資料指標。
  
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
  
