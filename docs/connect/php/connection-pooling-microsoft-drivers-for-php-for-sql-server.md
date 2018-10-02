---
title: 連線共用 (Microsoft Drivers for PHP for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e6dc56d020af182d657ec2766d996601e5442686
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624986"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>連接共用 (Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

以下是對於 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]中的連接共用所須注意的相關要點：  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會使用 ODBC 連接共用。  
  
-   依預設會在 Windows 中啟用連線共用。 在 Linux 和 macOS，來共用連接啟用設定 odbc 連接共用時才 (請參閱[啟用/停用連線共用](#enablingdisabling-connection-pooling))。 當啟用連接共用，並連接到伺服器時，驅動程式會嘗試使用共用的連接，然後再建立一個新。 如果在集區中找不到等同的連接，則會建立新連接，並加入至集區。 驅動程式會根據連接字串的比較，來判斷連接是否相等。  
  
-   使用來自集區的連接時，連接狀態會重設。  
  
-   關閉連接會將連接傳回集區。  
  
如需連接共用的詳細資訊，請參閱[驅動程式管理員連線共用](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="enablingdisabling-connection-pooling"></a>啟用/停用連接共用
### <a name="windows"></a>Windows
您可以將連接字串的 *ConnectionPooling* 屬性值設定為 **false** (或 0)，以強制驅動程式建立新連線 (而不是在連線集區中尋找相同的連線)。  
  
如果在連接字串中省略 *ConnectionPooling* 屬性，或是將該屬性設定為 **true** (或 1)，則只有在連線集區中沒有相同的連線存在時，驅動程式才會建立新的連線。  
  
如需其他連接屬性的相關資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
### <a name="linux-and-macos"></a>Linux 和 macOS
*ConnectionPooling*屬性不能啟用/停用連接共用。 

連接共用可以啟用/停用編輯 odbcinst.ini 組態檔。 驅動程式應重新載入，變更才會生效。

設定`Pooling`要`Yes`和 正`CPTimeout`odbcinst.ini 檔案中的值會啟用連接共用。 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
  
最低限度，odbcinst.ini 檔案看起來應該類似此範例：

```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
Description=Microsoft ODBC Driver 13 for SQL Server
Driver=/opt/microsoft/msodbcsql/lib64/libmsodbcsql-13.1.so.3.0
UsageCount=1
CPTimeout=120
```

設定`Pooling`至`No`在 odbcinst.ini 檔案會強制驅動程式建立新的連接。
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>Remarks
- 在 Linux 或 macOS 上，如果共用已啟用在 odbcinst.ini 檔案會共用所有連線。 這表示 ConnectionPooling 連接選項沒有任何作用。 若要停用共用，將 共用 = No odbcinst.ini 檔案中的，然後重新載入驅動程式。
  - unixODBC < = 2.3.4 （Linux 和 macOS） 可能不會傳回適當的診斷資訊，例如錯誤訊息、 警告和參考訊息
  - 基於這個理由，SQLSRV 和 PDO_SQLSRV 驅動程式可能無法正確地擷取長資料 （例如 xml、 二進位)，為字串。 因應措施的資料流的形式，就可以擷取長的資料。 針對 SQLSRV，請參閱下面的範例。

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
[如何：使用 Windows 驗證進行連線](../../connect/php/how-to-connect-using-windows-authentication.md)

[如何：使用 SQL Server 驗證進行連線](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
