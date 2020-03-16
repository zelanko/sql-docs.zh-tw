---
title: 使用 SQL Server Management Studio 佈建 Always Encrypted 金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 13bb5944c5907f3bebc9f01eb969b4b8979f8c97
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287122"
---
# <a name="provision-always-encrypted-keys-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 佈建 Always Encrypted 金鑰
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本文提供使用 [SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md) 佈建 Always Encrypted 資料行主要金鑰和資料行加密金鑰的步驟。

如需 Always Encrypted 金鑰管理概觀，包括最佳做法建議和重要安全性考量，請參閱 [Always Encrypted 的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。

<a name="provisioncmk"></a>
## <a name="provision-column-master-keys-with-the-new-column-master-key-dialog"></a>使用 [新增資料行主要金鑰] 對話方塊佈建資料行主要金鑰

[新增資料行主要金鑰]  對話方塊可讓您產生資料行主要金鑰或挑選金鑰存放區中的現有金鑰，以及建立資料庫中所建立或所選取金鑰的資料行主要金鑰中繼資料。

1.  使用物件總管  ，巡覽至資料庫下的 [安全性 > 永遠加密金鑰]  資料夾。
2.  以滑鼠右鍵按一下 [資料行主要金鑰]  資料夾，然後選取 [新增資料行主要金鑰]  。 
3.  在 [新增資料行主要金鑰]  對話方塊中，輸入資料行主要金鑰中繼資料物件的名稱。
4.  選取金鑰存放區︰
    - **憑證存放區 - 目前使用者** - 指出 Windows 憑證存放區中的目前使用者憑證存放區位置 (即個人存放區)。 
    - **憑證存放區 - 本機電腦** - 指出 Windows 憑證存放區中的本機電腦憑證存放區位置。 
    - **Azure Key Vault** - 您需要登入 Azure (按一下 [登入]  )。 登入之後，就可以挑選其中一個 Azure 訂用帳戶和金鑰保存庫。
    - **金鑰存放區提供者 (KSP)** ：指出金鑰存放區，可透過實作新一代密碼編譯 (CNG) API 的金鑰存放區提供者 (KSP) 存取。 這種類型的存放區通常是硬體安全性模組 (HSM)。 在您選取此選項之後，需要挑選 KSP。 預設會選取 [ (Microsoft 軟體金鑰存放區提供者)]  。 如果您想要使用 HSM 中所儲存的資料行主要金鑰，請選取裝置的 KSP (它必須先安裝和設定於電腦上，您才能開啟對話方塊)。
    -   **密碼編譯服務提供者 (CSP)** ：一種金鑰存放區，可透過實作密碼編譯 API (CAPI) 的密碼編譯服務提供者 (CSP) 存取。 這類存放區通常是硬體安全性模組 (HSM)。 在您選取此選項之後，需要挑選 CSP。  如果您想要使用 HSM 中所儲存的資料行主要金鑰，請選取裝置的 CSP (它必須先安裝和設定於電腦上，您才能開啟對話方塊)。
    
    > [!NOTE]
    > 因為 CAPI 是已被取代的應用程式開發介面，所以預設會停用 [密碼編譯服務提供者 (CAPI)] 選項。 啟用方式是在 Windows 登錄的 **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** 金鑰下建立 CAPI Provider Enabled DWORD 值，並將其設成 1。 除非您的金鑰存放區不支援 CNG，否則您應該使用 CNG，而非 CAPI。
   
    如需上述金鑰存放區的詳細資訊，請參閱[建立及儲存 Always Encrypted 的資料行主要金鑰](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

5. 如果您使用 [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)]，且 SQL Server 執行個體已設定安全記憶體保護區，您可以選取 [允許記憶體保護區計算]  核取方塊，將主要金鑰設為已啟用記憶體保護區。 如需詳細資料，請參閱[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md)。 

    > [!NOTE]
    > 如果 SQL Server 執行個體未正確設定安全記憶體保護區，則不會出現 [允許記憶體保護區計算]  核取方塊。

6.  挑選金鑰存放區中的現有金鑰，或按一下 [產生金鑰]  或 [產生憑證]  按鈕，以在金鑰存放區中建立金鑰。 
7.  按一下 [確定]  ，新的金鑰即會顯示在清單中。 

完成對話方塊之後，SQL Server Management Studio 會在資料庫中建立資料行主要金鑰的中繼資料。 此對話方塊的做法是產生和發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 陳述式。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

如果您設定已啟用記憶體保護區的資料行主要金鑰，SSMS 也會使用資料行主要金鑰來簽署中繼資料。 

::: moniker-end

### <a name="permissions-for-provisioning-a-column-master-key"></a>佈建資料行主要金鑰的權限

您需要資料庫的 *ALTER ANY COLUMN MASTER KEY* 資料庫權限，對話方塊才能建立資料行主要金鑰。 若要使用對話方塊建立新的資料行主要金鑰，或使用金鑰存放區建立中的現有金鑰，您可能需要金鑰存放區或/和金鑰的權限：
- **憑證存放區 - 本機電腦** - 您必須具有當成資料行主要金鑰使用之憑證的讀取權，或為電腦上的系統管理員。
- **Azure Key Vault** - 您需要 *get* 和 *list* 權限來選取和使用金鑰，以及 *create* 權限來建立新的金鑰。 若要設定已啟用記憶體保護區的資料行主要金鑰，您還需要 *sign* 權限，才能產生金鑰中繼資料的簽章。
- **金鑰存放區提供者 (CNG)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 KSP 設定)。
- **密碼編譯服務提供者 (CAPI)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 CSP 設定)。

如需詳細資訊，請參閱[建立及儲存 Always Encrypted 的資料行主要金鑰](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

<a name="provisioncek"></a> 
## <a name="provision-column-encryption-keys-with-the-new-column-encryption-key-dialog"></a>使用 [新增資料行加密金鑰] 對話方塊佈建資料行加密金鑰

[新增資料行加密金鑰]  對話方塊可讓您產生資料行加密金鑰、使用資料行主要金鑰進行加密，以及在資料庫中建立資料行加密金鑰中繼資料。

1.  使用物件總管  ，巡覽至資料庫下的 [安全性]/[永遠加密金鑰]  資料夾。
2.  以滑鼠右鍵按一下 [資料行加密金鑰]  資料夾，然後選取 [新增資料行加密金鑰]  。 
3.  在 [新增資料行加密金鑰]  對話方塊中，輸入資料行加密金鑰中繼資料物件的名稱。
4.  選取代表資料庫中資料行主要金鑰的中繼資料物件。
5.  按一下 [確定]  。 

完成對話方塊之後，SQL Server Management Studio 會產生新的資料行加密金鑰，然後擷取您從資料庫所選資料行主要金鑰的中繼資料。 SSMS 接著會使用資料行主要金鑰中繼資料來連絡包含資料行主要金鑰的金鑰存放區，並加密資料行加密金鑰。 最後，SSMS 會產生並發出 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 陳述式，在資料庫中建立新資料行加密的中繼資料。

### <a name="permissions-for-provisioning-a-column-encryption-key"></a>佈建資料行加密金鑰的權限

您需要資料庫的 *ALTER ANY COLUMN ENCRYPTION KEY* 和 *VIEW ANY COLUMN MASTER KEY DEFINITION* 資料庫權限，對話方塊才能建立資料行加密金鑰中繼資料以及存取資料行主要金鑰中繼資料。
若要存取金鑰存放區，並使用資料行主要金鑰，您可能需要金鑰存放區和/或金鑰的權限︰
- **憑證存放區 - 本機電腦** - 您必須具有當成資料行主要金鑰使用之憑證的讀取權，或為電腦上的系統管理員。
- **Azure 金鑰保存庫** - 您需要有包含資料行主要金鑰之保存庫的 *get*、*unwrapKey*、*wrapKey*、*sign* 和 *verify* 權限。
- **金鑰存放區提供者 (CNG)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 KSP 設定)。
- **密碼編譯服務提供者 (CAPI)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 CSP 設定)。

如需詳細資訊，請參閱[建立及儲存資料行主要金鑰 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

## <a name="provision-always-encrypted-keys-using-the-always-encrypted-wizard"></a>使用 [Always Encrypted 精靈] 佈建 Always Encrypted 金鑰

[Always Encrypted 精靈](../../../relational-databases/security/encryption/always-encrypted-wizard.md)是用來加密、解密和重新加密所選資料庫資料行的工具。 該工具除了可以使用已設定的金鑰，也可讓您產生新資料行主要金鑰和新資料行加密。 

## <a name="next-steps"></a>後續步驟
- [使用 [Always Encrypted 精靈] 設定資料行加密](always-encrypted-wizard.md)
- [使用 Always Encrypted 與 DAC 套件設定資料行加密](configure-always-encrypted-using-dacpac.md)
- [使用 SQL Server Management Studio 輪替 Always Encrypted 金鑰](rotate-always-encrypted-keys-using-ssms.md)
- [使用 Always Encrypted 開發應用程式](always-encrypted-client-development.md)
- [使用 Always Encrypted 與 SQL Server [匯入及匯出精靈]，將資料移轉進或移轉出資料行](always-encrypted-migrate-using-import-export-wizard.md)

## <a name="see-also"></a>另請參閱
- [一律加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [建立及儲存 Always Encrypted 的資料行主要金鑰](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [使用 SQL Server Management Studio 設定 Always Encrypted](configure-always-encrypted-using-sql-server-management-studio.md)
- [使用 PowerShell 佈建 Always Encrypted 金鑰](configure-always-encrypted-keys-using-powershell.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
