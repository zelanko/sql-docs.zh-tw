---
title: 閒置連線恢復功能
description: 了解什麼是閒置連線復原，以及它在 Microsoft Drivers for PHP for SQL Server 中的運作方式。
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b425d57a0b1aee0c01db62d3fd1b77eb59c8aed
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632948"
---
# <a name="idle-connection-resiliency"></a>閒置連線恢復功能
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[連線復原](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)是在特定限制內，能夠重新建立中斷閒置連線的準則。 如果對 Microsoft SQL Server 的連線失敗，連線復原會允許用戶端自動嘗試重新建立連線。 連線復原是資料來源的屬性；SQL Server 2014 和更新版本，以及 Azure SQL Database 才支援連線復原。

連線復原是使用兩個可新增至連接字串的連接關鍵字來實作：**ConnectRetryCount** 和 **ConnectRetryInterval**。

|關鍵字|值|預設|描述|
|-|-|-|-|
|**ConnectRetryCount**| 介於 0 和 255 (含) 之間的整數|1|重新建立已中斷連線的嘗試次數上限，超過即放棄。 根據預設，系統會在連線中斷時嘗試重新建立一次。 值為 0 表示不會嘗試重新連線。|
|**ConnectRetryInterval**| 介於 1 和 60 (含) 之間的整數|1| 重新建立連線嘗試的間隔時間 (以秒為單位)。 應用程式會在偵測到連線中斷時立即嘗試重新連線，然後等候 **ConnectRetryInterval** 秒後再試一次。 如果 **ConnectRetryCount** 等於 0，則會忽略此關鍵字。

如果 **ConnectRetryCount** 乘以 **ConnectRetryInterval** 的積大於 **LoginTimeout**，則用戶端會在達到 **LoginTimeout** 時停止嘗試連線；否則，會繼續嘗試重新連線，直到達到 **ConnectRetryCount** 為止。

#### <a name="remarks"></a>備註

連線復原適用於連線閒置的時候。 例如，執行交易時發生的失敗不會觸發重新連線嘗試 - 其本應該在此情況失敗。 下列情況 (又稱為無法復原工作階段狀態) 將不會觸發重新連線嘗試：

* 暫存資料表
* 全域和本機資料指標
* 交易內容與工作階段層級交易鎖定
* 應用程式鎖定
* EXECUTE AS/REVERT 資訊安全內容
* OLE 自動化控制代碼
* 已備妥的 XML 控制代碼
* 追蹤旗標

## <a name="example"></a>範例

下列程式碼會連線到資料庫並執行查詢。 該連線會藉由終止工作階段來中斷，然後嘗試使用已中斷的連線執行新查詢。 這個範例會使用 [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) 範例資料庫。

在此範例中，我們會在中斷連線之前，指定緩衝資料指標。 如果沒有指定緩衝資料指標，就不會重新建立連線，因為會有使用中的伺服器端資料指標，所以當中斷時，連線就不會進入閒置狀態。 不過，在該情況下，我們可以在中斷連線之前，先呼叫 sqlsrv_free_stmt() 以空出資料指標，然後就能成功重新建立連線。

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
