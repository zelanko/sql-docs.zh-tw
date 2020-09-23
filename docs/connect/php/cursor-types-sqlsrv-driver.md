---
title: 資料指標類型 (SQLSRV 驅動程式)
description: 了解如何透過 Microsoft Drivers for PHP for SQL Server 使用游標類型建立可依任何順序存取的結果集。
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e72381eed4aa89ccd9656d3eabadb22bccd357d
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411464"
---
# <a name="cursor-types-sqlsrv-driver"></a>資料指標類型 (SQLSRV 驅動程式)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQLSRV 驅動程式可讓您根據資料指標類型，建立能夠以任何順序存取資料列的結果集。  此主題將討論用戶端 (緩衝) 與伺服器端 (未緩衝) 的資料指標。  
  
## <a name="cursor-types"></a>資料指標類型  
當您搭配 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 建立結果集時，您可以指定資料指標的類型。 根據預設，會使用順向資料指標，其可讓您從結果集的第一個資料列開始，一次移動一個資料列，直到您抵達結果集的結尾為止。  
  
您可以搭配可捲動的資料指標建立結果集，其可讓您以任何順序存取結果集中的任何資料列。 下表列出可傳遞至 sqlsrv_query 或 sqlsrv_prepare 中 **Scrollable** 選項的值。  
  
|選項|描述|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|讓您從結果集的第一個資料列開始，一次移動一個資料列，直到您抵達結果集的結尾為止。<br /><br />此為預設的資料指標類型。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) 會針對搭配此資料指標類型所建立的結果集傳回錯誤。<br /><br />**forward** 是 SQLSRV_CURSOR_FORWARD 的縮寫格式。|  
|SQLSRV_CURSOR_STATIC|讓您以任何順序存取資料列，但將不會反映資料庫中的變更。<br /><br />**static** 是 SQLSRV_CURSOR_STATIC 的縮寫格式。|  
|SQLSRV_CURSOR_DYNAMIC|讓您以任何順序存取資料列，且會反映資料庫中的變更。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) 會針對搭配此資料指標類型所建立的結果集傳回錯誤。<br /><br />**dynamic** 是 SQLSRV_CURSOR_DYNAMIC 的縮寫格式。|  
|SQLSRV_CURSOR_KEYSET|讓您以任何順序存取資料列。 不過，如果資料列已從資料表中刪除，則索引鍵集資料指標不會更新資料列計數 (已刪除的資料列傳回時不會有值)。<br /><br />**keyset** 是 SQLSRV_CURSOR_KEYSET 的縮寫格式。|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|讓您以任何順序存取資料列。 建立用戶端資料指標查詢。<br /><br />**buffered** 是 SQLSRV_CURSOR_CLIENT_BUFFERED 的縮寫格式。|  
  
如果查詢會產生多個結果集，**Scrollable** 選項便會套用到所有結果集。  
  
## <a name="selecting-rows-in-a-result-set"></a>選取結果集中的資料列  
在您建立結果集之後，您可以使用 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)、[sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) 或 [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) 來指定資料列。  
  
下表描述可在 *row* 參數中指定的值。  
  
|參數|描述|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|指定下一個資料列。 此為您不針對可捲動的結果集指定 *row* 參數，這便會是預設值。|  
|SQLSRV_SCROLL_PRIOR|指定目前資料列之前的資料列。|  
|SQLSRV_SCROLL_FIRST|指定結果集中的第一個資料列。|  
|SQLSRV_SCROLL_LAST|指定結果集中的最後一個資料列。|  
|SQLSRV_SCROLL_ABSOLUTE|指定搭配 *offset* 參數指定的資料列。|  
|SQLSRV_SCROLL_RELATIVE|指定從目前資料列算起搭配 *offset* 參數指定的資料列。|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>伺服器端資料指標和 SQLSRV 驅動程式  
下列範例示範各種資料指標的效果。 在範例的行 33 上，您會看見指定不同資料指標的三個查詢陳述式中的第一個。  兩個查詢陳述式已加上註解。 每當您執行程式時，請使用不同的資料指標類型來在行 47 上查看資料庫更新的效果。  
  
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
用戶端資料指標為在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3.0 版中新增的功能，其讓您能夠在記憶體中快取整個結果集。 使用用戶端資料指標時，可在執行查詢之後使用資料列計數。  
  
用戶端資料指標應該用於小型到中型的結果集。 請針對大型結果集使用伺服器端資料指標。  
  
如果緩衝區因為不夠大而無法保存整個結果集，查詢將會傳回 false。 您可以將緩衝區大小上限提高到 PHP 記憶體限制。  
  
透過使用 SQLSRV 驅動程式，您可以使用 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) 的 ClientBufferMaxKBSize 設定來設定保存結果集的緩衝區大小。 [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md) 會傳回 ClientBufferMaxKBSize 的值。 您也可以在 php.ini 檔案中使用 sqlsrv.ClientBufferMaxKBSize 來設定緩衝區大小上限 (例如 sqlsrv.ClientBufferMaxKBSize = 1024)。  
  
下列範例顯示︰  
  
-   資料列計數一律可搭配用戶端資料指標使用。  
  
-   用戶端資料指標和批次陳述式的使用。  
  
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
  
下列範例顯示使用 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 和不同用戶端緩衝區大小的用戶端資料指標。
  
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
  
