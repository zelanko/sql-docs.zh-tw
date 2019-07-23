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
manager: v-mabarw
ms.openlocfilehash: 3edba0cde94d8661eed053319142ce7f84a70613
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265172"
---
# <a name="idle-connection-resiliency"></a>閒置連線恢復功能
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[連接復原](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)是指在某些條件約束中, 可以重新建立中斷的閒置連線的原則。 如果 Microsoft SQL Server 的連線失敗, 連接恢復功能可讓用戶端自動嘗試重新建立連線。 連接復原是資料來源的屬性;只有 SQL Server 2014 和更新版本, 且 Azure SQL Database 支援連接恢復功能。

使用可新增至連接字串的兩個連接關鍵字來執行連接復原: **ConnectRetryCount**和**ConnectRetryInterval**。

|關鍵字|值|預設|Description|
|-|-|-|-|
|**ConnectRetryCount**| 介於 0 和 255 (含) 之間的整數|1|在放棄之前重新建立中斷連接的最大嘗試次數。 根據預設, 會嘗試在中斷時重新建立連接。 值為0表示不會嘗試重新連接。|
|**ConnectRetryInterval**| 介於 1 和 60 (含) 之間的整數|1| 嘗試重新建立連接之間的時間 (以秒為單位)。 應用程式會在偵測到連線中斷時立即嘗試重新連線, 然後等待**ConnectRetryInterval**秒後再試一次。 如果**ConnectRetryCount**等於 0, 則會忽略這個關鍵字。

如果**ConnectRetryCount**乘以**ConnectRetryInterval**的乘積大於**LoginTimeout**, 則用戶端會在達到**LoginTimeout**之後停止嘗試連接;否則, 它會繼續嘗試重新連線, 直到達到**ConnectRetryCount**為止。

#### <a name="remarks"></a>Remarks

連接閒置時, 會套用連線恢復功能。 例如, 執行交易時所發生的失敗, 將不會觸發重新連線嘗試, 否則將會失敗, 否則會是預期的。 下列情況 (又稱為無法復原的會話狀態) 將不會觸發重新連線嘗試:

* 暫存資料表
* 全域和本機資料指標
* 交易內容和工作階段層級交易鎖定
* 應用程式鎖定
* 執行身分/還原安全性內容
* OLE automation 控制碼
* 備妥的 XML 控制碼
* 追蹤旗標

## <a name="example"></a>範例

下列程式碼會連接到資料庫並執行查詢。 中斷會話並嘗試使用中斷連接來執行新的查詢, 以中斷連接。 這個範例會使用 [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) 範例資料庫。

在此範例中, 我們會在中斷連接之前指定緩衝的資料指標。 如果沒有指定緩衝的資料指標, 就不會重新建立連接, 因為會有使用中的伺服器端資料指標, 因此當中斷時, 連接就不會處於閒置狀態。 不過, 在這種情況下, 我們可以先呼叫 sqlsrv_free_stmt (), 再中斷連接以 vacate 資料指標, 並成功重新建立連接。

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
