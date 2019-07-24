---
title: Azure Active Directory |Microsoft Docs
ms.date: 02/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- azure active directory, authentication, access token
author: david-puglielli
ms.author: v-dapugl
manager: v-mabarw
ms.openlocfilehash: 8712681a244e969d230b0b7099acd4aa56334f11
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265182"
---
# <a name="connect-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證進行連線
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)(Azure AD) 是一種中央使用者識別碼管理技術, 可做為[SQL Server 驗證](../../connect/php/how-to-connect-using-sql-server-authentication.md)的替代方式來運作。 Azure AD 可讓您使用使用者名稱和密碼、Windows 整合式驗證或 Azure AD 存取權杖, 透過 Azure AD 中的同盟身分識別來連接 Microsoft Azure SQL Database 和 SQL 資料倉儲。 適用于 SQL Server 的 PHP 驅動程式會提供這些功能的部分支援。

若要使用 Azure AD, 請使用**Authentication**或**AccessToken**關鍵字 (它們是互斥的), 如下表所示。 如需更多的技術詳細資料, 請參閱[使用 Azure Active Directory 搭配 ODBC 驅動程式](../../connect/odbc/using-azure-active-directory.md)。

|關鍵字|值|Description|
|-|-|-|
|**AccessToken**|未設定 (預設值)|由其他關鍵字決定的驗證模式。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。 |
||位元組字串|從 OAuth JSON 回應中解壓縮的 Azure AD 存取權杖。 連接字串不能包含使用者識別碼、密碼或驗證關鍵字 (在 Linux 或 macOS 中需要 ODBC 驅動程式17版或更新版本)。 |
|**驗證**|未設定 (預設值)|由其他關鍵字決定的驗證模式。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。 |
||`SqlPassword`|使用使用者名稱和密碼, 直接向 SQL Server 實例 (可能是 Azure 實例) 進行驗證。 使用者名稱和密碼必須使用**UID**和**PWD**關鍵字傳遞至連接字串。 |
||`ActiveDirectoryPassword`|使用使用者名稱和密碼, 以 Azure Active Directory 身分識別進行驗證。 使用者名稱和密碼必須使用**UID**和**PWD**關鍵字傳遞至連接字串。 |
||`ActiveDirectoryMsi`|使用系統指派的受控識別或使用者指派的受控識別 (需要17.3.1.1 或更新版本的 ODBC 驅動程式) 來進行驗證。 如需總覽和教學課程, 請參閱[什麼是適用于 Azure 資源的受控識別？](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)。|

**驗證**關鍵字會影響連接安全性設定。 如果是在連接字串中設定, 則**Encrypt**關鍵字會預設為 true, 表示用戶端會要求加密。 此外, 除非 [ **TrustServerCertificate** ] 設定為 [true] (預設**為 false** ), 否則無論加密設定是否都會驗證伺服器憑證。 這項功能與舊版、較不安全的登入方法有區別, 只有在連接字串中特別要求加密時, 才會驗證伺服器憑證。

在 Windows 上搭配 PHP 驅動程式 for SQL Server 使用 Azure AD 時, 可能會要求您安裝[Microsoft Online Services 登入](https://www.microsoft.com/download/details.aspx?id=41950)小幫手 (ODBC 17 + 不需要)。

#### <a name="limitations"></a>限制

在 Windows 上, 基礎 ODBC 驅動程式支援更多一個 ActiveDirectoryIntegrated**驗證**關鍵字的  值, 但 PHP 驅動程式不支援任何平臺上的此值。

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>範例-使用 SqlPassword 和 ActiveDirectoryPassword 進行連接

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = array("UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword');

$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=SqlPassword.\n";
    sqlsrv_close($conn);
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = array("Database"=>$azureDatabase,
                        "UID"=>$azureUsername,
                        "PWD"=>$azurePassword,
                        "Authentication"=>'ActiveDirectoryPassword');

$conn = sqlsrv_connect($azureServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    sqlsrv_close($conn);
}

?>
```

## <a name="example---connect-using-the-pdosqlsrv-driver"></a>範例-使用 PDO_SQLSRV 驅動程式進行連接

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

try {
    $conn = new PDO("sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword);
    echo "Connected successfully with Authentication=SqlPassword.\n";
    $conn = null;
} catch (PDOException $e) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword);
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-azure-ad-access-token"></a>範例-使用 Azure AD 存取權杖進行連接

### <a name="sqlsrv-driver"></a>SQLSRV 驅動程式

```php
<?php
// Using an access token to connect: do not use UID or PWD connection options
// Assume $accToken is the valid byte string extracted from an OAuth JSON response
$connectionInfo = array("Database"=>$azureAdDatabase, "AccessToken"=>$accToken);
$conn = sqlsrv_connect($azureAdServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Azure AD Access Token.\n";
    sqlsrv_close($conn);
}
?>
```

### <a name="pdosqlsrv-driver"></a>PDO_SQLSRV 驅動程式

```php
<?php
try {
    // Using an access token to connect: do not pass in $uid or $pwd
    // Assume $accToken is the valid byte string extracted from an OAuth JSON response
    $connectionInfo = "Database = $azureAdDatabase; AccessToken = $accToken;";
    $conn = new PDO("sqlsrv:server = $azureAdServer; $connectionInfo");
    echo "Connected successfully with Azure AD Access Token\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>範例-使用適用于 Azure 資源的受控識別進行連線

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>搭配使用系統指派的受控識別與 SQLSRV 驅動程式

使用系統指派的受控識別進行連接時, 請勿使用 UID 或 PWD 選項。

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$connectionInfo = array('Database'=>$azureDatabase,
                        'Authentication'=>'ActiveDirectoryMsi');
$conn = sqlsrv_connect($azureServer, $connectionInfo);

if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    $stmt = sqlsrv_query($conn, $tsql);
    if ($stmt === false) {
        echo "Failed to run the simple query (system-assigned).\n";
        print_r(sqlsrv_errors());
    } else {
        while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
            echo $row['SQL_VERSION'] . PHP_EOL;
        }

        sqlsrv_free_stmt($stmt);
    }
    
    sqlsrv_close($conn);
}
?>
```

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>將使用者指派的受控識別與 PDO_SQLSRV 驅動程式搭配使用

使用者指派的受控識別會建立為獨立的 Azure 資源。 Azure 會在所使用的訂用帳戶所信任的 Azure AD 租使用者中建立身分識別。 建立身分識別之後, 即可將身分識別指派給一或多個 Azure 服務實例。 `Object ID`複製此身分識別的, 並將它設定為連接字串中的使用者名稱。 

因此, 使用使用者指派的受控識別進行連線時, 請提供物件識別碼做為使用者名稱, 但省略密碼。

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$azureUser = '2d68f56e-9547-4dae-aee8-f3g28ab9674x';    // Object ID of the identity
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryMsi;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer; $connectionInfo", $azureUser);
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    
    try {
        $stmt = $conn->query($tsql);
        $result = $stmt->fetchall(PDO::FETCH_ASSOC);
        print_r($result);

        unset($stmt);
    } catch (PDOException $e) {
        echo "Failed to run the simple query (user-assigned).\n";
    }
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="see-also"></a>另請參閱
[搭配 ODBC 驅動程式使用 Azure Active Directory](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)

[什麼是適用于 Azure 資源的受控識別？](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
