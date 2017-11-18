---
title: "Azure Active Directory |Microsoft 文件"
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.suite: sql
ms.custom: 
ms.technology:
- drivers
ms.topic: article
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 01d921ebee152924b905fa7a9de8c6d46f41ca64
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connect-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證進行連接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis) (Azure AD) 是做為替代運作中央使用者識別碼管理技術[SQL Server 驗證](../../connect/php/how-to-connect-using-sql-server-authentication.md)。 Azure AD 可讓連線到 Microsoft Azure SQL Database 和 SQL 資料倉儲具有同盟識別身分在 Azure AD 中使用使用者名稱和密碼、 Windows 整合式驗證或 Azure AD 存取權杖。SQL Server 的 PHP 驅動程式提供這些功能的部分支援。

若要使用 Azure AD，**驗證**關鍵字。 值，**驗證**可能需要在下表中說明。

|關鍵字|值|Description|
|-|-|-|
|**驗證**|未設定 （預設值）|驗證模式取決於其他關鍵字。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。 |
||`SqlPassword`|SQL Server 執行個體 （這可能是 Azure 的執行個體） 直接驗證使用者名稱和密碼。 使用者名稱和密碼必須傳遞至連接字串使用**UID**和**PWD**關鍵字。 |
||`ActiveDirectoryPassword`|以 Azure Active Directory 識別身分的使用者名稱及密碼進行驗證。 使用者名稱和密碼必須傳遞至連接字串使用**UID**和**PWD**關鍵字。 |

**驗證**關鍵字會影響連接安全性設定。 如果在連接字串中，則預設設定**加密**關鍵字設定為 true，讓用戶端會要求加密。 此外，將會驗證伺服器憑證的加密設定無論除非**TrustServerCertificate**設為 true。 這被辨別從舊的檔案，以及較不安全，登入方法，在其中的伺服器憑證不會驗證除非加密會在特別要求的連接字串中。

之前使用 Azure AD 的 PHP 驅動程式在 Windows 上的 SQL Server，請確定您已安裝[Microsoft Online Services 登入小幫手](https://www.microsoft.com/download/details.aspx?id=41950)（適用於 Linux 和 MacOS 非必要）。

#### <a name="limitations"></a>限制

在 Windows 中，基礎的 ODBC 驅動程式支援的多個值**驗證**關鍵字， **ActiveDirectoryIntegrated**，但是 PHP 驅動程式在任何平台上不支援此值，因此也不支援 Azure AD 權杖型驗證。

## <a name="example"></a>範例

下列範例示範如何使用連接**SqlPassword**和**ActiveDirectoryPassword**。

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = array( "UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword' );

    $conn = sqlsrv_connect( $serverName, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=SqlPassword.\n";
        sqlsrv_close( $conn );
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = array( "Database"=>$azureDatabase, "UID"=>$azureUsername, "PWD"=>$azurePassword,
                             "Authentication"=>'ActiveDirectoryPassword' );

    $conn = sqlsrv_connect( $azureServer, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        sqlsrv_close( $conn );
    }

    ?>
```

下列範例會執行與上述使用相同的 PDO_SQLSRV 驅動程式。

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword );
        echo "Connected successfully with Authentication=SqlPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword );
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    ?>
```
## <a name="see-also"></a>另請參閱  
[使用 Azure Active Directory 的 ODBC 驅動程式](https://docs.microsoft.com/en-us/sql/connect/odbc/using-azure-active-directory)

