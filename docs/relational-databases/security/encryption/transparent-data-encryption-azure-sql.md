---
title: "Azure SQL Database 和資料倉儲的 TDE | Microsoft Docs"
description: "SQL Database 和資料倉儲的透明資料加密概觀。 本文涵蓋 TDE 的優點與組態選項，包括「受服務管理的 TDE」和「自行管理金鑰 (BYOK)」。"
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: cguyer
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: On Demand
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: 35c94a39989fda76ea023588b2d7a3aa4e463262
ms.contentlocale: zh-tw
ms.lasthandoff: 09/05/2017

---
# <a name="transparent-data-encryption-for-azure-sql-database-and-data-warehouse"></a>SQL Database 和資料倉儲的透明資料加密
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

透明資料加密 (Transparent Data Encryption, TDE) 可即時執行資料庫、相關聯備份及交易記錄檔的即時加密與解密，完全無須變更應用程式，就能協助保護 Azure SQL Database 和資料倉儲免受惡意活動所造成的威脅。

TDE 會使用一種名稱為資料庫加密金鑰 (DEK) 的對稱金鑰，將整個資料庫的儲存體加密。 這個資料庫加密金鑰受到 TDE 保護裝置的保護，而保護裝置是指受服務管理的憑證 (「受服務管理的 TDE」) 或儲存在 Azure Key Vault 的非對稱金鑰 (「自行管理金鑰」)。 TDE 保護裝置是設在伺服器層級。 

在資料庫啟動時，即會將加密的 DEK 解密，然後用於解密和重新加密 SQL 引擎處理序中的資料庫檔案。 TDE 會在分頁層次上執行資料的即時 I/O 加密和解密。 在系統將每個頁面讀取到記憶體中時，它會將其解密，並在寫入磁碟之前加密。 如需 TDE 的一般描述，請參閱[透明資料加密 (TDE)](transparent-data-encryption.md)。

在 Azure 虛擬機器上執行的 SQL Server 也可以使用 Key Vault 中的非對稱金鑰。 其設定步驟與使用 Azure SQL Database 中的非對稱金鑰不同。 如需詳細資訊，請參閱[使用 Azure Key Vault 進行可延伸金鑰管理 (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md)。

## <a name="service-managed-tde"></a>受服務管理的 TDE

在 Azure 中，TDE 的預設值是資料庫加密金鑰由內建的伺服器憑證保護。 每部伺服器各有其專用的內建伺服器憑證。 如果資料庫具有地理複寫關聯性，則主要資料庫和地理次要資料庫均會受到主要資料庫父伺服器金鑰的保護。 如有 2 個資料庫同時連線到同一部伺服器，則這兩個資料庫會共用同一個內建憑證。 Microsoft 會每隔 90 天自動輪換這些憑證。

Microsoft 也會順暢地移動和管理金鑰，以滿足地理複寫和還原作業的需要。 

> [!IMPORTANT]
> 根據預設，所有新建立的 SQL 資料庫會以受服務管理的 TDE 來加密。 現有的資料庫和 2017 年 5 月以前透過還原、地理複寫和資料庫複本建立的資料庫，則預設為不加密。
>

## <a name="bring-your-own-key"></a>自行管理金鑰

自行管理金鑰 (BYOK) 支援可讓使用者充分掌控自身的 TDE 加密金鑰，並控制存取的人員與時間。 Azure Key Vault (AKV) 是 Azure 的雲端式外部金鑰管理系統，也是 TDE 針對 BYOK 支援所整合的第一項金鑰管理服務。 使用 BYOK 時，AKV 中儲存的非對稱金鑰會保護資料庫加密金鑰。 非對稱金鑰永遠不會離開 Key Vault；一旦伺服器擁有 Key Vault 的權限，伺服器就會透過 Key Vault 服務，將基本金鑰的作業要求傳送給它。 非對稱金鑰是在伺服器層級設定，因此歸屬於該伺服器底下的所有資料庫都會繼承此金鑰。 現在，BYOK 支援可讓使用者控制金鑰管理工作，包括金鑰輪替、Key Vault 權限、刪除金鑰，以及啟用所有加密金鑰的稽核/報告。 Key Vault 提供集中式的金鑰管理、利用嚴密監控的硬體安全性模組 (HSM)，並促進金鑰和資料的分開管理作業，以協助符合法規合規性。 若要深入了解 Key Vault，請前往 [Key Vault 文件頁面](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)。

若要深入了解 Azure SQL Database 和資料倉儲的 TDE 與 BYOK 支援，請參閱[支援自行管理金鑰的透明資料加密](transparent-data-encryption-byok-azure-sql.md)。

若要開始使用支援 BYOK 的 TDE，請瀏覽[使用 PowerShell 開啟透明資料加密，並自行管理 Key Vault 金鑰](transparent-data-encryption-byok-azure-sql-configure.md)使用說明指南。

## <a name="moving-a-tde-protected-database"></a>移動 TDE 保護的資料庫

您無須解密資料庫，即可在 Azure 執行作業。 目標會自動繼承來源資料庫或主要資料庫的 TDE 設定。 這包括下列作業：
- 異地還原
- 自助時間點還原
- 還原已刪除的資料庫
- 使用中的地理複寫
- 建立資料庫複本

匯出 TDE 保護的資料庫時，不會對匯出的資料庫內容進行加密。 此匯出內容會儲存在未加密的 BACPAC 檔案中。 請務必為 BACPAC 檔案施以適當的保護措施，並在匯入新資料庫作業完成時，立即啟用 TDE。

例如，如果從內部部署 SQL Server 匯出 BACPAC 檔案，則新資料庫的匯入內容不會自動加密。 同樣地，如果將 BACPAC 檔案匯出到內部部署 SQL Server，新資料庫也不會自動加密。

其中一個例外是在 Azure SQL Database 之間進行匯出的時候。 新的資料庫會啟用 TDE，但 BACPAC 檔案本身仍未加密。

## <a name="managing-transparent-data-encryption-in-the-azure-portal"></a>在 Azure 入口網站中管理透明資料加密

若要透過 Azure 入口網站設定 TDE，您必須以 Azure 擁有者、參與者或 SQL 安全性管理員的身分連線。 

透明資料加密是設在資料庫層級。 若要啟用資料庫的 TDE，請前往 [Azure 入口網站](https://portal.azure.com)，並使用您的 Azure 系統管理員或參與者帳戶登入。 在您的使用者資料庫下方，找到 TDE 設定。 預設會使用受服務管理的 TDE，且自動為含有該資料庫的伺服器產生 TDE 憑證。 

![受服務管理的 TDE](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

TDE 的主要金鑰是設在伺服器層級，也稱為「TDE 保護裝置」。 若要使用支援自行管理金鑰的 TDE，並使用 Azure Key Vault 的金鑰來保護資料庫，請瀏覽伺服器下方的 TDE 設定。 

![支援 BYOK 的 TDE](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="managing-transparent-data-encryption-using-powershell"></a>使用 PowerShell 管理透明資料加密

若要透過 PowerShell 設定 TDE，您必須以 Azure 擁有者、參與者或 SQL 安全性管理員的身分連線。 

| 指令程式 | Description |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |啟用或停用資料庫的 TDE。|
| [Get-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |取得資料庫的 TDE 狀態。 |
| [Get-AzureRmSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |檢查資料庫的加密進度。 |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |將 Key Vault 金鑰新增至 SQL Server。 |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |取得 SQL Server 的 Key Vault 金鑰。 |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |設定 SQL Server 的 TDE 保護裝置。 |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |取得透明資料加密 (TDE) 保護裝置。 |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |從 SQL Server 移除 Key Vault 金鑰。 |
|  | |

## <a name="managing-transparent-data-encryption-using-transact-sql"></a>使用 Transact-SQL 管理透明資料加密

使用 master 資料庫中 **dbmanager** 角色的系統管理員或成員身分來登入，以連接到資料庫。

| Command | Description |
| --- | --- |
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) | 使用 SET ENCRYPTION ON/OFF 來加密或解密資料庫。 |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |傳回關於資料庫加密狀態及其相關聯之資料庫加密金鑰的資訊。 |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |傳回每個資料庫倉儲節點的加密狀態，及其相關聯資料庫的加密金鑰相關資訊。 | 
|  | |

您無法使用 Transact-SQL，將 TDE 保護裝置切換至 Azure Key Vault 金鑰；請使用 PowerShell 或 Azure 入口網站。

## <a name="managing-transparent-data-encryption-using-rest-api"></a>使用 REST API 管理透明資料加密
 
若要透過 REST API 設定 TDE，您必須以 Azure 擁有者、參與者或 SQL 安全性管理員的身分連線。 

| Command | Description |
| --- | --- |
|[建立或更新伺服器](/rest/api/sql/servers/createorupdate)|將 AAD 身分識別新增至 SQL Server (用來授與 Key Vault 的存取權)。|
|[建立或更新伺服器金鑰](/rest/api/sql/serverkeys/createorupdate)|將 Key Vault 金鑰新增至 SQL Server。|
|[刪除伺服器金鑰](/rest/api/sql/serverkeys/delete)|從 SQL Server 移除 Key Vault 金鑰。|
|[取得伺服器金鑰](/rest/api/sql/serverkeys/get)|從 SQL Server 取得特定 Key Vault 金鑰。|
|[依據伺服器列出伺服器金鑰](/rest/api/sql/serverkeys/listbyserver)|取得 SQL Server 的 Key Vault 金鑰。|
|[建立或更新加密保護裝置](/rest/api/sql/encryptionprotectors/createorupdate)|設定 SQL Server 的 TDE 保護裝置。|
|[取得加密保護裝置](/rest/api/sql/encryptionprotectors/get)|取得 SQL Server 的 TDE 保護裝置。|
|[依據伺服器列出加密保護裝置](/rest/api/sql/encryptionprotectors/listbyserver)|取得 SQL Server 的 TDE 保護裝置。|
|[建立或更新透明資料加密組態](/rest/api/sql/transparentdataencryptions/createorupdate)|啟用或停用資料庫的 TDE。|
|[取得透明資料加密組態](/rest/api/sql/transparentdataencryptions/get)|取得資料庫的 TDE 組態。|
|[列出透明資料加密組態結果](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|取得資料庫的加密結果。|

## <a name="next-steps"></a>後續的步驟

- 如需 TDE 的一般描述，請參閱[透明資料加密 (TDE)](transparent-data-encryption.md)。

- 若要深入了解 Azure SQL Database 和資料倉儲的 TDE 與 BYOK 支援，請瀏覽[支援自行管理金鑰的透明資料加密](transparent-data-encryption-byok-azure-sql.md)。

- 若要開始使用支援 BYOK 的 TDE，請瀏覽[使用 PowerShell 開啟透明資料加密，並自行管理 Key Vault 金鑰](transparent-data-encryption-byok-azure-sql-configure.md)使用說明指南。

- 如需 Key Vault 的詳細資訊，請參閱 [Key Vault 文件頁面](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)。

