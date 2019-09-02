---
title: 可延伸金鑰管理 (EKM) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Key Management
- Extensible Key Management
- EKM, described
ms.assetid: 9bfaf500-2d1e-4c02-b041-b8761a9e695b
author: aliceku
ms.author: aliceku
ms.openlocfilehash: 1526a23955a5e39f3f70ebe9a457560514e164fb
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2019
ms.locfileid: "70148790"
---
# <a name="extensible-key-management-ekm"></a>可延伸金鑰管理 (EKM)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會針對加密和金鑰產生使用「Microsoft 密碼編譯 API」  (MSCAPI) 提供者，藉以提供加密功能以及「可延伸金鑰管理」  (EKM)。 用於資料和金鑰加密的加密金鑰會建立於暫時性金鑰容器中，而且您必須先從提供者中匯出這些金鑰，然後再將它們儲存於資料庫中。 這個方法會讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]處理金鑰管理 (包括加密金鑰階層和金鑰備份)。  
  
 隨著法規相符的需求和資料隱私權的考量逐漸增加，許多組織便運用加密技術來提供「深度防護」解決方案。 這種方法通常不實用，因為它僅使用資料庫加密管理工具。 硬體廠商會提供使用「硬體安全模組」  (HSM) 來處理企業金鑰管理的產品。 HSM 裝置會將加密金鑰儲存在硬體或軟體模組上。 這是較安全的解決方案，因為加密金鑰不會與加密資料一起存放。  
  
 目前許多廠商會針對金鑰管理和加密速度提供 HSM。 HSM 裝置會使用硬體介面搭配伺服器處理序，當做應用程式與 HSM 之間的中繼。 此外，廠商也會在模組 (可能是硬體或軟體) 上實作 MSCAPI 提供者。 MSCAPI 通常只會提供 HSM 所提供的部分功能。 而且，廠商也可以針對 HSM、金鑰組態和金鑰存取提供管理軟體。  
  
 HSM 實作方式會因廠商而不同，而且若要使用它們搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，就需要公用介面。 雖然 MSCAPI 會提供此介面，但是它僅支援部分 HSM 功能。 此外，它也具有其他限制，例如無法以原生方式保存對稱金鑰，而且缺乏工作階段導向的支援。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可延伸金鑰管理可讓 EKM/HSM 協力廠商在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中註冊其模組。 註冊之後， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用者就可以使用儲存在 EKM 模組上的加密金鑰。 這可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存取這些模組支援的進階加密功能 (例如大量加密和解密) 和金鑰管理函數 (例如金鑰過時和金鑰輪替)。  
  
 在 Azure VM 中執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以使用儲存在 [Azure 金鑰保存庫](https://go.microsoft.com/fwlink/?LinkId=521401)中的金鑰。 如需詳細資訊，請參閱 [使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)處理金鑰管理 (包括加密金鑰階層和金鑰備份)。  
  
## <a name="ekm-configuration"></a>EKM 組態  
 並非每一個 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]版本都可使用可延伸金鑰管理。 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 根據預設，可延伸金鑰管理處於關閉狀態。 若要啟用這項功能，請使用具有下列選項和值的 sp_configure 命令，如下列範例所示：  
  
```  
sp_configure 'show advanced', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'EKM provider enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
> [!NOTE]  
>  如果您在不支援 EKM 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本上，針對這個選項使用 sp_configure 命令，將會收到錯誤。  
  
 若要停用此功能，請將值設定為 **0**。 如需如何設定伺服器選項的詳細資訊，請參閱 [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
## <a name="how-to-use-ekm"></a>如何使用 EKM  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可延伸金鑰管理可讓保護資料庫檔案的加密金鑰儲存在外部裝置中，例如智慧卡、USB 裝置或 EKM/HSM 模組。 此外，這項功能也可讓資料庫管理員進行資料保護 (除了系統管理員 (sysadmin) 群組的成員以外)。 資料可以使用只有資料庫使用者可在外部 EKM/HSM 模組上存取的加密金鑰進行加密。  
  
 可延伸金鑰管理也會提供下列優點：  
  
-   額外的授權檢查 (啟用責任分隔)。  
  
-   硬體架構加密/解密的效能較高。  
  
-   外部加密金鑰產生。  
  
-   外部加密金鑰儲存 (實體分隔資料和金鑰)。  
  
-   加密金鑰擷取。  
  
-   外部加密金鑰保留 (啟用加密金鑰循環)。  
  
-   加密金鑰復原更容易。  
  
-   可管理的加密金鑰散發。  
  
-   安全的加密金鑰處置。  
  
 您可以將可延伸金鑰管理用於使用者名稱和密碼組合，或是 EKM 驅動程式所定義的其他方法。  
  
> [!CAUTION]  
>  若要進行疑難排解， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 技術支援部門可能會需要 EKM 提供者的加密金鑰。 此時，您可能也需要存取廠商工具或處理序來協助解決問題。  
  
### <a name="authentication-with-an-ekm-device"></a>使用 EKM 裝置進行驗證  
 EKM 模組可以支援多種驗證類型。 但是，每個提供者只會公開一種驗證類型給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，也就是說，如果此模組支援基本驗證或其他驗證類型，它就會公開其中一種驗證類型，而不會同時公開這兩種。  
  
#### <a name="ekm-device-specific-basic-authentication-using-usernamepassword"></a>使用使用者名稱/密碼的 EKM 裝置特有基本驗證  
 對於這些使用「使用者名稱/密碼」  配對來支援基本驗證的 EKM 模組而言，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會使用認證來提供透明驗證。 如需認證的詳細資訊，請參閱[認證 &#40;Database Engine&#41;](../../../relational-databases/security/authentication-access/credentials-database-engine.md)。  
  
 您可以針對 EKM 提供者建立認證，並將它對應至登入 (Windows 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帳戶)，以便按照登入存取 EKM 模組。 認證的 [身分識別]  欄位包含使用者名稱，而 [密碼]  欄位則包含用來連接至 EKM 模組的密碼。  
  
 如果 EKM 提供者沒有任何登入對應認證，系統就會使用對應至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶的認證。  
  
 一個登入可以具有多個對應認證，只要這些認證用於不同的 EKM 提供者即可。 但是，每個登入的每個 EKM 提供者必須只有一個對應認證。 相同的認證可對應至其他登入。  
  
#### <a name="other-types-of-ekm-device-specific-authentication"></a>其他 EKM 裝置特有的驗證類型  
 對於具有 Windows 或「使用者/密碼」  組合以外驗證的 EKM 模組而言，就必須獨立於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外執行驗證。  
  
### <a name="encryption-and-decryption-by-an-ekm-device"></a>EKM 裝置的加密和解密  
 您可以使用下列函數和功能搭配對稱與非對稱金鑰，加密和解密資料：  
  
|函數或功能|參考|  
|-------------------------|---------------|  
|對稱金鑰加密|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|非對稱金鑰加密|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|EncryptByKey(key_guid, '純文字', ...)|[ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)|  
|DecryptByKey(加密文字, ...)|[DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)|  
|EncryptByAsmKey(key_guid, 'cleartext')|[ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)|  
|DecryptByAsmKey(ciphertext)|[DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
  
#### <a name="database-keys-encryption-by-ekm-keys"></a>EKM 金鑰的資料庫金鑰加密  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以使用 EKM 金鑰來加密資料庫中的其他金鑰。 您可以在 EKM 裝置上建立及使用對稱和非對稱金鑰。 您可以使用 EKM 非對稱金鑰來加密原生 (非 EKM) 對稱金鑰。  
  
 下列範例會建立資料庫對稱金鑰，然後使用 EKM 模組上的金鑰來加密該資料庫對稱金鑰。  
  
```  
CREATE SYMMETRIC KEY Key1  
WITH ALGORITHM = AES_256  
ENCRYPTION BY EKM_AKey1;  
GO  
--Open database key  
OPEN SYMMETRIC KEY Key1  
DECRYPTION BY EKM_AKey1  
```  
  
 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中資料庫和伺服器金鑰的詳細資訊，請參閱 [SQL Server 和資料庫加密金鑰 &#40;Database Engine&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)。  
  
> [!NOTE]  
>  您無法使用某個 EKM 金鑰來加密另一個 EKM 金鑰。  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不支援使用 EKM 提供者產生的非對稱金鑰來簽署模組。  
  
## <a name="related-tasks"></a>相關工作  
 [EKM provider enabled 伺服器組態選項](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
  
 [使用 EKM 在 SQL Server 上啟用 TDE](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
 [使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [sys.cryptographic_providers &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)   
 [sys.dm_cryptographic_provider_sessions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-sessions-transact-sql.md)   
 [sys.dm_cryptographic_provider_properties &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-properties-transact-sql.md)   
 [sys.dm_cryptographic_provider_algorithms &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-algorithms-transact-sql.md)   
 [sys.dm_cryptographic_provider_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-keys-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [備份與還原 Reporting Services 加密金鑰](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [刪除和重新建立加密金鑰 &#40;SSRS 組態管理員&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [加入和移除向外延展部署的加密金鑰 &#40;SSRS 組態管理員&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [備份服務主要金鑰](../../../relational-databases/security/encryption/back-up-the-service-master-key.md)   
 [還原服務主要金鑰](../../../relational-databases/security/encryption/restore-the-service-master-key.md)   
 [建立資料庫主要金鑰](../../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [備份資料庫主要金鑰](../../../relational-databases/security/encryption/back-up-a-database-master-key.md)   
 [還原資料庫主要金鑰](../../../relational-databases/security/encryption/restore-a-database-master-key.md)   
 [在兩部伺服器上建立相同的對稱金鑰](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
