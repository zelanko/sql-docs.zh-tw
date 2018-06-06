---
title: Azure SQL Database 和資料倉儲的透明資料加密 | Microsoft Docs
description: SQL Database 和資料倉儲的透明資料加密概觀。 本文件涵蓋透明資料加密的優點與設定選項，包括「受控服務的透明資料加密」和「攜帶您自己的金鑰 (BYOK)」。
keywords: ''
author: becczhang
manager: craigg
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.component: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.date: 05/08/2018
ms.author: rebeccaz
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: b88dfeac58ef9c00307b2cfee35aca3ea0549f02
ms.sourcegitcommit: feff98b3094a42f345a0dc8a31598b578c312b38
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2018
---
# <a name="transparent-data-encryption-for-sql-database-and-data-warehouse"></a>SQL Database 和資料倉儲的透明資料加密
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

透明資料加密 (TDE) 可協助 Azure SQL Database 和 Azure 資料倉儲防範惡意活動所帶來的威脅。 它可即時執行資料庫、相關聯備份及交易記錄檔的即時加密與解密，完全無須變更應用程式。 預設會為所有新部署的 Azure SQL Database 啟用 TDE，但針對舊版資料庫，您可能需要手動啟用。  

透明資料加密會使用一種稱為資料庫加密金鑰的對稱金鑰，將整個資料庫的儲存體加密。 此資料庫加密金鑰受到透明資料加密保護裝置保護。 保護裝置是指受控服務的憑證 (受控服務的透明資料加密) 或儲存在 Azure Key Vault 的非對稱金鑰 (攜帶您自己的金鑰)。 請在伺服器層級上設定透明資料加密保護裝置。 

在資料庫啟動時，即會將加密的資料庫加密金鑰解密，然後用於解密和重新加密 SQL Server Database 引擎處理序中的資料庫檔案。 透明資料加密會在頁面層級上執行資料的即時 I/O 加密和解密。 在系統將每個頁面讀取到記憶體中時，它會將其解密，然後在寫入磁碟之前加密。 如需透明資料加密的一般描述，請參閱[透明資料加密](transparent-data-encryption.md)。

在 Azure 虛擬機器上執行的 SQL Server 也可以使用 Key Vault 中的非對稱金鑰。 其設定步驟與使用 SQL Database 中的非對稱金鑰不同。 如需詳細資訊，請參閱[使用 Azure Key Vault 進行可延伸金鑰管理 (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md)。

## <a name="service-managed-transparent-data-encryption"></a>受控服務的透明資料加密

在 Azure 中，透明資料加密的預設值是資料庫加密金鑰由內建的伺服器憑證保護。 每部伺服器各有其專用的內建伺服器憑證。 如果資料庫具有異地複寫關聯性，則主要資料庫和異地次要資料庫均會受到主要資料庫父伺服器金鑰的保護。 如有兩個資料庫同時連線到同一部伺服器，則這兩個資料庫會共用同一個內建憑證。 Microsoft 會每隔 90 天自動輪換這些憑證。

Microsoft 也會順暢地移動和管理金鑰，以滿足異地複寫和還原作業的需要。 

> [!IMPORTANT]
> 根據預設，所有新建立的 SQL 資料庫會以受控服務的透明資料加密來加密。 現有的資料庫和 2017 年 5 月以前透過還原、異地複寫和資料庫複本建立的資料庫，則預設為不加密。
>

## <a name="bring-your-own-key"></a>自行管理金鑰

透過攜帶您自己的金鑰支援，可讓您充分掌控透明資料加密金鑰，並控制存取的人員與時間。 Key Vault 是 Azure 的雲端式外部金鑰管理系統，也是透明資料加密與「攜帶您自己的金鑰」支援整合的第一項金鑰管理服務。 使用「攜帶您自己的金鑰」支援，資料庫加密金鑰即受到儲存在 Key Vault 的非對稱金鑰保護。 非對稱金鑰永遠不會離開 Key Vault。 伺服器擁有 Key Vault 的權限之後，伺服器就會透過 Key Vault，將基本金鑰的作業要求傳送給它。 請在伺服器層級設定非對稱金鑰，因此歸屬於該伺服器底下的所有資料庫都會繼承此金鑰。

利用「攜帶您自己的金鑰」支援，您現在可以控制金鑰管理工作，例如金鑰輪替和 Key Vault 權限。 您也可以刪除金鑰，以及對所有加密金鑰啟用稽核/報告功能。 Key Vault 提供集中式金鑰管理，並且使用受嚴密監視的硬體安全性模組。 Key Vault 促使分開管理金鑰和資料，以協助符合法規相符性。 若要深入了解 Key Vault，請參閱 [Key Vault 文件頁面](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)。

若要深入了解 SQL Database 和資料倉儲的透明資料加密與「攜帶您自己的金鑰」支援，請參閱[支援攜帶您自己的金鑰的透明資料加密](transparent-data-encryption-byok-azure-sql.md)。

若要開始使用支援「攜帶您自己的金鑰」的透明資料加密，請瀏覽[透過 PowerShell，使用自行管理的 Key Vault 金鑰開啟透明資料加密](transparent-data-encryption-byok-azure-sql-configure.md)使用說明指南。

## <a name="move-a-transparent-data-encryption-protected-database"></a>移動受透明資料加密保護的資料庫

您無須解密資料庫，即可在 Azure 執行作業。 目標會自動繼承來源資料庫或主要資料庫的 透明資料加密設定。 包含的作業牽涉到：
- 異地還原。
- 自助時間點還原。
- 還原已刪除的資料庫。
- 使用中的異地複寫。
- 建立資料庫複本。

當您匯出受透明資料加密保護的資料庫時，匯出的資料庫內容不會加密。 此匯出內容會儲存在未加密的 BACPAC 檔案中。 請務必為 BACPAC 檔案施以適當的保護措施，並在匯入新資料庫作業完成後，立即啟用透明資料加密。

例如，如果從內部部署 SQL Server 執行個體匯出 BACPAC 檔案，則新資料庫的匯入內容不會自動加密。 同樣地，如果將 BACPAC 檔案匯出到內部部署 SQL Server 執行個體，新資料庫也不會自動加密。

其中一個例外是匯出到 SQL Database 及從中匯出的時候。 新的資料庫會啟用透明資料加密，但 BACPAC 檔案本身仍未加密。

## <a name="manage-transparent-data-encryption-in-the-azure-portal"></a>在 Azure 入口網站中管理透明資料加密

若要透過 Azure 入口網站設定透明資料加密，您必須以 Azure 擁有者、參與者或 SQL 安全性管理員的身分連線。 

請在資料庫層級上設定透明資料加密。 若要啟用資料庫的透明資料加密，請前往 [Azure 入口網站](https://portal.azure.com)，並使用您的 Azure 系統管理員或參與者帳戶登入。 在您的使用者資料庫底下尋找透明資料加密設定。 根據預設，會使用受控服務的透明資料加密。 包含資料庫的伺服器會自動產生透明資料加密憑證。 

![受控服務的透明資料加密](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

請在伺服器層級上設定透明資料加密主要金鑰，也就是透明資料加密保護裝置。 若要使用支援「攜帶您自己的金鑰」的透明資料加密，並使用 Key Vault 中的金鑰來保護資料庫，請參閱伺服器底下的透明資料加密設定。 

![支援「攜帶您自己的金鑰」的透明資料加密](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="manage-transparent-data-encryption-by-using-powershell"></a>使用 PowerShell 管理透明資料加密

若要透過 PowerShell　設定透明資料加密，您必須以 Azure 擁有者、參與者或 SQL 安全性管理員的身分連線。 

| 指令程式 | 描述 |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |啟用或停用資料庫的透明資料加密|
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |取得資料庫的透明資料加密狀態 |
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption-Activity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |檢查資料庫的加密進度 |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |將 Key Vault 金鑰新增至 SQL Server 執行個體 |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |為 SQL Server 執行個體取得 Key Vault 金鑰  |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |為 SQL Server 執行個體設定透明資料加密保護裝置 |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |取得透明資料加密保護裝置 |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |從 SQL Server 執行個體移除 Key Vault 金鑰 |
|  | |

## <a name="manage-transparent-data-encryption-by-using-transact-sql"></a>使用 Transact-SQL 管理透明資料加密

使用 master 資料庫中 **dbmanager** 角色的系統管理員或成員身分來登入，以連接到資料庫。

| 命令 | 描述 |
| --- | --- |
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) | SET ENCRYPTION ON/OFF 可加密或解密資料庫 |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |傳回關於資料庫加密狀態及其相關聯之資料庫加密金鑰的資訊 |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |傳回關於每個資料庫倉儲節點的加密狀態，及其相關聯之資料庫加密金鑰的資訊 | 
|  | |

您無法使用 Transact SQL，　將透明資料加密保護裝置切換為 Key Vault 中的金鑰。 請使用 PowerShell 或 Azure 入口網站。

## <a name="manage-transparent-data-encryption-by-using-the-rest-api"></a>使用 REST API 管理透明資料加密
 
若要透過 REST API 設定透明資料加密，您必須以 Azure 擁有者、參與者或 SQL 安全性管理員的身分連線。 

| 命令 | 描述 |
| --- | --- |
|[建立或更新伺服器](/rest/api/sql/servers/createorupdate)|將 Azure Active Directory 身分識別新增至 SQL Server 執行個體 (用來授與 Key Vault 的存取權)|
|[建立或更新伺服器金鑰](/rest/api/sql/serverkeys/createorupdate)|將 Key Vault 金鑰新增至 SQL Server 執行個體|
|[刪除伺服器金鑰](/rest/api/sql/serverkeys/delete)|從 SQL Server 執行個體移除 Key Vault 金鑰|
|[取得伺服器金鑰](/rest/api/sql/serverkeys/get)|從 SQL Server 執行個體取得特定的 Key Vault 金鑰|
|[依據伺服器列出伺服器金鑰](/rest/api/sql/serverkeys/listbyserver)|為 SQL Server 執行個體取得 Key Vault 金鑰 |
|[建立或更新加密保護裝置](/rest/api/sql/encryptionprotectors/createorupdate)|為 SQL Server 執行個體設定透明資料加密保護裝置|
|[取得加密保護裝置](/rest/api/sql/encryptionprotectors/get)|為 SQL Server 執行個體取得透明資料加密保護裝置|
|[依據伺服器列出加密保護裝置](/rest/api/sql/encryptionprotectors/listbyserver)|為 SQL Server 執行個體取得透明資料加密保護裝置 |
|[建立或更新透明資料加密組態](/rest/api/sql/transparentdataencryptions/createorupdate)|啟用或停用資料庫的透明資料加密|
|[取得透明資料加密組態](/rest/api/sql/transparentdataencryptions/get)|取得資料庫的透明資料加密設定|
|[列出透明資料加密組態結果](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|取得資料庫的加密結果|

## <a name="next-steps"></a>後續步驟

- 如需透明資料加密的一般描述，請參閱[透明資料加密](transparent-data-encryption.md)。
- 若要深入了解 SQL Database 和資料倉儲的透明資料加密與「攜帶您自己的金鑰」支援，請參閱[支援攜帶您自己的金鑰的透明資料加密](transparent-data-encryption-byok-azure-sql.md)。
- 若要開始使用支援「攜帶您自己的金鑰」的透明資料加密，請瀏覽[透過 PowerShell，使用自行管理的 Key Vault 金鑰開啟透明資料加密](transparent-data-encryption-byok-azure-sql-configure.md)使用說明指南。
- 如需 Key Vault 的詳細資訊，請參閱 [Key Vault 文件頁面](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)。
