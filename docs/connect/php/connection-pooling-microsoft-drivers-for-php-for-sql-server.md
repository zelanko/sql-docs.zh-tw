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
ms.openlocfilehash: 13e1075cd25fa352543837afa31ff2a3d540704f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015117"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>連接共用 (Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

以下是對於 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]中的連接共用所須注意的相關要點：  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會使用 ODBC 連接共用。  
  
-   依預設會在 Windows 中啟用連線共用。 在 Linux 和 macOS 中, 只有在已啟用 ODBC 的連接共用時, 才會共用連接 (請參閱[啟用/停用連接](#enablingdisabling-connection-pooling)共用)。 當連接共用已啟用且您連線到伺服器時, 驅動程式會先嘗試使用共用的連線, 再建立新的連接。 如果在集區中找不到等同的連接，則會建立新連接，並加入至集區。 驅動程式會根據連接字串的比較，來判斷連接是否相等。  
  
-   使用來自集區的連接時，連接狀態會重設。  
  
-   關閉連接會將連接傳回集區。  
  
如需連接共用的詳細資訊，請參閱[驅動程式管理員連線共用](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="enablingdisabling-connection-pooling"></a>啟用/停用連接共用
### <a name="windows"></a>Windows
您可以將連接字串的 *ConnectionPooling* 屬性值設定為 **false** (或 0)，以強制驅動程式建立新連線 (而不是在連線集區中尋找相同的連線)。  
  
如果在連接字串中省略 *ConnectionPooling* 屬性，或是將該屬性設定為 **true** (或 1)，則只有在連線集區中沒有相同的連線存在時，驅動程式才會建立新的連線。  
  
如需其他連接屬性的相關資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
### <a name="linux-and-macos"></a>Linux 與 macOS
*ConnectionPooling*屬性不能用來啟用/停用連接共用。 

藉由編輯 odbcinst 的設定檔, 可以啟用/停用連接共用。 必須重載驅動程式, 變更才會生效。

將`Pooling`設定`Yes`為, 而且`CPTimeout` odbcinst 中的正值會啟用連接共用。 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
  
Odbcinst .ini 檔案至少應該看起來像下列範例:

```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
Description=Microsoft ODBC Driver 13 for SQL Server
Driver=/opt/microsoft/msodbcsql/lib64/libmsodbcsql-13.1.so.3.0
UsageCount=1
CPTimeout=120
```

將`Pooling` odbcinst `No`中的設定為, 會強制驅動程式建立新的連接。
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>Remarks
- 在 Linux 或 macOS 中, 如果已在 odbcinst 中啟用共用, 所有連線都會共用。 這表示 ConnectionPooling 連接選項沒有任何作用。 若要停用共用, 請在 odbcinst 中設定 Pooling = No, 然後重載驅動程式。
  - unixODBC < = 2.3.4 (Linux 和 macOS) 可能不會傳回適當的診斷資訊, 例如錯誤訊息、警告和資訊訊息
  - 基於這個理由, SQLSRV 和 PDO_SQLSRV 驅動程式可能無法正確提取長資料 (例如 xml、二進位) 做為字串。 較長的資料可以當做因應措施的資料流程來提取。 針對 SQLSRV，請參閱下面的範例。

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
  
