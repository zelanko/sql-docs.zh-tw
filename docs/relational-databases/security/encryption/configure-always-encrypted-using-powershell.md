---
title: 使用 PowerShell 設定 Always Encrypted | Microsoft Docs
description: 了解如何匯入及使用 SqlServer PowerShell 模組，其提供 Cmdlet 讓您在 Azure SQL Database 與 SQL Server 中設定 Always Encrypted。
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cbfed6a62aa912eff42564a06ebc9574f8cab064
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97405413"
---
# <a name="configure-always-encrypted-using-powershell"></a>使用 PowerShell 設定永遠加密
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

SqlServer PowerShell 模組提供 Cmdlet 讓您在 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中設定 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)。

## <a name="security-considerations-when-using-powershell-to-configure-always-encrypted"></a>使用 PowerShell 設定 Always Encrypted 時的安全性考量

因為永遠加密的主要目標是為了確保已加密的敏感性資料安全無虞，即使資料庫系統遭到入侵亦然，所以在 SQL Server 電腦上執行處理金鑰或敏感性資料的 PowerShell 指令碼，可能會降低或損害此功能的優勢。 如需其他安全性相關建議，請參閱 [金鑰管理的安全性考量](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)。

無論是否有角色隔離，您都可以使用 PowerShell 來管理 Always Encrypted 金鑰來控制能夠存取金鑰存放區中實際加密金鑰以及能夠存取資料庫的人員。

 如需其他建議，請參閱 [金鑰管理的安全性考量](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)。

## <a name="prerequisites"></a>必要條件

在未裝載 SQL Server 執行個體的安全電腦上安裝 [SqlServer 模組](/powershell/sqlserver/sqlserver/vlatest/sqlserver) 。 此模組可以直接從 PowerShell 資源庫進行安裝。  如需更多詳細資料，請參閱[下載](../../../powershell/download-sql-server-ps-module.md)指示。


## <a name="importing-the-sqlserver-module"></a><a name="importsqlservermodule"></a> 匯入 SqlServer 模組 

若要載入 SqlServer 模組：

1.  使用 **Set-ExecutionPolicy** Cmdlet，設定適當的指令碼執行原則。
2.  使用 **Import-Module** Cmdlet，匯入 SqlServer 模組。

此範例會載入 SqlServer 模組。

```
# Import the SQL Server Module.  
Import-Module "SqlServer" 
```

## <a name="connecting-to-a-database"></a><a name="connectingtodatabase"></a> 連接到資料庫

某些永遠加密 Cmdlet 會處理資料庫中的資料或中繼資料，因此要求您必須先連接到資料庫。 使用 SqlServer 模組設定永遠加密時，有兩種建議的方法可連接到資料庫： 
1. 使用 **Get-SqlDatabase** Cmdlet 進行連線。
2. 使用 SQL Server PowerShell 提供者進行連線。

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="using-get-sqldatabase"></a>使用 Get-SqlDatabase
**Get-SqlDatabase** Cmdlet 可讓您連線至 SQL Server 或 Azure SQL Database 中的資料庫。 會傳回資料庫物件，然後使用連線至資料庫之 Cmdlet 的 **InputObject** 參數來傳遞。 

### <a name="using-sql-server-powershell"></a>使用 SQL Server PowerShell

```
# Import the SqlServer module
Import-Module "SqlServer"  

# Connect to your database
# Set the valid server name, database name and authentication keywords in the connection string
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$database = Get-SqlDatabase -ConnectionString $connStr

# List column master keys for the specified database.
Get-SqlColumnMasterKey -InputObject $database
```

或者，您可以使用管道：


```
$database | Get-SqlColumnMasterKey
```

### <a name="using-sql-server-powershell-provider"></a>使用 SQL Server PowerShell 提供者
[SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)會公開類似於檔案系統路徑之路徑中的 SQL Server 物件階層。 透過 SQL Server PowerShell，您可以使用 Windows PowerShell 別名來巡覽路徑，這與於一般用來巡覽檔案系統路徑的命令類似。 一旦您瀏覽至目標執行個體和資料庫後，後續的 Cmdlet 就會以該資料庫為目標，如下列範例所示。 

> [!NOTE]
> 此連線至資料庫的方法只適用於 SQL Server (Azure SQL Database 不支援)。

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
 
## <a name="always-encrypted-tasks-using-powershell"></a>使用 PowerShell 的永遠加密工作

- [使用 Provision 佈建 Always Encrypted 金鑰](configure-always-encrypted-keys-using-powershell.md)
- [使用 PowerShell 更換永遠加密金鑰](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [使用 PowerShell 利用 Always Encrypted 加密、重新加密或解密資料行](configure-column-encryption-using-powershell.md)


##  <a name="always-encrypted-cmdlet-reference"></a><a name="aecmdletreference"></a> 永遠加密 Cmdlet 參考

下列 PowerShell Cmdlet 可用於永遠加密：

|CMDLET |描述
|:---|:---
|**[Add-SqlAzureAuthenticationContext](/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)** |對 Azure 執行驗證，並取得驗證權杖。
|**[Add-SqlColumnEncryptionKeyValue](/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)** |為資料庫中現有的資料行加密金鑰物件新增加密值。
|**[Complete-SqlColumnMasterKeyRotation](/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)** |完成資料行主要金鑰的輪替
|**[Get-SqlColumnEncryptionKey](/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)**   |傳回資料庫中定義的所有資料行加密金鑰物件，或傳回具有指定名稱的一個資料行加密金鑰物件。
|**[Get-SqlColumnMasterKey](/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey)**   |傳回資料庫中定義的資料行主要金鑰物件，或傳回具有指定名稱的一個資料行主要金鑰物件。
|**[Invoke-SqlColumnMasterKeyRotation](/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation)** |起始資料行主要金鑰的輪替。
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)** |建立 SqlColumnMasterKeySettings 物件，描述儲存在 Azure 金鑰保存庫中的非對稱金鑰。
|**[New-SqlCngColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)** |建立 SqlColumnMasterKeySettings 物件，描述儲存在支援新一代密碼編譯 (CNG) API 之金鑰存放區中的非對稱金鑰。
|**[New-SqlColumnEncryptionKey](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)**   |在資料庫中建立資料行加密金鑰物件。
|**[New-SqlColumnEncryptionKeyEncryptedValue](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)**   |產生資料行加密金鑰的加密值。
|**[New-SqlColumnEncryptionSettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings)** |建立 SqlColumnEncryptionSettings 物件，以封裝單一資料行加密的相關資訊，包括 CEK 和加密類型。
|**[New-SqlColumnMasterKey](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)**   |在資料庫中建立資料行主要金鑰物件。
|**[New-SqlColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkeysettings)**|使用指定的提供者與機碼路徑，為資料行主要金鑰建立 SqlColumnMasterKeySettings 物件。
|**[New-SqlCspColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)** |建立 SqlColumnMasterKeySettings 物件，描述使用支援密碼編譯 API 之密碼編譯服務提供者 (CSP) 儲存在金鑰存放區中的非對稱金鑰。
|**[Remove-SqlColumnEncryptionKey](/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey)** |從資料庫移除資料行加密金鑰物件。
|**[Remove-SqlColumnEncryptionKeyValue](/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue)**   |從資料庫中現有的資料行加密金鑰物件移除加密值。
|**[Remove-SqlColumnMasterKey](/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)** |從資料庫移除資料行主要金鑰物件。
|**[Set-SqlColumnEncryption](/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)** |加密、解密或重新加密資料庫中指定的資料行。



## <a name="see-also"></a>另請參閱

- [一律加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [使用 SQL Server Management Studio 設定 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [使用 Always Encrypted 開發應用程式](always-encrypted-client-development.md)