---
title: Always Encrypted 精靈 | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2016
ms.prod: sql
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.alwaysencryptedwizard.encryption.f1
- sql13.swb.alwaysencryptedwizard.f1
- sql.swb.alwaysencryptedwizard.masterkey.f1
helpviewer_keywords:
- Wizard, Always Encrypted
ms.assetid: 68daddc9-ce48-49aa-917f-6dec86ad5af5
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bc80b486a6231020447cba3a3ab899fc9e699965
ms.sourcegitcommit: 3762dd447ca4bb449eda8476e72f393db0851b38
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/18/2018
ms.locfileid: "46013503"
---
# <a name="always-encrypted-wizard"></a>永遠加密精靈
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

使用 [永遠加密精靈]  ，協助保護儲存在 SQL Server 資料庫中的機密資料。 一律加密可讓用戶端將用戶端應用程式內的機密資料進行加密，且永遠不會顯示 SQL Server 的加密金鑰。 如此一來，「永遠加密」功能即可區隔擁有資料 (且可以檢視資料) 的使用者和管理資料 (但不應具備存取權) 的使用者。  如需此功能的完整描述，請參閱 [永遠加密 &#40;Database Engine&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)。  
 
 - 如需示範如何透過精靈設定 [永遠加密] 功能，並在用戶端應用程式加以運用的完整逐步解說，請參閱 [SQL Database 教學課程︰透過永遠加密來保護敏感性資料](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)。  
 
 - 如需使用精靈的影片，請參閱 [Keeping Sensitive Data Secure with Always Encrypted](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)。 此外，請參閱 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全性小組部落格的 [SSMS Encryption Wizard - Enabling Always Encrypted in a Few Easy Steps](http://blogs.msdn.com/b/sqlsecurity/archive/2015/11/01/ssms-encryption-wizard-enabling-always-encrypted-made-easy.aspx)(SSMS 加密精靈 - 幾個簡單步驟即可啟用永遠加密)。  
 
 - **權限︰** 若要使用此精靈來查詢加密資料行及選取金鑰，您必須具有 `VIEW ANY COLUMN MASTER KEY DEFINITION` 和 `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` 權限。 若要建立新的金鑰，您也必須具有 `ALTER ANY COLUMN MASTER KEY` 和 `ALTER ANY COLUMN ENCRYPTION KEY` 權限。  
 
 #### <a name="to-open-the-always-encrypted-wizard"></a>若要開啟永遠加密精靈  
 
 1.  使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的物件總管元件，連接到您的 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。  
   
 2.  以滑鼠右鍵按一下您的資料庫，指向 [工作]，然後按一下 [加密資料行]。  
   
 ## <a name="column-selection-page"></a>資料行選取頁面  
 - 找出資料表與資料行，然後針對所選資料行選取加密類型 (確定性或隨機) 和加密金鑰。 若要解密目前加密的資料行，請選取 [純文字] 。 若要旋轉資料行加密金鑰，請選取不同的加密金鑰，精靈即會解密資料行，並以新的金鑰重新加密該資料行。 (雖然 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援加密時態表和記憶體中的資料表，但精靈無法對此進行設定。)  
 
## <a name="master-key-configuration-page"></a>主要金鑰設定頁面  
 - 在 Windows 憑證存放區或 Azure 金鑰保存庫中，建立新的資料行主要金鑰。 如需詳細資訊，請參閱 [金鑰儲存] 底下的連結。  
 
 - 如果您在 [資料行選取] 頁面中選擇自動產生的資料行加密金鑰，則必須設定要與產生的資料行加密金鑰搭配進行加密的資料行主要金鑰。 如果您已在資料庫定義資料行主要金鑰，則可加以選取  (若要使用現有的資料行主要金鑰，使用者必須具有金鑰的存取權限)。或者，您可以在所選的金鑰存放區 (Windows 憑證存放區或 Azure 金鑰保存庫) 中產生資料行主要金鑰，並在資料庫中定義金鑰。  
 
 ### <a name="key-storage"></a>**金鑰儲存**  
 
 - 選擇要儲存資料行主要金鑰的位置。  
 
   - **將主要金鑰儲存在 Windows 憑證存放區** ：如需詳細資訊，請參閱 [Using Certificate Stores](/windows/desktop/SecCrypto/using-certificate-stores)  
 
   - **將主要金鑰儲存在 Azure 金鑰保存庫** ：如需詳細資訊，請參閱 [開始使用 Azure 金鑰保存庫](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)。  
 
 - 若要在 Azure 金鑰保存庫中產生資料行主要金鑰，使用者必須擁有金鑰保存庫的 **WrapKey**、 **UnwrapKey**、 **Verify**以及 **Sign** 權限。 使用者可能也需要 **Get**、 **List**、 **Create**、 **Delete**、 **Update**、 **Import**、 **Backup**以及 **Restore** 權限。 如需詳細資訊，請參閱 [什麼是 Azure 金鑰保存庫？](https://azure.microsoft.com/documentation/articles/key-vault-whatis/) 和   [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx)。  
 
 - 精靈只支援兩種選項。 您必須使用 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 來設定硬體安全模組和用戶端儲存庫。  
 
 ## <a name="always-encrypted-terms"></a>永遠加密相關字詞  
 
 - **確定性加密** 使用的方法一律會針對任何指定純文字值產生相同加密值。 使用確定性加密時，可以進行分組、依等號比較進行篩選，和根據加密值聯結資料表，但也可讓未經授權的使用者透過檢視加密資料行中的模式，猜測加密值的相關資訊。 只要其中有一小組可能的加密值時 (例如 True/False 或北/南/東/西區域)，就會增加此弱點。 確定性加密必須針對字元資料行使用 binary2 排序次序的資料行定序。  
 
 - **隨機加密** 使用的方法會以更難預測的方式來加密資料。 隨機加密較為安全，但會防止等號比較搜尋、分組、編製索引和聯結加密的資料行。  

 - **資料行主要金鑰** 是用來加密資料行加密金鑰的保護金鑰。 資料行主要金鑰必須儲存於信任的金鑰存放區。 有關資料行主要金鑰的資訊 (包含其位置) 都儲存於系統目錄檢視的資料庫中。  

 - **資料行加密金鑰** 是用來加密儲存於資料庫資料行中的機密資料。 您可以使用單一資料行加密金鑰來加密資料行中的所有值。 資料行加密金鑰的加密值會儲存於系統目錄檢視的資料庫中。 您應該將資料行加密金鑰存放在安全/信任的位置以作為備份。  

 ## <a name="see-also"></a>另請參閱  
 - [永遠加密 &#40;Database Engine&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 - [使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
