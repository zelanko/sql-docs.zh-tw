---
title: "使用 PowerShell 設定 Always Encrypted | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-security
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
caps.latest.revision: "15"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 591f48405009951f3f8e956e3a2aa40364a58e44
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="configure-always-encrypted-using-powershell"></a>使用 PowerShell 設定永遠加密
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

SqlServer PowerShell 模組提供 Cmdlet 讓您在 Azure SQL Database 與 SQL Server 2016 中設定 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) 。

因為 SqlServer 模組中的永遠加密 Cmdlet 會處理金鑰或敏感性資料，所以請務必在安全的電腦上執行 Cmdlet。 管理永遠加密時，請從與裝載您的 SQL Server 執行個體不同的電腦上執行 Cmdlet。

因為永遠加密的主要目標是為了確保已加密的敏感性資料安全無虞，即使資料庫系統遭到入侵亦然，所以在 SQL Server 電腦上執行處理金鑰或敏感性資料的 PowerShell 指令碼，可能會降低或損害此功能的優勢。 如需其他安全性相關建議，請參閱 [金鑰管理的安全性考量](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)。

[此頁面底部](#aecmdletreference)的連結。

## <a name="prerequisites"></a>必要條件

在未裝載 SQL Server 執行個體的安全電腦上安裝 [SqlServer 模組](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/sqlserver) 。 此模組可以直接從 PowerShell 資源庫進行安裝。  如需更多詳細資料，請參閱[下載](../../../ssms/download-sql-server-ps-module.md)指示。


## <a name="importsqlservermodule"></a> 匯入 SqlServer 模組 

若要載入 SqlServer 模組：

1.  使用 **Set-ExecutionPolicy** Cmdlet，設定適當的指令碼執行原則。
2.  使用 **Import-Module** Cmdlet，匯入 SqlServer 模組。

此範例會載入 SqlServer 模組。

```
# Import the SQL Server Module.  
Import-Module "SqlServer" 
```

## <a name="connectingtodatabase"></a> 連接到資料庫

某些永遠加密 Cmdlet 會處理資料庫中的資料或中繼資料，因此要求您必須先連接到資料庫。 使用 SqlServer 模組設定永遠加密時，有兩種建議的方法可連接到資料庫： 
1. 使用 SQL Server PowerShell 連接。
2. 使用 SQL Server 管理物件 (SMO) 連接。

### <a name="using-sql-server-powershell"></a>使用 SQL Server PowerShell

此方法只適用於 SQL Server (Azure SQL Database 不支援)。

透過 SQL Server PowerShell，您可以使用 Windows PowerShell 別名來巡覽路徑，這與於一般用來巡覽檔案系統路徑的命令類似。 一旦您巡覽至目標執行個體和資料庫後，後續的 Cmdlet 就會以該資料庫為目標，如下列範例所示：

```
# Import the SqlServer module.
Import-Module "SqlServer"
# Navigate to the database in the remote instance.
cd SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
# List column master keys in the above database.
Get-SqlColumnMasterKey
```

 
或者，您可以使用泛型 **Path** 參數來指定資料庫路徑，而不是巡覽至資料庫。


```
# Import the SqlServer module.
Import-Module "SqlServer" 
# List column master keys for the specified database.
Get-SqlColumnMasterKey -Path SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
```
 
### <a name="using-smo"></a>使用 SMO

此方法適用於 Azure SQL Database 和 SQL Server。
透過 SMO，您可以建立 [資料庫類別](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.database.aspx)的物件，然後使用連接到資料庫之 Cmdlet 的 **InputObject** 參數來傳遞物件。


```
# Import the SqlServer module
Import-Module "SqlServer"  

# Connect to your database (Azure SQL database).
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName] 

# List column master keys for the specified database.
Get-SqlColumnMasterKey -InputObject $database
```


或者，您可以使用管道：


```
$database | Get-SqlColumnMasterKey
```

## <a name="always-encrypted-tasks-using-powershell"></a>使用 PowerShell 的永遠加密工作

- [使用 PowerShell 設定永遠加密金鑰](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md) 
- [使用 PowerShell 更換永遠加密金鑰](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [使用 PowerShell 設定資料行加密](../../../relational-databases/security/encryption/configure-column-encryption-using-powershell.md)


##  <a name="aecmdletreference"></a> 永遠加密 Cmdlet 參考

下列 PowerShell Cmdlet 可用於永遠加密：

|CMDLET |描述
|:---|:---
|**[Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)**   |對 Azure 執行驗證，並取得驗證權杖。
|**[Add-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)**   |為資料庫中現有的資料行加密金鑰物件新增加密值。
|**[Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)**   |完成資料行主要金鑰的輪替
|**[Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)** |傳回資料庫中定義的所有資料行加密金鑰物件，或傳回具有指定名稱的一個資料行加密金鑰物件。
|**[Get-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey)** |傳回資料庫中定義的資料行主要金鑰物件，或傳回具有指定名稱的一個資料行主要金鑰物件。
|**[Invoke-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation)**   |起始資料行主要金鑰的輪替。
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)**   |建立 SqlColumnMasterKeySettings 物件，描述儲存在 Azure 金鑰保存庫中的非對稱金鑰。
|**[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)**   |建立 SqlColumnMasterKeySettings 物件，描述儲存在支援新一代密碼編譯 (CNG) API 之金鑰存放區中的非對稱金鑰。
|**[New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)** |在資料庫中建立資料行加密金鑰物件。
|**[New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)** |產生資料行加密金鑰的加密值。
|**[New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings)**   |建立 SqlColumnEncryptionSettings 物件，以封裝單一資料行加密的相關資訊，包括 CEK 和加密類型。
|**[New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)** |在資料庫中建立資料行主要金鑰物件。
|**[New-SqlColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkeysettings)**|使用指定的提供者與機碼路徑，為資料行主要金鑰建立 SqlColumnMasterKeySettings 物件。
|**[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)**   |建立 SqlColumnMasterKeySettings 物件，描述使用支援密碼編譯 API 之密碼編譯服務提供者 (CSP) 儲存在金鑰存放區中的非對稱金鑰。
|**[Remove-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey)**   |從資料庫移除資料行加密金鑰物件。
|**[Remove-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue)** |從資料庫中現有的資料行加密金鑰物件移除加密值。
|**[Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)**   |從資料庫移除資料行主要金鑰物件。
|**[Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)**   |加密、解密或重新加密資料庫中指定的資料行。



## <a name="additional-resources"></a>其他資源

- [一律加密 (Database Engine)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [永遠加密的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [搭配 .NET Framework Data Provider for SQL Server 使用永遠加密](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [使用 SQL Server Management Studio 設定永遠加密](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)


