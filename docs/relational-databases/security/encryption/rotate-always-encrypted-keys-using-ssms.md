---
title: 使用 SQL Server Management Studio 輪替 Always Encrypted 金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
- sql13.SWB.COLUMNMASTERKEY.CLEANUP.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5d0a96f061f01749194cd3f0d1be1aae5443ff8a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "73595703"
---
# <a name="rotate-always-encrypted-keys-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 輪替 Always Encrypted 金鑰
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本文描述使用 [SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md) 輪替 Always Encrypted 資料行主要金鑰和資料行加密金鑰的工作。

如需 Always Encrypted 金鑰管理概觀，包括最佳做法建議和重要安全性考量，請參閱 [Always Encrypted 的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。

<a name="rotatecmk"></a>
## <a name="rotate-column-master-keys"></a>輪替資料行主要金鑰 

資料行主要金鑰輪替是一項以新資料行主要金鑰來取代現有資料行主要金鑰的程序。 如果金鑰已遭洩漏，或是為了符合您的組織原則或必須定期輪替授權密碼編譯金鑰的標準規定，您可能必須輪替金鑰。 資料行主要金鑰輪替包含解密目前資料行主要金鑰所保護的資料行加密金鑰、使用新的資料行主要金鑰重新進行加密，以及更新金鑰中繼資料。 

### <a name="step-1-provision-a-new-column-master-key"></a>步驟 1:佈建新的資料行主要金鑰

請遵循[使用 [新增資料行主要金鑰] 對話方塊佈建資料行主要金鑰](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog)中的步驟。

### <a name="step-2-encrypt-column-encryption-keys-with-the-new-column-master-key"></a>步驟 2:使用新的資料行主要金鑰來加密資料行加密金鑰

資料行主要金鑰通常會保護一或多個資料行加密金鑰。 每個資料行加密金鑰在資料庫中皆存有加密值，其為使用資料行主要金鑰將資料行加密金鑰加密的產物。
在此步驟中，使用新資料行主要金鑰，將輪替中資料行主要金鑰所保護的每個資料行加密金鑰加密，並將新加密值儲存在資料庫中。 因此，每個受到輪替影響的資料行加密金鑰皆會有兩個加密值︰其中一個值是由現有資料行主要金鑰加密，而另一個新值是由新資料行主要金鑰加密。

1.  使用**物件總管**巡覽至 [安全性] > [Always Encrypted 金鑰] > [資料行主要金鑰]  資料夾，找出您要輪替的資料行主要金鑰。
2.  以滑鼠右鍵按一下資料行主要金鑰，然後選取 [輪替]  。
3.  在 [資料行主要金鑰輪替]  對話方塊的 [目標]  欄位中，選取您在步驟 1 中建立之新資料行主要金鑰的名稱。
4.  檢閱現有資料行主要金鑰所保護的資料行加密金鑰清單。 這些金鑰將會受到輪替影響。
5.  按一下 [確定]  。

SQL Server Management Studio 將會取得舊資料行主要金鑰所保護之資料行加密金鑰的中繼資料，以及舊與新資料行主要金鑰的中繼資料。 SSMS 接著將使用資料行主要金鑰中繼資料來存取包含舊資料行主要金鑰的金鑰存放區，並解密資料行加密金鑰。 接著，SSMS 將存取保存新資料行主要金鑰的金鑰存放區，以產生資料行加密金鑰的一組新加密值，接著將新值新增至中繼資料 (產生並發出 [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 陳述式)。

> [!NOTE]
> 請確定舊資料行主要金鑰所加密的每個資料行加密金鑰，皆不會由任何其他資料行主要金鑰所加密。 換句話說，每個受到替換影響的資料行加密金鑰，在資料庫中皆必須正好只有一個加密值。 如果任何受影響的資料行加密金鑰有一個以上的加密值，則您需要移除該值，才可以繼續使用輪替 (請參閱步驟 4  了解如何移除資料行加密金鑰的加密值)。

### <a name="step-3-configure-your-applications-with-the-new-column-master-key"></a>步驟 3：使用新的資料行主要金鑰來設定應用程式

在此步驟中，您需要確定查詢輪替中資料行主要金鑰所保護的資料庫資料行 (也就是使用資料行加密金鑰加密的資料庫資料行，而該加密金鑰由輪替中資料行主要金鑰加密) 的所有用戶端應用程式，皆可以存取新資料行主要金鑰。 此步驟取決於新資料行主要金鑰所在金鑰存放區的類型。 例如：

- 若新資料行主要金鑰是儲存在 Windows 憑證存放區的憑證，則您需要將憑證部署至同一個憑證存放區位置 (「目前使用者」  或「本機電腦」  )，作為資料庫中資料行主要金鑰的金鑰路徑中所指定的位置。 應用程式必須能夠存取憑證︰
  - 如果憑證儲存在「目前使用者」  憑證存放區位置中，憑證必須匯入應用程式的 Windows 身分識別 (使用者) 的「目前使用者」存放區。
  - 如果憑證儲存在「本機電腦」  憑證存放區位置中，應用程式的 Windows 身分識別必須有權存取憑證。
- 若新資料行主要金鑰儲存在 Microsoft Azure 金鑰保存庫中，就必須實作應用程式，使其可以向 Azure 驗證並有權存取金鑰。

如需詳細資料，請參閱[建立及儲存 Always Encrypted 的資料行主要金鑰](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

> [!NOTE]
> 在輪替的這個時間點，舊資料行主要金鑰和新資料行主要金鑰皆為有效，且可以用來存取資料。

### <a name="step-4-clean-up-column-encryption-key-values-encrypted-with-the-old-column-master-key"></a>步驟 4：清除使用舊資料行主要金鑰來加密的資料行加密金鑰值

將所有應用程式設定為使用新資料行主要金鑰後，從資料庫移除舊  資料行主要金鑰所加密的資料行加密金鑰值。 移除舊值可確保您準備好進行下一個輪替 (請記住，要輪替的資料行主要金鑰所保護的每個資料行加密金鑰皆必須正好只有一個加密值)。

另一個要在封存或移除舊資料行主要金鑰前清除舊值的原因與效能相關：在查詢加密資料行時，已啟用永遠加密的用戶端驅動程式可能需要嘗試解密兩個值︰舊值和新值。 驅動程式不知道在應用程式環境中，這兩個資料行主要金鑰哪一個有效，因此驅動程式會從伺服器擷取這兩個加密值。 若其中一個值是受到已無法使用的資料行主要金鑰 (例如該舊資料行主要金鑰已從存放區移除) 保護而造成解密失敗，則驅動程式會嘗試使用新資料行主要金鑰來解密另一個值。

> [!WARNING]
> 若您先行移除資料行加密金鑰的值，而應用程式尚無法使用其對應的資料行主要金鑰，則該應用程式將無法再解密資料庫資料行。

1.  使用物件總管  ，巡覽至 [安全性] > [永遠加密金鑰]  資料夾，並找出要取代的現有資料行主要金鑰。
2.  以滑鼠右鍵按一下現有資料行主要金鑰，然後選取 [清除]  。
3.  檢閱要移除的資料行加密金鑰值清單。
4.  按一下 [確定]  。

SQL Server Management Studio 將會發出 [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 陳述式，來捨棄舊資料行主要金鑰所加密之資料行加密金鑰的加密值。

### <a name="step-5-delete-metadata-for-your-old-column-master-key"></a>步驟 5：刪除舊資料行主要金鑰的中繼資料

如果您選擇從資料庫移除舊資料行主要金鑰的定義，請使用下列步驟。

1. 使用物件總管  ，巡覽至 安全性 > 永遠加密金鑰} > 資料行主要金鑰  資料夾，然後找出要從資料庫移除的舊資料行主要金鑰。
2. 以滑鼠右鍵按一下舊資料行主要金鑰，然後選取 [刪除]  。 (這樣會產生並發出 [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) 陳述式來移除資料行主要金鑰中繼資料)。
3. 按一下 [確定]  。

> [!NOTE]
> 強烈建議您不要在輪替之後永久刪除舊的資料行主要金鑰。 而是應該將舊的資料行主要金鑰保留在其目前金鑰存放區中，或將它封存在另一個安全的地方。 如果您將資料庫從備份檔案還原到設定新資料行主要金鑰之前的某個時間點，則需要舊的金鑰才能存取資料。

### <a name="permissions-for-rotating-column-master-key"></a>輪替資料行主要金鑰的權限

輪替資料行主要金鑰需要下列資料庫權限︰

- **ALTER ANY COLUMN MASTER KEY** - 建立新資料行主要金鑰的中繼資料以及刪除舊資料行主要金鑰之中繼資料時的必要項目。
- **ALTER ANY COLUMN ENCRYPTION KEY** - 修改資料行加密金鑰中繼資料 (新增加密值) 時的必要項目。

您也需要可以在金鑰存放區中存取舊資料行主要金鑰和新資料行主要金鑰。 若要存取金鑰存放區，並使用資料行主要金鑰，您可能需要金鑰存放區和/或金鑰的權限︰
- **憑證存放區 - 本機電腦** - 您必須具有當成資料行主要金鑰使用之憑證的讀取權，或為電腦上的系統管理員。
- **Azure Key Vault** - 您需要有包含資料行主要金鑰之保存庫的 *create*、*get*、*unwrapKey*、*wrapKey*、*sign* 和 *verify* 權限。
- **金鑰存放區提供者 (CNG)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 KSP 設定)。
- **密碼編譯服務提供者 (CAPI)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 CSP 設定)。

如需詳細資訊，請參閱[建立及儲存 Always Encrypted 的資料行主要金鑰](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

<a name="rotatecek"></a> 
## <a name="rotate-column-encryption-keys"></a>輪替資料行加密金鑰

輪替資料行加密金鑰包括解密該金鑰所加密之所有資料行中要轉出的資料，以及使用新的資料行加密金鑰重新加密資料。

>[!NOTE]
> 如果包含輪替中金鑰所加密之資料行的資料表很大，則輪替資料行加密金鑰可能需要很長的時間。 正在重新加密資料時，您的應用程式無法寫入受影響的資料表中。 因此，您的組織需要非常仔細地規劃資料行加密金鑰輪替。
若要輪替資料行加密金鑰，請使用 [永遠加密精靈]。

1.  開啟資料庫的精靈：以滑鼠右鍵按一下資料庫，並指向 [工作]  ，然後按一下 [加密資料行]  。
2.  檢閱[簡介]  頁面，然後按一下 [下一步]  。
3.  在 [資料行選取]  頁面上，展開資料表，然後找出舊資料行加密金鑰目前所加密且您想要取代的所有資料行。
4.  針對舊資料行加密金鑰所加密的每個資料行，將 [加密金鑰]  設定為自動產生的新金鑰。 **注意：** 您也可以先建立新的資料行加密金鑰，然後執行精靈，請參閱[使用 [新增資料行加密金鑰] 對話方塊佈建資料行加密金鑰](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)。
5.  在 [主要金鑰組態]  頁面上，選取要儲存新金鑰的位置，並選取主要金鑰來源，然後按一下 [下一步]  。 **注意：** 如果您使用的是現有資料行加密金鑰，而非自動產生的資料行加密金鑰，則不需要在這個頁面上執行任何動作。
6.  在 [驗證]  頁面上，選擇是否要立即執行指令碼或建立 PowerShell 指令碼，然後按一下 [下一步]  。
7.  在 [摘要]  頁面上，檢閱您已選取的選項，並按一下 [完成]  ，然後在完成時關閉精靈。
8.  使用物件總管  ，巡覽至 [安全性]/[永遠加密金鑰]/[資料行加密金鑰]  資料夾，然後找出要從資料庫移除的舊資料行加密金鑰。 以滑鼠右鍵按一下金鑰，然後選取 [刪除]  。

### <a name="permissions-for-rotating-column-encryption-keys"></a>輪替資料行加密金鑰的權限

輪替資料行加密金鑰需要下列資料庫權限：**ALTER ANY COLUMN MASTER KEY** - 如果您使用新的自動產生資料行加密金鑰 (也會產生新資料行主要金鑰和其新的中繼資料)，此為必要項目。
**ALTER ANY COLUMN ENCRYPTION KEY** - 為新的資料行加密金鑰增新中繼資料時的必要項目。

您也需要可以存取新和舊資料行加密金鑰的資料行主要金鑰。 若要存取金鑰存放區，並使用資料行主要金鑰，您可能需要金鑰存放區和/或金鑰的權限︰
- **憑證存放區 - 本機電腦** - 您必須具有當成資料行主要金鑰使用之憑證的讀取權，或為電腦上的系統管理員。
- **Azure Key Vault** - 您需要有包含資料行主要金鑰之保存庫的 get、unwrapKey 和 verify 權限。
- **金鑰存放區提供者 (CNG)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 KSP 設定)。
- **密碼編譯服務提供者 (CAPI)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 CSP 設定)。

如需詳細資訊，請參閱[建立及儲存 Always Encrypted 的資料行主要金鑰](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

## <a name="next-steps"></a>後續步驟
- [使用 Always Encrypted 與 SQL Server Management Studio 查詢資料行](always-encrypted-query-columns-ssms.md)
- [使用 Always Encrypted 開發應用程式](always-encrypted-client-development.md)

## <a name="see-also"></a>另請參閱
- [一律加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 的金鑰管理概觀](overview-of-key-management-for-always-encrypted.md) 
- [使用 SQL Server Management Studio 設定 Always Encrypted](configure-always-encrypted-using-sql-server-management-studio.md)
- [使用 PowerShell 設定 Always Encrypted](configure-always-encrypted-using-powershell.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
