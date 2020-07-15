---
title: 使用 [Always Encrypted 精靈] 設定資料行加密 | Microsoft Docs
description: 了解如何透過使用 SQL Server 中的 [Always Encrypted 精靈]，以設定資料庫資料行的 Always Encrypted 組態。
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.alwaysencryptedwizard.encryption.f1
- sql13.swb.alwaysencryptedwizard.f1
- sql13.swb.alwaysencryptedwizard.masterkey.f1
helpviewer_keywords:
- Wizard, Always Encrypted
ms.assetid: 68daddc9-ce48-49aa-917f-6dec86ad5af5
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f592004e96a9b469a56bc9ff85b8f4080af38406
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85627448"
---
# <a name="configure-column-encryption-using-always-encrypted-wizard"></a>使用 [Always Encrypted 精靈] 設定資料行加密
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

[Always Encrypted 精靈] 是一個功能強大的工具，可讓您設定所選取資料庫資料行所需的 [Always Encrypted](always-encrypted-database-engine.md) 設定。 根據目前設定和所需目標設定，精靈可以加密資料行、將其解密 (移除加密) 或重新加密 (例如，使用新的資料行加密金鑰，或與針對資料行所設定目前類型不同的加密類型)。 在精靈的單一執行中，可以設定多個資料行。

精靈可讓您使用現有資料行加密金鑰來加密資料行，或您可以選擇產生新的資料行加密金鑰，或同時產生新資料行加密金鑰和新資料行主要金鑰。 

精靈的運作方式是將資料移出資料庫，並在 SSMS 處理序中執行密碼編譯作業。 精靈會在資料庫中建立具有所需加密設定的新資料表、從原始資料表載入所有資料、執行所要求的密碼編譯作業、將資料上傳至新資料表，然後交換原始資料表與新資料表。

> [!NOTE]
> 執行密碼編譯作業可能需要很長的時間。 在這段期間，資料庫無法寫入交易。 PowerShell 是在較大資料表上進行密碼編譯作業時的建議工具。 請參閱[使用 Always Encrypted 與 PowerShell 設定資料行加密](configure-column-encryption-using-powershell.md)。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> 如果您使用 [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] 且 SQL Server 執行個體是以安全記憶體保護區進行設定，您可以就地執行密碼編譯作業，而不需要將資料移出資料庫。 請參閱[使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密](always-encrypted-enclaves-configure-encryption.md)。 請注意，此精靈不支援就地加密。

::: moniker-end

建議使用 PowerShell 

 - 如需端對端逐步解說，其示範如何使用精靈來設定 Always Encrypted 並在用戶端應用程式中使用，請參閱下列 Azure SQL Database 教學課程：
    - [使用 Always Encrypted 和 Windows 憑證存放區中資料行主要金鑰保護 Azure SQL Database 中的敏感性資料](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)
    - [使用 Always Encrypted 和 Azure Key Vault 中資料行主要金鑰保護 Azure SQL Database 中的敏感性資料](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted-azure-key-vault)

 - 如需使用精靈的影片，請參閱 [Keeping Sensitive Data Secure with Always Encrypted](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)。 此外，請參閱 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全性小組部落格的 [SSMS Encryption Wizard - Enabling Always Encrypted in a Few Easy Steps](https://techcommunity.microsoft.com/t5/SQL-Server/SSMS-Encryption-Wizard-Enabling-Always-Encrypted-in-a-Few-Easy/ba-p/384545)(SSMS 加密精靈 - 幾個簡單步驟即可啟用永遠加密)。  
 - 如需 Always Encrypted 金鑰的資訊，請參閱 [Always Encrypted 金鑰管理概觀](overview-of-key-management-for-always-encrypted.md)。
 - 如需 Always Encrypted 中所支援加密類型的資訊，請參閱[選取決定性加密或隨機加密](always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。
 
 ## <a name="permissions"></a>權限
若要使用精靈來執行密碼編譯作業，您必須具備 **VIEW ANY COLUMN MASTER KEY DEFINITION** 和 **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** 權限。 您也必須具備在保存金鑰的金鑰存放區中，存取您正在使用資料行主要金鑰的權限：
- **憑證存放區 - 本機電腦** - 您必須具有當成資料行主要金鑰使用之憑證的讀取權，或為電腦上的系統管理員。
- **Azure Key Vault** - 您需要有包含資料行主要金鑰之保存庫的 get、unwrapKey 和 verify 權限。
- **金鑰存放區提供者 (CNG)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 KSP 設定)。
- **密碼編譯服務提供者 (CAPI)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 CSP 設定)。

此外，若您正在使用精靈建立新的金鑰，您必須具備[使用 [新增資料行主要金鑰] 對話方塊佈建資料行主要金鑰](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog)及[使用 [新增資料行加密金鑰] 對話方塊佈建資料行加密金鑰](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)中所列的額外權限。

## <a name="open-the-always-encrypted-wizard"></a>開啟 [Always Encrypted 精靈]
您可以在三個不同層級啟動精靈： 
- 資料庫層級 - 若您想要加密位於不同資料表中的多個資料行。
- 資料表層級 - 若您想要加密位於相同資料表中的多個資料行。
- 資料行層級 - 若您想要加密單一特定資料行。
 
 1. 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的物件總管元件，連接到您的 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。  
   
 2. 加密：
     1. 資料庫中位於不同資料表內的多個資料行：請以滑鼠右鍵按一下您的資料庫、指向 [工作]，然後選取 [加密資料行]。
     1. 位於相同資料表中的多個資料行：請巡覽至資料表、以滑鼠右鍵按一下資料表，然後選取 [加密資料行]。
     1. 個別資料行：請巡覽至資料行、以滑鼠右鍵按一下資料行，然後選取 [加密資料行]。


   
 ## <a name="column-selection-page"></a>資料行選取頁面
在此頁面中，您可以選取您想要加密、重新加密或解密的資料行，且您可以為所選取的資料行定義目標加密設定。

若要加密純文字資料行 (並未加密的資料行)，請為資料行選取加密類型 ([決定性] 或 [隨機]) 和加密金鑰。 

若要為已加密的資料行變更加密類型或輪替 (變更) 資料行加密金鑰，請選取所需的加密類型和金鑰。 

若您想要精靈使用新的資料行加密金鑰加密或重新加密一或多個資料行，請挑選其名稱中包含 **(新增)** 的金鑰。 精靈將會產生金鑰。

若要解密目前已加密的資料行，請針對加密類型選取 [純文字]。


> [!NOTE]
> 精靈不支援在時態性和記憶體內部資料表上進行密碼編譯作業。 您可以使用 Transact-SQL 建立空白的時態性或記憶體內部資料表，並使用您的應用程式插入資料。

## <a name="master-key-configuration-page"></a>主要金鑰設定頁面
若您已在上一個頁面為任何資料行選取自動產生的資料行加密金鑰，在此頁面中您需要選取現有的資料行主要金鑰，或設定將加密資料行加密金鑰的新資料行主要金鑰。 

設定新的資料行主要金鑰時，您可以在 Windows 憑證存放區或 Azure Key Vault 中挑選現有金鑰，並讓精靈只為資料庫中的金鑰建立中繼資料物件，或選擇同時產生金鑰及描述資料庫中金鑰的中繼資料物件。 

如需在 Windows 憑證存放區、Azure Key Vault 或其他金鑰存放區中建立和儲存資料行主要金鑰的詳細資訊，請參閱[對 Always Encrypted 建立和儲存資料行主要金鑰](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

> [!TIP]
> 精靈只允許您在 Windows 憑證存放區和 Azure Key Vault 中瀏覽和建立金鑰。 精靈也會自動產生兩個新金鑰的名稱，以及描述金鑰的資料庫中繼資料物件。 若您需要深入控制您金鑰的佈建方式 (以及針對包含您資料行主要金鑰的金鑰存放區擁有更多選擇)，您可以先使用 [新增資料行主要金鑰] 和 [新增資料行加密金鑰] 對話方塊來建立金鑰，然後執行精靈並挑選您已建立的金鑰。 請參閱[使用 [新增資料行主要金鑰] 對話方塊佈建資料行主要金鑰](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog)和[使用 [新增資料行加密金鑰] 對話方塊佈建資料行加密金鑰](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)。 

## <a name="next-steps"></a>後續步驟
- [使用 Always Encrypted 與 SQL Server Management Studio 查詢資料行](always-encrypted-query-columns-ssms.md)
- [使用 Always Encrypted 開發應用程式](always-encrypted-client-development.md)

## <a name="see-also"></a>另請參閱  
 - [一律加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
 - [Always Encrypted 的金鑰管理概觀](overview-of-key-management-for-always-encrypted.md) 
 - [使用 SQL Server Management Studio 設定 Always Encrypted](configure-always-encrypted-using-sql-server-management-studio.md)
 - [使用 PowerShell 佈建 Always Encrypted 金鑰](configure-always-encrypted-keys-using-powershell.md)
 - [使用 Always Encrypted 與 PowerShell 設定資料行加密](configure-column-encryption-using-powershell.md)
 - [使用 Always Encrypted 與 DAC 套件設定資料行加密](configure-always-encrypted-using-dacpac.md)
