---
title: 閒置連接恢復功能
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: ba55069430198661a4454269afd12db6c21bd24d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="idle-connection-resiliency"></a>閒置連接恢復功能
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[連接恢復功能](https://msdn.microsoft.com/library/dn632678.aspx)是，閒置中斷的連線可重新建立，在某些條件約束的原則。 如果在連接到 Microsoft SQL Server 失敗，連接恢復功能可讓用戶端自動嘗試重新建立連線。 連接恢復功能是資料來源; 的屬性只有 SQL Server 2014 及更新版本和 Azure SQL Database 支援連接恢復功能。

連接恢復功能實作與兩個連接關鍵字可加入至連接字串： **ConnectRetryCount**和**ConnectRetryInterval**。

|關鍵字|值|預設值|Description|
|-|-|-|-|
|**ConnectRetryCount**| 介於 0 和 255 之間 （含） 之間的整數|1|嘗試重新建立後才放棄中斷的連線的數目上限。 根據預設，一次進行以重新建立連線時中斷。 值為 0 表示沒有重新連線將會嘗試。|
|**ConnectRetryInterval**| 介於 1 到 60 （含） 之間的整數|1| 時間 （秒），嘗試重新建立連線。 應用程式會嘗試立即重新連線，一旦偵測連線中斷，並將等候**ConnectRetryInterval**秒後再試一次。 這個關鍵字會被忽略，如果**ConnectRetryCount**等於 0。

如果產品的**ConnectRetryCount**乘以**ConnectRetryInterval**大於**LoginTimeout**，則用戶端會停止嘗試一次連接**LoginTimeout**為止; 否則它將會繼續嘗試重新連線，直到**ConnectRetryCount**為止。

#### <a name="remarks"></a>備註

連線閒置時，適用於連接恢復功能。 執行交易，例如，不會觸發重新連線嘗試 – 時所發生的失敗會在失敗因為將會預期。 下列情況下，稱為非可復原的工作階段狀態，不會觸發重新連線嘗試次數：

* 暫存資料表
* 全域和本機資料指標
* 交易內容和工作階段層級的交易鎖定
* 應用程式鎖定
* EXECUTE AS / 還原的安全性內容
* OLE automation 控點
* 已備妥的 XML 控制代碼
* 追蹤旗標

## <a name="example"></a>範例

下列程式碼會連接到資料庫並執行查詢。 終止工作階段中斷連線，並新查詢時會使用中斷的連線。 這個範例會使用[AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx)範例資料庫。

在此範例中，我們會指定緩衝的資料指標之前中斷連接。 如果我們沒有指定的經緩衝處理的資料指標，會不會重新建立連線，因為有作用中的伺服器端資料指標，因此連線不會閒置時中斷。 不過，我們無法在此情況下呼叫 sqlsrv_free_stmt() 之前中斷連線 vacate 資料指標，而且連接會成功重新建立。

```php
<?php
// This function breaks the connection by determining its session ID and killing it.
// A separate connection is used to break the main connection because a session
// cannot kill itself. The sleep() function ensures enough time has passed for KILL
// to finish ending the session.
function BreakConnection( $conn, $conn_break )
{
    $stmt1 = sqlsrv_query( $conn, "SELECT @@SPID" );
    if ( sqlsrv_fetch( $stmt1 ) )
    {
        $spid=sqlsrv_get_field( $stmt1, 0 );
    }

    $stmt2 = sqlsrv_prepare( $conn_break, "KILL ".$spid );
    sqlsrv_execute( $stmt2 );
    sleep(1);
}

// Connect to the local server using Windows authentication and specify
// AdventureWorks as the database in use. Specify values for
// ConnectRetryCount and ConnectRetryInterval as well.
$databaseName = 'AdventureWorks2014';
$serverName = '(local)';
$connectionInfo = array( "Database"=>$databaseName, "ConnectRetryCount"=>10, "ConnectRetryInterval"=>10 );

$conn = sqlsrv_connect( $serverName, $connectionInfo );
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}

// A separate connection that will be used to break the main connection $conn
$conn_break = sqlsrv_connect( $serverName, array( "Database"=>$databaseName) );

// Create a statement to retrieve the contents of a table
$stmt1 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Employee",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt1 === false )
{
     echo "Error in statement 1.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 1 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt1 );
    echo $rowcount." rows in result set.\n";
}

// Now break the connection $conn
BreakConnection( $conn, $conn_break );

// Create another statement. The connection will be reestablished.
$stmt2 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Department",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt2 === false )
{
     echo "Error in statement 2.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 2 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt2 );
    echo $rowcount." rows in result set.\n";
}

sqlsrv_close( $conn );
sqlsrv_close( $conn_break );
?>
```
預期的輸出：
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>另請參閱
[Windows ODBC 驅動程式中的連接恢復功能](https://docs.microsoft.com/en-us/sql/connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver)
