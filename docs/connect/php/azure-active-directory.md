---
title: Azure Active Directory
description: 了解如何搭配 Microsoft Drivers for PHP for SQL Server 使用 Azure Active Directory 驗證。
ms.date: 02/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- azure active directory, authentication, access token
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac1e598b5599caa9020ed795d1bffd185887ad76
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81625458"
---
# <a name="connect-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證進行連線
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) \(英文\) 是一種中央使用者識別碼管理技術，可作為 [SQL Server 驗證](how-to-connect-using-sql-server-authentication.md)的替代方案。 Azure AD 允許您使用使用者名稱與密碼、Windows 整合式驗證或 Azure AD 存取權杖，透過 Azure AD 中的同盟識別身分來連線到 Microsoft Azure SQL Database 與 SQL 資料倉儲。 PHP Drivers for SQL Server 會提供這些功能的部分支援。

若要使用 Azure AD，請使用 **Authentication** 或 **AccessToken** 關鍵字 (它們彼此互斥)，如下表所示。 如需更多的技術詳細資料，請參閱[搭配 ODBC 驅動程式使用 Azure Active Directory](../odbc/using-azure-active-directory.md)。

|關鍵字|值|描述|
|-|-|-|
|**AccessToken**|未設定 (預設值)|由其他關鍵字決定的驗證模式。 如需詳細資訊，請參閱 [Connection Options](connection-options.md)。 |
||位元組字串|從 OAuth JSON 回應中擷取的 Azure AD 存取權杖。 連接字串不能包含使用者識別碼、密碼或驗證關鍵字 (在 Linux 或 macOS 中需要 ODBC 驅動程式 17 版或更新版本)。 |
|**驗證**|未設定 (預設值)|由其他關鍵字決定的驗證模式。 如需詳細資訊，請參閱 [Connection Options](connection-options.md)。 |
||`SqlPassword`|利用使用者名稱與密碼直接向 SQL Server 執行個體 (可能是 Azure 執行個體) 進行驗證。 使用者名稱與密碼必須使用 **UID** 和 **PWD** 關鍵字，傳遞至連接字串。 |
||`ActiveDirectoryPassword`|利用使用者名稱與密碼，以 Azure Active Directory 身分識別進行驗證。 使用者名稱與密碼必須使用 **UID** 和 **PWD** 關鍵字，傳遞至連接字串。 |
||`ActiveDirectoryMsi`|使用系統指派的受控識別或使用者指派的受控識別 (需要 17.3.1.1 版或更新版本的 ODBC 驅動程式) 來進行驗證。 如需概觀和教學課程，請參閱[什麼是適用於 Azure 資源的受控識別？](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) \(英文\)。|

**Authentication** 關鍵字會影響連線安全性設定。 如果是在連接字串中設定，則根據預設，**Encrypt** 關鍵字會設定為 true，這表示用戶端會要求加密。 此外，除非 **TrustServerCertificate** 設定為 true (預設為 **false**)，否則無論加密設定如何，都將會驗證伺服器憑證。 這項功能與舊版、較不安全的登入方法有區別，只有在連接字串中特別要求加密時，才會驗證伺服器憑證。

#### <a name="limitations"></a>限制

在 Windows 上，底層 ODBC 驅動程式針對 **Authentication** 關鍵字還支援另一個值 **ActiveDirectoryIntegrated**，但 PHP 驅動程式在任何平台上都不支援此值。

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>範例 - 使用 SqlPassword 和 ActiveDirectoryPassword 進行連線

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

## <a name="example---connect-using-the-pdo_sqlsrv-driver"></a>範例 - 使用 PDO_SQLSRV 驅動程式進行連線

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

## <a name="example---connect-using-azure-ad-access-token"></a>範例 - 使用 Azure AD 存取權杖進行連線

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

### <a name="pdo_sqlsrv-driver"></a>PDO_SQLSRV 驅動程式

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

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>範例 - 使用適用於 Azure 資源的受控識別進行連線

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>搭配 SQLSRV 驅動程式使用系統指派的受控識別

使用系統指派的受控識別進行連線時，請勿使用 [UID] 或 [PWD] 選項。

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

### <a name="using-the-user-assigned-managed-identity-with-pdo_sqlsrv-driver"></a>搭配 PDO_SQLSRV 驅動程式使用使用者指派的受控識別

使用者指派的受控識別會以獨立 Azure 資源的形式建立。 Azure 會在所使用訂用帳戶信任的 Azure AD 租用戶中建立身分識別。 建立身分識別之後，即可將它指派給一個或多個 Azure 服務執行個體。 複製此身分識別的 `Object ID`，並將它設定為連接字串中的使用者名稱。 

因此，當使用使用者指派的受控識別進行連線時，請提供物件識別碼作為使用者名稱，但省略密碼。

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
[搭配 ODBC 驅動程式使用 Azure Active Directory](../odbc/using-azure-active-directory.md)

[什麼是適用於 Azure 資源的受控識別？](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
