---
title: "使用 PowerShell 設定資料行加密 | Microsoft Docs"
ms.custom: ""
ms.date: "01/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "powershell"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 074c012b-cf14-4230-bf0d-55e23d24f9c8
caps.latest.revision: 8
author: "stevestein"
ms.author: "sstein"
manager: "jhubbard"
caps.handback.revision: 6
---
# 使用 PowerShell 設定資料行加密
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

本文逐步說明如何使用 *SqlServer* PowerShell 模組中的 [Set-SqlColumnEncryption](https://msdn.microsoft.com/library/mt759790.aspx) Cmdlet，為資料庫資料行設定目標永遠加密組態。 **Set-SqlColumnEncryption** Cmdlet 會同時修改目標資料庫的結構描述及儲存在所選資料行中的資料。 您可以根據資料行的指定目標加密設定和目前的加密組態，對儲存在資料行中的資料進行加密、重新加密或解密。
如需 SqlServer PowerShell 模組中關於 Always Encrypted 支援的詳細資訊，請參閱[使用 PowerShell 設定 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)。

## <a name="prerequisites"></a>必要條件

若要設定目標加密組態，您必須確定：
- 資料庫中已設定一個資料行加密金鑰 (如果您要加密或重新加密資料行)。 如需詳細資訊，請參閱 [使用 PowerShell 設定永遠加密金鑰](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)。
- 您可以從電腦執行 PowerShell Cmdlet，以存取您要加密、重新加密或解密之每個資料行的資料行主要金鑰。 

## <a name="performance-and-availability-considerations"></a>效能與可用性考量

若要為資料庫套用指定的目標加密設定，**Set-SqlColumnEncryption** Cmdlet 會以透明方式從包含目標資料表的資料行下載所有資料、將資料上傳回到一組暫存資料表 (包含目標加密設定)，最後使用新的資料表版本來取代原始資料表。 適用於 SQL Server 的基礎 .NET Framework 資料提供者會根據目標資料行目前的加密設定以及針對目標資料行指定的目標加密設定而定，在下載或/和上傳加密或/和解密資料。 根據受影響資料表中的資料大小與網路頻寬而定，移動資料的作業可能需要一段很長的時間。

**Set-SqlColumnEncryption** Cmdlet 支援兩種方法來設定目標加密設定︰線上和離線。

使用離線方法時，目標資料表 (以及與目標資料表相關的所有資料表，例如，與目標資料表具有外部索引鍵關聯性的所有資料表) 無法在作業持續期間寫入交易。

使用線上方法時，複製和加密、解密或重新加密資料的作業會以累加方式執行。 應用程式可以在整個資料移動作業期間，從目標資料表讀取資料以及將資料寫入目標資料表，但最後一個反覆運算除外，該期間受限於 MaxDownTimeInSeconds 參數 (您可以定義)。 若要偵測並處理變更，應用程式可以在複製資料時進行，Cmdlet 會在目標資料庫中啟用「變更追蹤」。 因此，比起離線方法，線上方法很可能會使用伺服器端上的更多資源。 使用線上方法的作業可能也需要更多時間，特別是在對資料庫執行大量寫入的工作負載時。 線上方法可用來一次加密一個資料表，而該資料表必須具有主索引鍵。

以下是在離線和線上方法之間進行選擇的指導方針：

使用離線方法：
- 若要將作業期間縮至最短。 
- 若要同時在多個資料表中加密/解密/重新加密資料行。
- 如果資料表沒有主索引鍵。

使用離線方法：
- 若要使用資料庫，將應用程式的停機時間/無法使用的情況最小化。

## <a name="security-considerations"></a>安全性考量

用來設定資料庫資料行加密的 **Set-SqlColumnEncryption** Cmdlet，會處理永遠加密金鑰和儲存在資料庫資料行中的資料。 因此，請務必在安全的電腦上執行 Cmdlet。 如果您的資料庫在 SQL Server 上，請從與裝載您的 SQL Server 執行個體不同的電腦上執行 Cmdlet。 因為永遠加密的主要目標是為了確保已加密的敏感性資料安全無虞，即使資料庫系統遭到入侵亦然，所以在 SQL Server 電腦上執行處理金鑰和/或敏感性資料的 PowerShell 指令碼，可能會降低或損害此功能的優點。

工作  |發行項  |存取純文字金鑰/金鑰存放區  |存取資料庫   
---|---|---|---
步驟 1： 啟動 PowerShell 環境並匯入 SqlServer 模組。 | [匯入 SqlServer 模組](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 否 | 否
步驟 2： 連接到您的伺服器和資料庫 | [連接到資料庫](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 否 | 是
步驟 3： 如果您的資料行主要金鑰 (用於保護資料行加密金鑰並需要更換) 儲存在 Azure 金鑰保存庫中，請向 Azure 驗證 | [Add-SqlAzureAuthenticationContext](https://msdn.microsoft.com/library/mt759815.aspx) | 是 | 否
步驟 4： 建構 SqlColumnEncryptionSettings 物件的陣列 - 您要加密、重新加密或解密的每個資料庫資料行各有一個物件。 SqlColumnMasterKeySettings 是存在於 PowerShell 記憶體中的物件。 它會指定資料行的目標加密配置。 | [New-SqlColumnEncryptionSettings](https://msdn.microsoft.com/library/mt759825.aspx) | 否 | 否
步驟 5： 針對您在上一個步驟中建立的 SqlColumnMasterKeySettings 物件陣列，設定在其中指定的所需加密組態。 將會根據資料行的指定目標設定和目前的加密組態，對資料行進行加密、重新加密或解密。| [Set-SqlColumnEncryption](https://msdn.microsoft.com/library/mt759790.aspx)<br><br>**注意︰**此步驟可能需要很長的時間。 根據您選取的方法 (線上與離線) 而定，您的應用程式將無法在整個作業期間或作業的部分期間存取資料表。 | 是 | 是

## <a name="encrypt-columns-using-offline-approach---example"></a>使用離線方法加密資料行 - 範例

下列範例示範如何設定兩個資料行的目標加密組態。  若有任何一個資料行尚未經過加密，將會對其進行加密。 若有任何資料行已使用不同的金鑰和/或不同的加密類型加密，則會將它解密，然後使用指定的目標金鑰/類型重新加密。


```
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Encrypt the selected columns (or re-encrypt, if they are already encrypted using keys/encrypt types, different than the specified keys/types.
$ces = @()
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.SSN" -EncryptionType "Deterministic" -EncryptionKey "CEK1"
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.BirthDate" -EncryptionType "Randomized" -EncryptionKey "CEK1"
Set-SqlColumnEncryption -InputObject $database -ColumnEncryptionSettings $ces -LogFileDirectory .
```
 
## <a name="encrypt-columns-using-online-approach---example"></a>使用線上方法加密資料行 - 範例

下列範例示範如何使用線上方法，設定兩個資料行的目標加密設定。 若有任何一個資料行尚未經過加密，將會對其進行加密。 若有任何資料行已使用不同的金鑰和/或不同的加密類型加密，則會將它解密，然後使用指定的目標金鑰/類型重新加密。

```
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Encrypt the selected columns (or re-encrypt, if they are already encrypted using keys/encrypt types, different than the specified keys/types.
$ces = @()
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.SSN" -EncryptionType "Deterministic" -EncryptionKey "CEK1"
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.BirthDate" -EncryptionType "Randomized" -EncryptionKey "CEK1"
Set-SqlColumnEncryption -InputObject $database -ColumnEncryptionSettings $ces -UseOnlineApproach -MaxDowntimeInSeconds 180 -LogFileDirectory .
```
## <a name="decrypt-columns---example"></a>解密資料行 - 範例

下列範例示範如何解密目前在資料庫中加密的所有資料行。


```
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Find all encrypted columns, and create a SqlColumnEncryptionSetting object for each column.
$ces = @()
$tables = $database.Tables
for($i=0; $i -lt $tables.Count; $i++){
    $columns = $tables[$i].Columns
    for($j=0; $j -lt $columns.Count; $j++) {
        if($columns[$j].isEncrypted) {
            $threeColPartName = $tables[$i].Schema + "." + $tables[$i].Name + "." + $columns[$j].Name 
            $ces += New-SqlColumnEncryptionSettings -ColumnName $threeColPartName -EncryptionType "Plaintext" 
        }
    }
}

# Decrypt all columns.
Set-SqlColumnEncryption -ColumnEncryptionSettings $ces -InputObject $database -LogFileDirectory .
```
 

## <a name="additional-resources"></a>其他資源
- [使用 PowerShell 設定 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [Always Encrypted (資料庫引擎)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)


