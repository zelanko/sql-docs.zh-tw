---
title: 備份加密 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 334b95a8-6061-4fe0-9e34-b32c9f1706ce
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 862f97bbe21d47c830dad59e69f2c508e7eebc15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103763"
---
# <a name="backup-encryption"></a>備份加密
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份的加密選項概觀。 內容包括在備份期間加密的用法、益處和建議做法等詳細資料。  
  
  
##  <a name="Overview"></a> 概觀  
 從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]開始，SQL Server 即擁有在建立備份時加密資料的能力。 在建立備份時透過指定加密演算法及加密程式 (憑證或非對稱金鑰)，即可建立加密的備份檔案。 所有儲存目的地：支援內部部署及 Window Azure 儲存體。 此外， [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 作業可設定加密選項，此為 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]引進的新功能。  
  
 若要在備份期間加密，您必須指定加密演算法以及確保加密金鑰的加密程式。 以下為支援的加密選項：  
  
-   **加密演算法：** 支援的加密演算法包括：AES 128、AES 192、AES 256 和 Triple DES  
  
-   **加密程式：** 憑證或非對稱金鑰  
  
> [!CAUTION]  
>  備份憑證或非對稱金鑰是非常重要的，而且最好與其用以加密的備份檔案存放於不同位置。 若沒有憑證或非對稱金鑰，您將無法還原備份，而此備份檔案將無法使用。  
  
 **從加密備份還原：** 在還原期間，SQL Server 還原不要求指定任何加密參數。 但它要求用以加密備份檔案的憑證或非對稱金鑰可用於您要進行還原的執行個體上。 執行還原的使用者帳戶必須擁有憑證或金鑰的 **VIEW DEFINITION** 權限。 若您要將加密的備份還原到不同的執行個體，您必須確定憑證可用於該執行個體上。  
  
 若您要從 TDE 加密資料庫中還原備份，TDE 憑證需可用於您要進行還原的執行個體上。  
  
##  <a name="Benefits"></a> 優點  
  
1.  加密資料庫備份能幫助您確保資料的安全：SQL Server 提供建立備份時加密備份資料的選項。  
  
2.  加密亦可用於使用 TDE 加密的資料庫。  
  
3.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]建立的備份支援加密，可提供離站備份額外的安全性。  
  
4.  此功能支援最高 AES 256 位元的多個加密演算法。 如此可提供您選項，選取符合您需求的演算法。  
  
5.  您可以將加密金鑰與延伸金鑰管理 (EKM) 提供者整合。  
  
  
##  <a name="Prerequisites"></a> 必要條件  
 下列為加密備份的必要條件：  
  
1.  **建立 master 資料庫的資料庫主要金鑰：** 資料庫主要金鑰是一個用來保護資料庫中憑證之私密金鑰和非對稱金鑰的對稱金鑰。 如需詳細資訊，請參閱 [SQL Server 和資料庫加密金鑰 &#40;Database Engine&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)。  
  
2.  建立用來備份加密的憑證或非對稱金鑰。 如需建立憑證的詳細資訊，請參閱 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)。 如需建立非對稱金鑰的詳細資訊，請參閱 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)。  
  
    > [!IMPORTANT]  
    >  僅支援位於延伸金鑰管理 (EKM) 的非對稱金鑰。  
  
##  <a name="Restrictions"></a> 限制  
 下列為適用於加密選項的限制：  
  
-   若您使用非對稱金鑰加密備份資料，則僅支援位於 EKM 提供者的非對稱金鑰。  
  
-   SQL Server Express 和 SQL Server Web 不支援備份期間加密。 但是可支援從加密的備份還原到 SQL Server Express 或 SQL Server Web 的執行個體。  
  
-   舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法讀取加密的備份。  
  
-   加密備份不支援附加至現有備份組的選項。  
  
  
##  <a name="Permissions"></a> 權限  
 **加密備份或從加密的備份還原：**  
  
 用來加密資料庫備份的憑證或非對稱金鑰上的**VIEW DEFINITION** 權限。  
  
> [!NOTE]  
>  備份或還原 TDE 所保護的資料庫並不需要存取 TDE 憑證。  
  
##  <a name="Methods"></a> 備份加密方式  
 下列章節將簡單介紹在備份期間加密資料的步驟。 如需有關使用 Transact-SQL 加密備份之不同步驟的完整逐步解說，請參閱 [建立加密的備份](../../relational-databases/backup-restore/create-an-encrypted-backup.md)。  
  
### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio  
 在下列任一對話方塊中建立資料庫備份時，您可以加密備份：  
  
1.  [備份資料庫 &#40;備份選項頁面&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)：您可以在 [備份選項]  頁面選取 [加密]  ，並指定用於加密的加密演算法以及憑證或非對稱金鑰。  
  
2.  [使用維護計畫精靈](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure)：當您選取備份工作時，您可以在 [Define Backup ()Task (定義備份 () 工作)]  頁面的 [選項]  索引標籤上，選取 [備份加密]  ，並指定用於加密的加密演算法以及憑證或金鑰。  
  
### <a name="using-transact-sql"></a>使用 Transact SQL  
 下列為加密備份檔案的範例 Transact-SQL 陳述式：  
  
```sql  
BACKUP DATABASE [MYTestDB]  
TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
  
```  
  
 如需完整 Transact-SQL 陳述式的語法，請參閱 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)。  
  
### <a name="using-powershell"></a>使用 PowerShell  
 此範例會建立加密選項，然後將它當作 **Backup-SqlDatabase** Cmdlet 的參數值使用，以建立加密備份。  
  
```  
C:\PS>$encryptionOption = New-SqlBackupEncryptionOption -Algorithm Aes256 -EncryptorType ServerCertificate -EncryptorName "BackupCert"  
```  
  
```  
C:\PS>Backup-SqlDatabase -ServerInstance . -Database "MyTestDB" -BackupFile "MyTestDB.bak" -CompressionOption On -EncryptionOption $encryptionOption  
```  
  
##  <a name="RecommendedPractices"></a> 建議的做法  
 建立加密憑證和金鑰的備份至您安裝執行個體的本機電腦以外的位置。 若考量到損毀復原狀況，請考慮將憑證或金鑰的備份儲存至異地位置。 若沒有用來加密此備份的憑證，您就無法還原加密的備份。  
  
 若要還原加密的備份，在相符的指模取得備份時所使用的原始憑證，應可用於您要進行還原的執行個體上。 因此，憑證不應該更新到期日或做其他任何的變更。 更新會導致觸發指模變更的憑證更新，而使憑證對備份檔案無效。 執行還原的帳戶應擁有備份時用以加密之憑證或非對稱金鑰的 VIEW DEFINITION 權限。  
  
 可用性群組資料庫備份通常會在慣用的備份複本上執行。  如果您不是在當初取得備份的複本上還原備份，請確定用於備份的原始憑證可在您要還原的目標複本上使用。  
  
 若資料庫已啟用 TDE，在加密資料庫和備份時請分別選擇不同的憑證或非對稱金鑰，以提升安全性。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
|主題/工作|Description|  
|-----------------|-----------------|  
|[建立加密的備份](../../relational-databases/backup-restore/create-an-encrypted-backup.md)|描述建立加密備份所需的基本步驟|  
|[使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)|提供在 Azure 金鑰保存庫中建立受金鑰保護的加密備份範例。|  
  
## <a name="see-also"></a>另請參閱  
 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
  
