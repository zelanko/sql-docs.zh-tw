---
title: 閒置連線恢復功能
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: a2361c8a2e8cbc709d50a9139678a08e2e850e2d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62522026"
---
# <a name="idle-connection-resiliency"></a>閒置連線恢復功能
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[連接恢復功能](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)是，中斷閒置連接在重新建立，在某些條件約束的準則。 如果 Microsoft SQL Server 的連線失敗，連接恢復功能可讓用戶端嘗試自動重新建立連線。 連接恢復功能是資料來源的屬性只有 SQL Server 2014 及更新版本和 Azure SQL Database 支援連接恢復功能。

連接恢復功能透過兩個連接關鍵字可加入至連接字串中實作： **ConnectRetryCount**並**ConnectRetryInterval**。

|關鍵字|值|預設|描述|
|-|-|-|-|
|**ConnectRetryCount**| 介於 0 和 255 (含) 之間的整數|1|若要重新建立放棄之前中斷的連線的嘗試次數上限。 根據預設，單一嘗試重新建立連線時中斷。 值 0 表示沒有重新連線將會嘗試。|
|**ConnectRetryInterval**| 介於 1 和 60 (含) 之間的整數|1| 時間 （秒），嘗試重新建立連線。 應用程式會嘗試立即重新連線，一旦偵測連線中斷，並接著將會等候**ConnectRetryInterval**秒後再試一次。 如果，則會忽略這個關鍵字**ConnectRetryCount**等於 0。

如果的乘積**ConnectRetryCount**乘以**ConnectRetryInterval**大於**LoginTimeout**，則用戶端將會停止嘗試一次連線**LoginTimeout**為止; 否則它會繼續嘗試重新連線到**ConnectRetryCount**為止。

#### <a name="remarks"></a>備註

當連線處於閒置狀態時，適用於連接恢復功能。 失敗發生時執行的交易，例如，將不會觸發重新連線嘗試次數-它們會失敗，因為預期。 下列情況下，稱為無法復原的工作階段狀態，將不會觸發重新連線嘗試：

* 暫存資料表
* 全域和本機資料指標
* 交易內容 」 和 「 工作階段層級的交易鎖定
* 應用程式鎖定
* EXECUTE AS / 還原的安全性內容
* OLE automation 的控制代碼
* 備妥的 XML 控制代碼
* 追蹤旗標

## <a name="example"></a>範例

下列程式碼連接到資料庫，並執行查詢。 藉由刪除工作階段中斷連線，新的查詢會嘗試使用中斷的連線。 這個範例會使用 [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) 範例資料庫。

在此範例中，我們會指定緩衝的資料指標之前中斷連接。 如果我們未指定緩衝的資料指標，就不會重新建立連線因為會有作用中的伺服器端資料指標，因此不會連線閒置時中斷。 不過，我們可以在此情況下呼叫 sqlsrv_free_stmt() 之前中斷連線 vacate 資料指標，而且連接會成功重新建立。

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
預期輸出：
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>另請參閱
[Windows ODBC 驅動程式中的連接恢復功能](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
