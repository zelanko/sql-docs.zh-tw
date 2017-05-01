---
title: "使用 PowerShell 設定 Always Encrypted | Microsoft Docs"
ms.custom: 
ms.date: 09/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-security
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7e3971933bb32cc47f761d18ba8c0dd57b139636
ms.lasthandoff: 04/11/2017

---
# <a name="configure-always-encrypted-using-powershell"></a>使用 PowerShell 設定永遠加密
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

SqlServer PowerShell 模組提供 Cmdlet 讓您在 Azure SQL Database 與 SQL Server 2016 中設定 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) 。

因為 SqlServer 模組中大部分的永遠加密 Cmdlet 會處理永遠加密金鑰或儲存在加密資料行中的敏感性資料，所以請務必在安全的電腦上執行 Cmdlet。 管理永遠加密時，請從與裝載您的 SQL Server 執行個體不同的電腦上執行 Cmdlet。 

因為永遠加密的主要目標是為了確保已加密的敏感性資料安全無虞，即使資料庫系統遭到入侵亦然，所以在 SQL Server 電腦上執行處理金鑰或敏感性資料的 PowerShell 指令碼，可能會降低或損害此功能的優點。 如需其他安全性相關建議，請參閱 [金鑰管理的安全性考量](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)。

[此頁面底部](#aecmdletreference)的連結。

## <a name="prerequisites"></a>必要條件

在未裝載 SQL Server 執行個體的安全電腦上安裝 [SqlServer 模組](https://msdn.microsoft.com/library/mt740629.aspx) 。 

安裝最新版的 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)來安裝 SqlServer 模組。
請注意， *SqlServer* 模組不同於 *sqlps* 模組，其不支援永遠加密。 如需詳細資訊，請參閱小組的 [SQL PowerShell - 2016 年 7 月更新](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update) 部落格文章。

## <a name="importsqlservermodule"></a> 匯入 SqlServer 模組 

若要載入 SqlServer 模組：

1.    使用 **Set-ExecutionPolicy** Cmdlet，設定適當的指令碼執行原則。
2.    使用 **Import-Module** Cmdlet，匯入 SqlServer 模組。

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

透過 SQL Server PowerShell，您可以使用 Windows PowerShell 別名來巡覽路徑，這與於一般用來巡覽檔案系統路徑的命令類似。 一旦您巡覽至目標執行個體和資料庫，後續的 Cmdlet 將會以該資料庫為目標，如下列範例所示：

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

|CMDLET    |描述
|:---|:---
|**[Add-SqlAzureAuthenticationContext](https://msdn.microsoft.com/library/mt759815.aspx)**    |對 Azure 執行驗證，並取得驗證權杖。
|**[Add-SqlColumnEncryptionKeyValue](https://msdn.microsoft.com/library/mt759817.aspx)**    |為資料庫中現有的資料行加密金鑰物件新增加密值。
|**[Complete-SqlColumnMasterKeyRotation](https://msdn.microsoft.com/library/mt759791.aspx)**    |完成資料行主要金鑰的輪替
|**[Get-SqlColumnEncryptionKey](https://msdn.microsoft.com/library/mt759814.aspx)**    |傳回資料庫中定義的所有資料行加密金鑰物件，或傳回具有指定名稱的一個資料行加密金鑰物件。
|**[Get-SqlColumnMasterKey](https://msdn.microsoft.com/library/mt759782.aspx)**    |傳回資料庫中定義的資料行主要金鑰物件，或傳回具有指定名稱的一個資料行主要金鑰物件。
|**[Invoke-SqlColumnMasterKeyRotation](https://msdn.microsoft.com/library/mt759810.aspx)**    |起始資料行主要金鑰的輪替。
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759795.aspx)**    |建立 SqlColumnMasterKeySettings 物件，描述儲存在 Azure 金鑰保存庫中的非對稱金鑰。
|**[New-SqlCngColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759818.aspx)**    |建立 SqlColumnMasterKeySettings 物件，描述儲存在支援新一代密碼編譯 (CNG) API 之金鑰存放區中的非對稱金鑰。
|**[New-SqlColumnEncryptionKey](https://msdn.microsoft.com/library/mt759808.aspx)**    |在資料庫中建立新的資料行加密金鑰物件。
|**[New-SqlColumnEncryptionKeyEncryptedValue](https://msdn.microsoft.com/library/mt759794.aspx)**    |產生資料行加密金鑰的加密值。
|**[New-SqlColumnEncryptionSettings](https://msdn.microsoft.com/library/mt759825.aspx)**    |建立新的 SqlColumnEncryptionSettings 物件，以封裝單一資料行加密的相關資訊，包括 CEK 和加密類型。
|**[New-SqlColumnMasterKey](https://msdn.microsoft.com/library/mt759813.aspx)**    |在資料庫中建立新的資料行主要金鑰物件。
|**New-SqlColumnMasterKeySettings**|使用指定的提供者與機碼路徑，為資料行主要金鑰建立 SqlColumnMasterKeySettings 物件。
|**[New-SqlCspColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759784.aspx)**    |建立 SqlColumnMasterKeySettings 物件，描述使用支援密碼編譯 API 之密碼編譯服務提供者 (CSP) 儲存在金鑰存放區中的非對稱金鑰。
|**[Remove-SqlColumnEncryptionKey](https://msdn.microsoft.com/library/mt759786.aspx)**    |從資料庫移除資料行加密金鑰物件。
|**[Remove-SqlColumnEncryptionKeyValue](https://msdn.microsoft.com/library/mt759783.aspx)**    |從資料庫中現有的資料行加密金鑰物件移除加密值。
|**[Remove-SqlColumnMasterKey](https://msdn.microsoft.com/library/mt759800.aspx)**    |從資料庫移除資料行主要金鑰物件。
|**[Set-SqlColumnEncryption](https://msdn.microsoft.com/library/mt759790.aspx)**    |加密、解密或重新加密資料庫中指定的資料行。



## <a name="additional-resources"></a>其他資源

- [一律加密 (Database Engine)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [永遠加密的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [搭配 .NET Framework Data Provider for SQL Server 使用永遠加密](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [使用 SQL Server Management Studio 設定永遠加密](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)



