---
title: 備份、還原和移動 SSIS 目錄 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bf806aef-8556-48ab-aed5-e95de9a2204e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f9de552ddd54168f516f42d9988302561616fd65
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439365"
---
# <a name="backup-restore-and-move-the-ssis-catalog"></a>備份、 還原和移動的 SSIS 目錄
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 包括 SSISDB 資料庫。 您可以查詢 SSISDB 資料庫中的檢視，以檢查物件、設定以及儲存在 [SSISDB]**** 目錄中的作業資料。 本主題提供備份與還原資料庫的指示。  
  
 **SSISDB** 目錄會儲存您已經部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器的封裝。 如需目錄的詳細資訊，請參閱 [SSIS 目錄](catalog/ssis-catalog.md)。  
  
##  <a name="to-back-up-the-ssis-database"></a><a name="backup"></a>若要備份 SSIS 資料庫  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 並連接至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體。  
  
2.  使用 BACKUP MASTER KEY Transact-SQL 陳述式，備份 SSISDB 資料庫的主要金鑰。 此金鑰儲存在您指定的檔案。 使用密碼來加密檔案中的主要金鑰密碼。  
  
     如需陳述式的詳細資訊，請參閱 [BACKUP MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-master-key-transact-sql)。  
  
     在下列範例中，主要金鑰是匯出至 `c:\temp directory\RCTestInstKey` 檔案。 `LS2Setup!` 密碼是用來加密主要金鑰。  
  
    ```  
    backup master key to file = 'c:\temp\RCTestInstKey'  
           encryption by password = 'LS2Setup!'  
  
    ```  
  
3.  使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [備份資料庫]**** 對話方塊備份 SSISDB 資料庫。 如需詳細資訊，請參閱 [如何：備份資料庫 (SQL Server Management Studio)](https://go.microsoft.com/fwlink/?LinkId=231812)。  
  
4.  執行下列操作，產生 ##MS_SSISServerCleanupJobLogin## 的 CREATE LOGIN 指令碼。 如需詳細資訊，請參閱 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)。  
  
    1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的物件總管中，展開 [安全性]**** 節點，然後展開 [登入]**** 節點。  
  
    2.  以滑鼠右鍵按一下 [##MS_SSISServerCleanupJobLogin##]****，然後按一下 [編寫登入的指令碼為]**** > [CREATE 至]**** > [新增查詢編輯器視窗]****。  
  
5.  如果您要將 SSISDB 資料庫還原至從未建立過 SSISDB 目錄的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，請執行下列動作，藉以產生 sp_ssis_startup 的 CREATE PROCEDURE 指令碼。 如需詳細資訊，請參閱 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)。  
  
    1.  在物件總管中，展開 [**資料庫**] 節點，然後展開 [**系統資料庫**] [主要程式設計] [  >  **master**  >  **Programmability**  >  **預存程式**] 節點。  
  
    2.  以滑鼠右鍵按一下 [dbo.sp_ssis_startup]****，然後按一下 [編寫預存程序的指令碼為]**** > [CREATE 至]**** > [新增查詢編輯器視窗]****。  
  
6.  確認已啟動 SQL Server Agent  
  
7.  如果您要將 SSISDB 資料庫還原至從未建立過 SSISDB 目錄的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，請執行下列動作，藉以產生 SSIS 伺服器維護作業的指令碼。 當您建立 SSISDB 目錄時，系統就會自動在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 中建立指令碼。 此作業有助於清除保留週期外部的清除作業，並移除舊版專案。  
  
    1.  在物件總管中，展開 [SQL Server Agent]**** 節點，然後展開 [作業]**** 節點。  
  
    2.  以滑鼠右鍵按一下 [SSIS 伺服器維護作業]，然後按一下 [**腳本作業] 做為**[  >  **建立至**  >  **新查詢編輯器視窗]**。  
  
### <a name="to-restore-the-ssis-database"></a>若要還原 SSIS 資料庫  
  
1.  如果您要將 SSISDB 資料庫還原至從未建立過 SSISDB 目錄的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，請執行 sp_configure 預存程序，藉以啟用 Common Language Runtime (CLR)。 如需詳細資訊，請參閱 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 和 [CLR 已啟用選項](https://go.microsoft.com/fwlink/?LinkId=231855)。  
  
    ```  
    use master   
           sp_configure 'clr enabled', 1  
           reconfigure  
  
    ```  
  
2.  如果您要將 SSISDB 資料庫還原至從未建立過 SSISDB 目錄的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，請建立非對稱金鑰並根據非對稱金鑰建立登入，並且將 UNSAFE 權限授與登入。  
  
    ```  
    Create Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey  
           FROM Executable File = 'C:\Program Files\Microsoft SQL Server\110\DTS\Binn\Microsoft.SqlServer.IntegrationServices.Server.dll'  
  
    ```  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] CLR 預存程序需要授與 UNSAFE 權限給登入，因為登入需要對於限制資源的額外存取，例如 Microsoft Win32 API。 如需 UNSAFE 程式碼權限的詳細資訊，請參閱 [建立組件](../relational-databases/clr-integration/assemblies/creating-an-assembly.md)。  
  
    ```  
    Create Login MS_SQLEnableSystemAssemblyLoadingUser  
           FROM Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey   
  
           Grant unsafe Assembly to MS_SQLEnableSystemAssemblyLoadingUser  
  
    ```  
  
3.  使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [還原資料庫]**** 對話方塊，從備份還原 SSISDB 資料庫。 如需詳細資訊，請參閱下列主題。  
  
    -   [還原資料庫 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)  
  
    -   [還原資料庫 &#40;檔案頁面&#41;](../relational-databases/backup-restore/restore-database-files-page.md)  
  
    -   [還原資料庫 &#40;選項頁面&#41;](../relational-databases/backup-restore/restore-database-options-page.md)  
  
4.  針對 ##MS_SSISServerCleanupJobLogin##、sp_ssis_startup 和 SSIS 伺服器維護作業，執行您在 [備份 SSIS 資料庫](#backup) 中所建立的指令碼。 確認已啟動 SQL Server Agent。  
  
5.  執行下列陳述式以設定 sp_ssis_startup 程序進行自動執行。 如需詳細資訊，請參閱 [sp_procoption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql)。  
  
    ```  
    EXEC sp_procoption N'sp_ssis_startup','startup','on'  
    ```  
  
6.  使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [登入屬性]**** 對話方塊，將 SSISDB 使用者 ##MS_SSISServerCleanupJobUser## (SSISDB 資料庫) 對應至 ##MS_SSISServerCleanupJobLogin##。  
  
7.  使用下列其中一種方法來還原主要金鑰。 如需加密的詳細資訊，請參閱 [加密階層](../relational-databases/security/encryption/encryption-hierarchy.md)。  
  
    -   **方法1**  
  
         如果您已經備份資料庫主要金鑰，而且您有用來加密主要金鑰的密碼，請使用此方法。  
  
        ```  
               Restore master key from file = 'c:\temp\RCTestInstKey'  
               Decryption by password = 'LS2Setup!' -- 'Password used to encrypt the master key during SSISDB backup'  
               Encryption by password = 'LS3Setup!' -- 'New Password'  
               Force  
  
        ```  
  
        > [!NOTE]  
        >  確認 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務帳戶擁有讀取備份金鑰檔案的權限。  
  
        > [!NOTE]  
        >  如果服務主要金鑰尚未加密資料庫主要金鑰，您將會看到下列警告訊息顯示在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中。 忽略警告訊息。  
        >   
        >  **無法解密目前的主要金鑰。因為指定了 FORCE 選項，所以已忽略錯誤。**  
        >   
        >  FORCE 引數會指定即使未開放目前的資料庫主要金鑰，也應該繼續還原程序。 若是 SSISDB 目錄，因為尚未在您要還原資料庫所在的執行個體上開放資料庫主要金鑰，因此您將會看到此訊息。  
  
    -   **方法2**  
  
         如果您有建立 SSISDB 所使用的原始密碼，請使用此方法。  
  
        ```  
        open master key decryption by password = 'LS1Setup!' --'Password used when creating SSISDB'  
               Alter Master Key Add encryption by Service Master Key  
        ```  
  
8.  執行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] catalog.check_schema_version [，以判斷 SSISDB 目錄結構描述與](/sql/integration-services/system-stored-procedures/catalog-check-schema-version)二進位檔 (ISServerExec 和 SQLCLR 組件) 是否相容。  
  
9. 若要確認已成功還原 SSISDB 資料庫，請針對 SSISDB 目錄執行作業，例如執行已經部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器的封裝。 如需詳細資訊，請參閱 [使用 SQL Server Management Studio 在 SSIS 伺服器上執行封裝](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)。  
  
### <a name="to-move-the-ssis-database"></a>若要移動 SSIS 資料庫  
  
-   遵循移動使用者資料庫的指示進行。 如需詳細資訊，請參閱 [移動使用者資料庫](../relational-databases/databases/move-user-databases.md)。  
  
     確定您有備份 SSISDB 資料庫的主要金鑰並保護備份檔案。 如需詳細資訊，請參閱 [備份 SSIS 資料庫](#backup)。  
  
     確定 Integration Services (SSIS) 相關物件建立在尚未建立 SSISDB 目錄的新 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體中。  
  
  
