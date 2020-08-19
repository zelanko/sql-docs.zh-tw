---
description: 使用 PowerShell 輪替 Always Encrypted 金鑰
title: 使用 PowerShell 輪替 Always Encrypted 金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 5117b4fd-c8d3-48d5-87c9-756800769f31
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1f2010ad30f38d2e7bf89a18b833d93e00aec1f8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448110"
---
# <a name="rotate-always-encrypted-keys-using-powershell"></a>使用 PowerShell 輪替 Always Encrypted 金鑰
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

本文提供使用 SqlServer PowerShell 模組更換永遠加密金鑰的步驟。 如需如何開始針對永遠加密使用 SqlServer PowerShell 模組的詳細資訊，請參閱 [Configure Always Encrypted using PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)(使用 PowerShell 設定永遠加密)。

輪替永遠加密金鑰是以新金鑰取代現有金鑰的程序。 如果金鑰已遭洩漏，或是為了符合您的組織原則或必須定期輪替授權密碼編譯金鑰的標準規定，您可能必須輪替金鑰。 

永遠加密會使用兩種類型的金鑰，因此有兩個高階金鑰輪替工作流程。輪替資料行主要金鑰，以及輪替資料行加密金鑰。

* **資料行加密金鑰輪替** - 包含以目前金鑰加密的資料解密，然後使用新的資料行加密金鑰將資料重新加密。 因為輪替資料行加密金鑰需要同時存取金鑰和資料庫，所以資料行加密金鑰輪替只能在不進行角色分離的情況下執行。
* **資料行主要金鑰輪替** - 包含解密以目前資料行主要金鑰所保護的資料行加密金鑰、使用新的資料行主要金鑰重新進行加密，然後更新兩種金鑰的中繼資料。 資料行主要金鑰輪替完成時不一定要進行角色分離 (使用 SqlServer PowerShell 模組時)。

## <a name="column-master-key-rotation-without-role-separation"></a>不進行角色分離的資料行主要金鑰輪替

本節所描述的資料行主要金鑰輪替方法，不支援安全性系統管理員與 DBA 之間的角色分離。 底下的部分步驟會結合實體金鑰的作業，與金鑰中繼資料的作業，因此這個工作流程建議用於使用 DevOps 模型的組織，或是您的資料庫裝載於雲端且主要目標是限制雲端管理員 (而不是內部部署 DBA) 存取敏感性資料時。 如果潛在的對象包括 DBA，或是 DBA 不應具有存取敏感性資料的權限，即不建議使用。  


| Task | 發行項 | 存取純文字金鑰/金鑰存放區| 存取資料庫
|:---|:---|:---|:---
|步驟 1： 在金鑰存放區中建立新的資料行主要金鑰。<br><br>**注意：** SqlServer PowerShell 模組不支援此步驟。 若要從命令列完成這項工作，您需要使用金鑰存放區特有的工具。 | [建立及儲存 Always Encrypted 的資料行主要金鑰](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)| 是 | 否
|步驟 2： 啟動 PowerShell 環境並匯入 SqlServer 模組 | [匯入 SqlServer 模組](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 否 | 否
|步驟 3： 連接到您的伺服器和資料庫。 | [連線至資料庫](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 否 | 是
|步驟 4： 建立 SqlColumnMasterKeySettings 物件，其中包含新資料行主要金鑰位置的相關資訊。 SqlColumnMasterKeySettings 是存在於 PowerShell 記憶體中的物件。 若要建立它，您需要使用金鑰存放區特有的 Cmdlet。 |[New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)<br> | 否 | 否
|步驟 5。 在資料庫中建立新資料行主要金鑰的相關中繼資料。 | [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**注意︰** 實際上，這個 Cmdlet 發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 陳述式來建立金鑰中繼資料。 | 否 | 是
|步驟 6. 向 Azure 驗證，若您目前的資料行主要金鑰或新的資料行主要金鑰儲存在 Azure 金鑰保存庫 | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | 是 | 否
|步驟 7： 開始輪替，使用新的資料行主要金鑰將每個資料行加密金鑰加密，資料行加密金鑰目前是使用舊的資料行主要金鑰保護。 在這個步驟之後，與舊資料行主要金鑰相關聯且正在被輪替的每個受影響的資料行加密金鑰，會同時使用舊的和新的資料行主要金鑰來加密，並在資料庫中繼資料中有兩個加密的值。| [Invoke-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation) | 是 | 是
|步驟 8。 與在資料庫中查詢加密資料行 (且使用舊的資料行主要金鑰保護) 之所有應用程式的系統管理員協調，讓他們可以確保應用程式可以存取新的資料行主要金鑰。| [建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) | 是 | 否
|步驟 9. 完成輪替<br><br>**注意︰** 在執行此步驟之前，請先確定查詢使用舊資料行主要金鑰保護之加密資料行的所有應用程式，已設定為使用新的資料行主要金鑰。 如果您提前執行此步驟，這些應用程式中可能有些會無法解密資料。 從資料庫移除以舊的資料行主要金鑰所建立的加密值，完成輪替。 這會移除舊資料行主要金鑰和它所保護的資料行加密金鑰之間的關聯。 |[Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)| 否 | 是
|步驟 10： 從舊資料行主要金鑰移除中繼資料。 |[Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)| 否 | 是

> [!NOTE]
> 強烈建議您不要在輪替之後永久刪除舊的資料行主要金鑰。 而是應該將舊的資料行主要金鑰保留在其目前金鑰存放區中，或將它封存在另一個安全的地方。 如果您將資料庫從備份檔案還原到設定新資料行主要金鑰之前  的某個時間點，則需要舊的金鑰才能存取資料。

### <a name="rotating-a-column-master-key-without-role-separation-windows-certificate-example"></a>輪替資料行主要金鑰，而不進行角色分離 (Windows 憑證範例)

底下的指令碼是端對端範例，它將現有的資料行主要金鑰 (CMK1) 取代為新的資料行主要金鑰 (CMK2)。

```powershell
# Create a new column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048

# Import the SqlServer module
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Create metadata for your new column master key in the database.
$newCmkName = "CMK2"
New-SqlColumnMasterKey -Name $newCmkName -InputObject $database -ColumnMasterKeySettings $newCmkSettings

# Initiate the rotation from the current column master key to the new column master key.
$oldCmkName = "CMK1"
Invoke-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName -TargetColumnMasterKeyName $newCmkName -InputObject $database

# Complete the rotation of the old column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName  -InputObject $database

# Remove the old column master key metadata.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```

## <a name="column-master-key-rotation-with-role-separation"></a>進行角色分離的資料行主要金鑰輪替

本節所描述的資料行主要金鑰輪替工作流程，能確保安全性系統管理員與資料庫管理員之間的分離。

> [!IMPORTANT]
> 執行下表中「存取純文字金鑰/金鑰存放區」=「是」的任何步驟 (存取純文字金鑰或金鑰存放區的步驟) 之前，請確定 PowerShell 環境是在不同於裝載資料庫之電腦的安全電腦上執行。 如需詳細資訊，請參閱 [金鑰管理的安全性考量](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)。

### <a name="part-1-dba"></a>第 1 部分︰DBA

DBA 擷取有關要輪替之資料行主要金鑰的中繼資料，以及受影響之資料行加密金鑰 (與目前的資料行主要金鑰相關聯) 的中繼資料。 DBA 將這項資訊與安全性系統管理員分享。


| Task | 發行項 | 存取純文字金鑰/金鑰存放區| 存取資料庫
|:---|:---|:---|:---
|步驟 1： 啟動 PowerShell 環境並匯入 SqlServer 模組。 | [匯入 SqlServer 模組](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 否 | None
|步驟 2： 連接到您的伺服器和資料庫。 | [連線至資料庫](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 否 | 是
|步驟 3： 擷取關於舊資料行主要金鑰的中繼資料。| [Get-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey) | 否 | 是
|步驟 4： 擷取關於資料行加密金鑰 (受到舊的資料行主要金鑰保護) 的中繼資料，包括其加密的值。 | [Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey) | 否 | 是
|步驟 5。 提供資料行主要金鑰 (資料行主要金鑰的提供者名稱與金鑰路徑) 的位置，以及受舊資料行主要金鑰保護之對應資料行加密金鑰的加密值。| 請參閱以下範例。 | 否 | 否

### <a name="part-2-security-administrator"></a>第 2 部分︰安全性系統管理員

安全性系統管理員會產生新的資料行主要金鑰、用新的資料行主要金鑰將受影響的資料行加密金鑰重新加密，然後與 DBA 共用新資料行主要金鑰的相關資訊，以及受影響之資料行加密金鑰的新加密值集。

| Task | 發行項 | 存取純文字金鑰/金鑰存放區| 存取資料庫
|:---|:---|:---|:---
|步驟 1： 從 DBA 取得舊資料行主要金鑰的位置和相對應之資料行加密金鑰 (使用舊的資料行主要金鑰保護) 的加密值。|N/A<br>請參閱以下範例。|否| 否
|步驟 2： 在金鑰存放區中建立新的資料行主要金鑰。<br><br>**注意：** SqlServer 模組不支援此步驟。 若要從命令列完成這項工作，您需要使用金鑰存放區類型特有的工具。|[建立及儲存 Always Encrypted 的資料行主要金鑰](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)| 是 | 否
|步驟 3： 啟動 PowerShell 環境並匯入 SqlServer 模組。 | [匯入 SqlServer 模組](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 否 | 否
|步驟 4： 建立 SqlColumnMasterKeySettings 物件，其中包含 **舊的** 資料行主要金鑰位置相關資訊。 SqlColumnMasterKeySettings 是存在於 PowerShell 記憶體中的物件。 |New-SqlColumnMasterKeySettings| 否 | 否
|步驟 5。 建立 SqlColumnMasterKeySettings 物件，其中包含 **新的** 資料行主要金鑰位置相關資訊。 SqlColumnMasterKeySettings 是存在於 PowerShell 記憶體中的物件。 若要建立它，您需要使用金鑰存放區特有的 Cmdlet。 | [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)| 否 | 否
|步驟 6. 向 Azure 驗證，若您目前的資料行主要金鑰或舊的 (目前的) 資料行主要金鑰儲存在 Azure 金鑰保存庫。 | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | 是 | 否
|步驟 7： 使用新的資料行主要金鑰將每個資料行加密金鑰值重新加密，資料行加密金鑰目前是使用舊的資料行主要金鑰保護。 | [New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)<br><br>**注意︰** 呼叫這個 Cmdlet 時，請針對舊和新的資料行主要金鑰傳遞 SqlColumnMasterKeySettings 物件，以及資料行加密金鑰的值，以便重新加密。|是|否
|步驟 8。 將新資料行主要金鑰 (資料行主要金鑰的提供者名稱與金鑰路徑) 的位置，以及資料行加密金鑰的新加密值設定提供給您的 DBA。| 請參閱以下範例。 | 否 | 否

> [!NOTE]
> 強烈建議您不要在輪替之後永久刪除舊的資料行主要金鑰。 而是應該將舊的資料行主要金鑰保留在其目前金鑰存放區中，或將它封存在另一個安全的地方。 如果您將資料庫從備份檔案還原到設定新資料行主要金鑰之前  的某個時間點，則需要舊的金鑰才能存取資料。

### <a name="part-3-dba"></a>第 3 部分︰DBA

DBA 建立新資料行主要金鑰的中繼資料，並更新受影響之資料行加密金鑰的中繼資料，以新增新的加密值集。 在此步驟中，DBA 也會與查詢加密資料行之應用程式的系統管理員協調，系統管理員會確定應用程式可以存取新的資料行主要金鑰。 一旦所有應用程式都已設定為使用新的資料行主要金鑰，DBA 會移除舊的加密值集和舊的資料行主要金鑰中繼資料。

| Task | 發行項 | 存取純文字金鑰/金鑰存放區| 存取資料庫
|:---|:---|:---|:---
|步驟 1： 從安全性系統管理員取得新資料行主要金鑰的位置和新的相對應之資料行加密金鑰 (使用舊的資料行主要金鑰保護) 的加密值集。| 請參閱以下範例。 | 否 | 否
|步驟 2： 啟動 PowerShell 環境並匯入 SqlServer 模組。 | [匯入 SqlServer 模組](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 否 | 否
|步驟 3： 連接到您的伺服器和資料庫。 | [連線至資料庫](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 否 | 是
|步驟 4： 建立 SqlColumnMasterKeySettings 物件，其中包含新資料行主要金鑰位置的相關資訊。 SqlColumnMasterKeySettings 是存在於 PowerShell 記憶體中的物件。 |New-SqlColumnMasterKeySettings| 否| 否
|步驟 5。 在資料庫中建立新資料行主要金鑰的相關中繼資料。|[New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**注意：** 實際上，這個 Cmdlet 會發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 陳述式來建立金鑰中繼資料。 | 否 | 是
|步驟 6. 擷取關於資料行加密金鑰 (受到舊的資料行主要金鑰保護) 的中繼資料。| [Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)| 否 | 是
|步驟 7： 將新的加密值 (使用新的資料行主要金鑰所產生) 加入每個受影響之資料行加密金鑰的中繼資料。|[Add-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)|否|是
|步驟 8。 與在資料庫中查詢加密資料行 (且使用舊的資料行主要金鑰保護) 之所有應用程式的系統管理員協調，讓他們可以確保應用程式可以存取新的資料行主要金鑰。|[建立及儲存資料行主要金鑰 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)| 否|否
|步驟 9. 從資料庫移除與舊資料行主要金鑰相關聯的加密值，完成輪替。<br><br>**注意：** 在執行此步驟之前，請先確定查詢使用舊資料行主要金鑰保護之加密資料行的所有應用程式，已設定為使用新的資料行主要金鑰。 如果您提前執行此步驟，這些應用程式中可能有些會無法解密資料。<br><br>這個步驟會移除舊資料行主要金鑰和它所保護的資料行加密金鑰之間的關聯。 | [Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)<br><br>您也可以使用 [Remove-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue) | 否|是
|步驟 10： 從資料庫移除舊的資料行主要金鑰中繼資料| [Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)| 否|是

### <a name="rotating-a-column-master-key-with-role-separation-windows-certificate-example"></a>輪替資料行主要金鑰，並進行角色分離 (Windows 憑證範例)

以下指令碼是端對端範例，它會產生新的資料行主要金鑰，此金鑰是 Windows 憑證存放區中的憑證，並且輪替現有 (目前) 資料行主要金鑰，將它取代成新的資料行主要金鑰。 指令碼假設目標資料庫包含名為 CMK1 (要被輪替) 的資料行主要金鑰，它會將某些資料行加密金鑰加密。

第 1 部分︰DBA

```powershell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Retrieve the data about the old column master key, which needs to be rotated.
$oldCmkName = "CMK1"
$oldCmk = Get-SqlColumnMasterKey -Name $oldCmkName -InputObject $database


# Share the location of the old column master key with a Security Administrator, via a CSV file on a share drive.
$oldCmkDataFile = "Z:\oldcmkdata.txt"
"KeyStoreProviderName, KeyPath" > $oldCmkDataFile
$oldCmk.KeyStoreProviderName +", " + $oldCmk.KeyPath >> $oldCmkDataFile


# Find column encryption keys associated with the old column master key and provide the encrypted values of column encryption keys to the Security Administrator, via a CSV file on a share drive.
$ceks = Get-SqlColumnEncryptionKey -InputObject $database
$oldCekValuesFile = "Z:\oldcekvalues.txt"
"CEKName, CEKEncryptedValue" > $oldCekValuesFile 
for($i=0; $i -lt $ceks.Length; $i++){
    if($ceks[$i].ColumnEncryptionKeyValues.Length -eq 2) {
        # This column encryption has 2 encrypted values - let's check, if it is associated with the old column master key.
        if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName -or $ceks[$i].ColumnEncryptionKeyValues[1].ColumnMasterKeyName -eq $oldCmkName) {
            Write-Host $ceks[$i].Name "already has 2 encrypted values and therefore" $oldCmkName + "cannot be rotated"
            exit 1
        }
    }
    if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName) {# This column encryption key has 1 encrypted value that was produced using the old column master key
        # Save the name and the encrypted value of the column encryption key in the file.
        $encryptedValue =  "0x" + -join ($ceks[$i].ColumnEncryptionKeyValues[0].EncryptedValue |  foreach {$_.ToString("X2") } )
        $ceks[$i].Name + "," + $encryptedValue >> $oldCekValuesFile
    }
} 
```


第 2 部分︰安全性系統管理員

```powershell
# Obtain the location of the old column master key and the encrypted values of the corresponding column encryption keys, from your DBA, via a CSV file on a share drive.
$oldCmkDataFile = "Z:\oldcmkdata.txt"
$oldCmkData = Import-Csv $oldCmkDataFile
$oldCekValuesFile = "Z:\oldcekvalues.txt"
$oldCekValues = @(Import-Csv $oldCekValuesFile)

# Create a new column master key in Windows Certificate Store.
$storeLocation = "CurrentUser"
$certPath = "Cert:\" + $storeLocation + "\My"
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation $certPath -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Create a SqlColumnMasterKeySettings object for your old column master key. 
$oldCmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $oldCmkData.KeyStoreProviderName -KeyPath $oldCmkData.KeyPath

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation $storeLocation -Thumbprint $cert.Thumbprint


# Prepare a CSV file, you will use to share the encrypted values of column encryption keys, produced using the new column master key.
$newCekValuesFile = "Z:\newcekvalues.txt"
"CEKName, CEKEncryptedValue" > $newCekValuesFile

# Re-encrypt each value with the new column master key and save the new encrypted value in the file.
for($i=0; $i -lt $oldCekValues.Count; $i++){
    # Re-encrypt each value with the new CMK
    $newValue = New-SqlColumnEncryptionKeyEncryptedValue -TargetColumnMasterKeySettings $newCmkSettings -ColumnMasterKeySettings $oldCmkSettings -EncryptedValue $oldCekValues[$i].CEKEncryptedValue
    $oldCekValues[$i].CEKName + ", " + $newValue >> $newCekValuesFile
}

# Share the new column master key data with your DBA, via a CSV file.
$newCmkDataFile = $home + "\newcmkdata.txt"
"KeyStoreProviderName, KeyPath" > $newCmkDataFile
$newCmkSettings.KeyStoreProviderName +", " + $newCmkSettings.KeyPath >> $newCmkDataFile
```


第 3 部分︰DBA

```powershell
# Obtain the location of the new column master key and the new encrypted values of the corresponding column encryption keys, from your Security Administrator, via a CSV file on a share drive.
$newCmkDataFile = "Z:\newcmkdata.txt"
$newCmkData = Import-Csv $newCmkDataFile
$newCekValuesFile = "Z:\newcekvalues.txt"
$newCekValues = @(Import-Csv $newCekValuesFile)

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $newCmkData.KeyStoreProviderName -KeyPath $newCmkData.KeyPath
# Create metadata for the new column master key in the database.
$newCmkName = "CMK2"
New-SqlColumnMasterKey -Name $newCmkName -InputObject $database -ColumnMasterKeySettings $newCmkSettings


# Get all CEK objects
$oldCmkName = "CMK1"
$ceks = Get-SqlColumnEncryptionKey -InputObject $database
for($i=0; $i -lt $ceks.Length; $i++){
    if($ceks[$i].ColumnEncryptionKeyValues.Length -eq 2) {# This column encryption key has 2 encrypted values. Let's check, if it is associated with the old CMK.
        if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName -or $ceks[$i].ColumnEncryptionKeyValues[1].ColumnMasterKeyName -eq $oldCmkName) {
            Write-Host $ceks[$i].Name "already has 2 encrypted values and therefore" $oldCmkName + "cannot be rotated"
            exit 1
        }
    }
    if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName) {
        # Find the corresponding new encrypted value, received from the Security Administrator.
        $newValueRow = ($newCekValues| Where-Object {$_.CEKName -eq $ceks[$i].Name }[0])
        # Update the column encryption key metadata object by adding the new encrypted value
        Add-SqlColumnEncryptionKeyValue -ColumnMasterKeyName $newCmkName -Name $ceks[$i].Name -EncryptedValue $newValueRow.CEKEncryptedValue -InputObject $database 
    }
}

# Complete the rotation of the current column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName  -InputObject $database

# Remove the old column master key.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```

## <a name="rotating-a-column-encryption-key"></a>輪替資料行加密金鑰

輪替資料行加密金鑰包括解密將使用要被輪替之金鑰加密的所有資料行中的資料，然後使用新的資料行加密金鑰重新加密資料。 此輪替工作流程需要同時存取金鑰和資料庫，因此無法在分離角色的情況下執行。 如果包含輪替中金鑰所加密之資料行的資料表很大，則輪替資料行加密金鑰可能需要較長的時間。 因此，您的組織需要仔細規劃資料行加密金鑰輪替。

您可以使用離線或線上方法來輪替資料行加密金鑰。 前一個方法可能比較快，但您的應用程式無法寫入受影響的資料表。 第二種方法可能需要更長的時間，但您可以限制時間間隔，應用程式在該期間內無法使用受影響的資料表。 如需詳細資訊，請參閱[使用 Always Encrypted 搭配 PowerShell 設定資料行加密](configure-column-encryption-using-powershell.md)和 [Set-SqlColumnEncryption](/powershell/module/sqlserver/set-sqlcolumnencryption/)。

| Task | 發行項 | 存取純文字金鑰/金鑰存放區| 存取資料庫
|:---|:---|:---|:---
|步驟 1： 啟動 PowerShell 環境並匯入 SqlServer 模組。 | [匯入 SqlServer 模組](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | 否 | 否
|步驟 2： 連接到您的伺服器和資料庫。 | [連線至資料庫](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 否 | 是
|步驟 3： 向 Azure 驗證，如果您的資料行主要金鑰 (用於保護資料行加密金鑰，且要被輪替) 儲存在 Azure 金鑰保存庫中的話。 | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | 是 | 否
|步驟 4： 產生新的資料行加密金鑰，並使用資料行主要金鑰將它加密，然後在資料庫中建立資料行加密金鑰中繼資料。  | [New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)<br><br>**注意：** 請使用一種可在內部產生並加密資料行加密金鑰的 Cmdlet。<br>實際上，這個 Cmdlet 會發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 陳述式來建立金鑰中繼資料。 | 是 | 是
|步驟 5。 尋找使用舊資料行加密金鑰加密的所有資料行。 | [SQL Server 管理物件 (SMO) 程式設計指南](../../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md) | 否 | 是
|步驟 6. 為每個受影響的資料行建立 *SqlColumnEncryptionSettings* 物件。  SqlColumnMasterKeySettings 是存在於 PowerShell 記憶體中的物件。 它會指定資料行的目標加密配置。 在此情況下，該物件應該指定須使用新的資料行加密金鑰來加密受影響的資料行。 | [New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings) | 否 | 否
|步驟 7： 使用新的資料行加密金鑰，重新加密在步驟 5 中識別的資料行。 | [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)<br><br>**注意︰** 此步驟可能需要很長的時間。 根據您選取的方法 (線上與離線) 而定，您的應用程式可能無法在整個作業期間或作業的部分期間存取資料表。 | 是 | 是
|步驟 8。 移除舊資料行加密金鑰的中繼資料。 | [Remove-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey) | 否 | 是

### <a name="example---rotating-a-column-encryption-key"></a>範例 - 輪替資料行加密金鑰

以下的指令碼將示範輪替資料行加密金鑰。  指令碼會假設目標資料庫包含使用名為 CEK1 (要被輪替) 的資料行加密金鑰所加密的部分資料行，這個資料行加密金鑰是使用名為 CMK1 (資料行主要金鑰不會儲存在 Azure Key Vault 中) 的資料行主要金鑰來保護。 


```powershell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Generate a new column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cmkName = "CMK1"
$newCekName = "CEK2"
New-SqlColumnEncryptionKey -Name $newCekName -InputObject $database -ColumnMasterKey $cmkName 


# Find all columns encrypted with the old column encryption key, and create a SqlColumnEncryptionSetting object for each column.
$ces = @()
$oldCekName = "CEK1"
$tables = $database.Tables
for($i=0; $i -lt $tables.Count; $i++){
    $columns = $tables[$i].Columns
    for($j=0; $j -lt $columns.Count; $j++) {
        if($columns[$j].isEncrypted -and $columns[$j].ColumnEncryptionKeyName -eq $oldCekName) {
            $threeColPartName = $tables[$i].Schema + "." + $tables[$i].Name + "." + $columns[$j].Name 
            $ces += New-SqlColumnEncryptionSettings -ColumnName $threeColPartName -EncryptionType $columns[$j].EncryptionType -EncryptionKey $newCekName
        }
     }
}

# Re-encrypt all columns, currently encrypted with the old column encryption key, using the new column encryption key.
Set-SqlColumnEncryption -ColumnEncryptionSettings $ces -InputObject $database -UseOnlineApproach -MaxDowntimeInSeconds 120 -LogFileDirectory .

# Remove the old column encryption key metadata.
Remove-SqlColumnEncryptionKey -Name $oldCekName -InputObject $database
```

## <a name="next-steps"></a>後續步驟
- [使用 Always Encrypted 與 SQL Server Management Studio 查詢資料行](always-encrypted-query-columns-ssms.md)
- [使用 Always Encrypted 開發應用程式](always-encrypted-client-development.md)
  
## <a name="see-also"></a>另請參閱
- [一律加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 的金鑰管理概觀](overview-of-key-management-for-always-encrypted.md) 
- [使用 PowerShell 設定 Always Encrypted](configure-always-encrypted-using-powershell.md)
- [使用 SQL Server Management Studio 輪替 Always Encrypted 金鑰](rotate-always-encrypted-keys-using-ssms.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
