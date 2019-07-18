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
manager: mbarwin
ms.openlocfilehash: 30423cd7c15a920d99fad4c0ea08e074beaece0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62522803"
---
# <a name="connect-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證進行連線
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) 是做為替代運作方式的中央使用者識別碼管理技術[SQL Server 驗證](../../connect/php/how-to-connect-using-sql-server-authentication.md)。 Azure AD 可連線到 Microsoft Azure SQL Database 和 SQL 資料倉儲具有同盟識別身分讓 Azure AD 中使用使用者名稱和密碼、 Windows 整合式驗證或 Azure AD 存取權杖。 SQL Server 的 PHP 驅動程式提供這些功能的部分支援。

若要使用 Azure AD，使用**驗證**或是**AccessToken**關鍵字 （它們是互斥的） 下, 表所示。 如需更多技術的詳細資訊，請參閱[使用 Azure Active Directory 與 ODBC 驅動程式](../../connect/odbc/using-azure-active-directory.md)。

|關鍵字|值|Description|
|-|-|-|
|**AccessToken**|未設定 （預設值）|驗證模式取決於其他關鍵字。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。 |
||位元組的字串|Azure AD 存取權杖的 OAuth JSON 回應中擷取。 連接字串不可以包含使用者識別碼、 密碼或驗證關鍵字 (需要 ODBC Driver 17 版或更新版本在 Linux 或 macOS)。 |
|**驗證**|未設定 （預設值）|驗證模式取決於其他關鍵字。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。 |
||`SqlPassword`|直接向 SQL Server 執行個體 （這可能是 Azure 的執行個體） 的使用者名稱和密碼。 使用者名稱和密碼必須傳遞至連接字串使用**UID**並**PWD**關鍵字。 |
||`ActiveDirectoryPassword`|使用 Azure Active Directory 身分識別的使用者名稱和密碼進行驗證。 使用者名稱和密碼必須傳遞至連接字串使用**UID**並**PWD**關鍵字。 |
||`ActiveDirectoryMsi`|使用系統指派的受控身分識別或使用者指派的受控身分識別進行驗證 (需要 ODBC 驅動程式版本 17.3.1.1 或更新版本)。 如需概觀和教學課程，請參閱[什麼是適用於 Azure 資源管理的身分識別？](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)。|

**驗證**關鍵字會影響連線安全性設定。 如果在連接字串中，則根據預設，它會設定**Encrypt**關鍵字設定為 true，表示用戶端會要求加密。 此外，將會驗證伺服器憑證的加密設定無論除非**TrustServerCertificate**設定為 true (**false**預設情況下)。 這項功能從舊的、 較不安全的登入方法，只有在連接字串中特別要求加密時，會驗證伺服器憑證有所區分。

使用 Azure AD 與 PHP 驅動程式中，Windows 上的 SQL Server，您可能會要求您安裝[Microsoft Online Services 登入小幫手](https://www.microsoft.com/download/details.aspx?id=41950)（不需要 ODBC 17 +）。

#### <a name="limitations"></a>限制

在 Windows，基礎 ODBC 驅動程式支援多個值**驗證**關鍵字**ActiveDirectoryIntegrated**，但是的 PHP 驅動程式在任何平台上不支援此值。

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>範例-使用 SqlPassword 和 ActiveDirectoryPassword 連線

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

## <a name="example---connect-using-the-pdosqlsrv-driver"></a>範例-使用 PDO_SQLSRV 驅動程式連接

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

## <a name="example---connect-using-azure-ad-access-token"></a>範例-使用 Azure AD 存取權杖進行連線

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

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>範例-使用適用於 Azure 資源的受管理的身分識別進行連接

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>使用 SQLSRV 驅動程式的系統指派的受控身分識別

當連接使用系統指派給受控身分識別時，請勿使用 UID 或 PWD 選項。

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

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>使用 PDO_SQLSRV 驅動程式的使用者指派的受控身分識別

使用者指派的受控身分識別會建立為獨立的 Azure 資源。 Azure 中使用的訂用帳戶信任 Azure AD 租用戶中建立身分識別。 建立身分識別之後，身分識別可以指派給一或多個 Azure 服務執行個體。 複製`Object ID`此身分識別和組為使用者的連接字串中的名稱。 

因此，當使用使用者指派連接受控身分識別，提供使用者名稱的物件識別碼，但省略密碼。

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

[什麼是適用於 Azure 資源管理的身分識別？](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
