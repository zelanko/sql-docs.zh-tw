---
title: 連接共用 (Microsoft Drivers for PHP for SQL Server)
description: 深入了解使用 Microsoft Driver for PHP for SQL Server 時的連線共用，以及此體驗在不同的作業系統上可能有哪些差異。
ms.custom: ''
ms.date: 08/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 147e744a69850a5c76b9706c03a96fa67d2efb5f
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435268"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>連接共用 (Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

以下是對於 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]中的連接共用所須注意的相關要點：  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會使用 ODBC 連接共用。  
  
-   依預設會在 Windows 中啟用連線共用。 在 Linux 與 macOS 中，只有在已針對 ODBC 啟用連線共用時才會共用連線 (請參閱[啟用/停用連線共用](#enablingdisabling-connection-pooling))。 當連線共用已啟用且您連線到伺服器時，驅動程式會在建立新連線之前先嘗試使用共用連線。 如果在集區中找不到等同的連接，則會建立新連接，並加入至集區。 驅動程式會根據連接字串的比較，來判斷連接是否相等。  
  
-   使用來自集區的連線時，連線狀態會重設 (僅限 Windows)。  
  
-   關閉連接會將連接傳回集區。  
  
如需連接共用的詳細資訊，請參閱[驅動程式管理員連線共用](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="enablingdisabling-connection-pooling"></a>啟用/停用連線共用
### <a name="windows"></a>Windows
您可以將連接字串的 *ConnectionPooling* 屬性值設定為 **false** (或 0)，以強制驅動程式建立新連線 (而不是在連線集區中尋找相同的連線)。  
  
如果在連接字串中省略 *ConnectionPooling* 屬性，或是將該屬性設定為 **true** (或 1)，則只有在連線集區中沒有相同的連線存在時，驅動程式才會建立新的連線。  

> [!NOTE]  
> 依預設會啟用 Multiple Active Result Set (MARS)。 如果同時使用了 MARS 和共用，為了讓 MARS 能夠正常運作，驅動程式需要較長的時間來重設*第一個*查詢的連線，因此會忽略任何指定的查詢逾時。 不過，查詢逾時設定將在後續的查詢中生效。
  
如有必要，請參閱[如何：停用 Multiple Active Resultsets (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)。 如需其他連接屬性的相關資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  

### <a name="linux-and-macos"></a>Linux 與 macOS
*ConnectionPooling* 屬性無法用來啟用/停用連線共用。 

您可以透過編輯 odbcinst.ini 設定檔來啟用/停用連線共用。 必須重新載入驅動程式，變更才會生效。

在 odbcinst.ini 檔案中將 `Pooling` 設定為 `Yes`，並使用正 `CPTimeout` 值，即可啟用連線共用。 
```
[ODBC]
Pooling=Yes

[ODBC Driver 17 for SQL Server]
CPTimeout=<int value>
```
  
odbcinst.ini 檔案看起來至少要像下面的範例一樣：

```
[ODBC]
Pooling=Yes

[ODBC Driver 17 for SQL Server]
Description=Microsoft ODBC Driver 17 for SQL Server
Driver=/opt/microsoft/msodbcsql17/lib64/libmsodbcsql-17.5.so.2.1
UsageCount=1
CPTimeout=120
```

將 odbcinst.ini 檔案中的 `Pooling` 設定為 `No` 可強制驅動程式建立新連線。
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>備註
- 在 Linux 或 macOS 中，不建議將連線共用使用於 2.3.7 之前的 unixODBC。 如果已在 odbcinst.ini 檔案中啟用共用，即表示 ConnectionPooling 連線選項沒有作用，因此所有連線都會共用。 若要停用共用，請在 odbcinst.ini 檔案中設定 Pooling=No，然後重新載入驅動程式。 
  - unixODBC <= 2.3.4 (Linux 與 macOS) 可能不會傳回適當的診斷資訊，例如錯誤訊息、警告與資訊訊息
  - 基於此理由，SQLSRV 與 PDO_SQLSRV 驅動程式可能無法正確地以字串形式擷取長資料 (例如 xml、binary)。 作為因應措施，長資料能以資料流的方式擷取。 針對 SQLSRV，請參閱下面的範例。

```
<?php
$connectionInfo = array("Database"=>"test", "UID"=>"username", "PWD"=>"password");

$conn1 = sqlsrv_connect("servername", $connectionInfo);

$longSample = str_repeat("a", 8500);
$xml1 = 
'<ParentXMLTag>
  <ChildTag01>'.$longSample.'</ChildTag01>
</ParentXMLTag>';

// Create table and insert xml string into it
sqlsrv_query($conn1, "CREATE TABLE xml_table (field xml)");
sqlsrv_query($conn1, "INSERT into xml_table values ('$xml1')");

// retrieve the inserted xml
$column1 = getColumn($conn1);

// return the connection to the pool
sqlsrv_close($conn1);

// This connection is from the pool
$conn2 = sqlsrv_connect("servername", $connectionInfo);
$column2 = getColumn($conn2);

sqlsrv_query($conn2, "DROP TABLE xml_table");
sqlsrv_close($conn2);

function getColumn($conn)
{
    $tsql = "SELECT * from xml_table";
    $stmt = sqlsrv_query($conn, $tsql);
    sqlsrv_fetch($stmt);
    // This might fail in Linux and macOS
    // $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    // The workaround is to fetch it as a stream
    $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));
    sqlsrv_free_stmt($stmt);
    return ($column);
}
?>
```


## <a name="see-also"></a>另請參閱  
[如何：使用 Windows 驗證進行連接](../../connect/php/how-to-connect-using-windows-authentication.md)

[操作說明：使用 SQL Server 驗證進行連線](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
