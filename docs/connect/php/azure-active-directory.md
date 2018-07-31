---
title: Azure Active Directory |Microsoft Docs
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: 71e6b3b4556621b6bc8a8a4c7996cfdb47a12849
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979440"
---
# <a name="connect-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證進行連線
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) 是做為替代運作方式的中央使用者識別碼管理技術[SQL Server 驗證](../../connect/php/how-to-connect-using-sql-server-authentication.md)。 Azure AD 允許連線到 Microsoft Azure SQL Database 和 SQL 資料倉儲同盟身分識別與 Azure AD 中使用使用者名稱和密碼、 Windows 整合式驗證或 Azure AD 存取權杖;SQL Server 的 PHP 驅動程式提供這些功能的部分支援。

若要使用 Azure AD，使用**驗證**關鍵字。 值，**驗證**可能需要在下表中說明。

|關鍵字|值|Description|
|-|-|-|
|**驗證**|未設定 （預設值）|驗證模式取決於其他關鍵字。 如需詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。 |
||`SqlPassword`|直接向 SQL Server 執行個體 （這可能是 Azure 的執行個體） 的使用者名稱和密碼。 使用者名稱和密碼必須傳遞至連接字串使用**UID**並**PWD**關鍵字。 |
||`ActiveDirectoryPassword`|使用 Azure Active Directory 身分識別的使用者名稱和密碼進行驗證。 使用者名稱和密碼必須傳遞至連接字串使用**UID**並**PWD**關鍵字。 |

**驗證**關鍵字會影響連線安全性設定。 如果在連接字串中，則根據預設，它會設定**Encrypt**關鍵字設定為 true，讓用戶端會要求加密。 此外，將會驗證伺服器憑證的加密設定無論除非**TrustServerCertificate**設為 true。 這被區分從舊的檔案，並較不安全的登入方法所在的伺服器憑證不會驗證只有在連接字串中特別要求加密。

之前使用 Azure AD 與 PHP 驅動程式中，Windows 上的 SQL Server，請確定您已安裝[Microsoft Online Services 登入小幫手](https://www.microsoft.com/download/details.aspx?id=41950)（不需要適用於 Linux 和 MacOS）。

#### <a name="limitations"></a>限制

在 Windows，基礎 ODBC 驅動程式支援多個值**驗證**關鍵字**ActiveDirectoryIntegrated**，但是的 PHP 驅動程式在任何平台上不支援此值，因此也不支援 Azure AD 權杖型驗證。

## <a name="example"></a>範例

下列範例示範如何使用連接**SqlPassword**並**ActiveDirectoryPassword**。

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

下列範例會執行與上述相同使用 PDO_SQLSRV 驅動程式。

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
[搭配 ODBC 驅動程式使用 Azure Active Directory](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)
