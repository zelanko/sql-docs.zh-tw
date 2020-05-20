---
title: 將受 TDE 保護的資料庫移至另一個 SQL Server
description: 說明如何使用 SQL Server Management Studio (SSMS) 或 Transact-SQL (T-SQL)，透過透明資料加密 (TDE) 來保護資料庫，然後將資料庫移到另一個 SQL Server 執行個體。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption, moving
- TDE, moving a database
ms.assetid: fb420903-df54-4016-bab6-49e6dfbdedc7
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 21918147a6efdc750ecb56eb44c457fea9d962ac
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "75558506"
---
# <a name="move-a-tde-protected-database-to-another-sql-server"></a>將 TDE 保護的資料庫移至另一個 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../../includes/tsql-md.md)]，透過透明資料加密 (TDE) 保護資料庫，然後將資料庫移到另一個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。 TDE 會執行資料和記錄檔的即時 I/O 加密和解密。 加密會使用資料庫加密金鑰 (DEK)，此金鑰會儲存在資料庫開機記錄中，以在復原期間提供可用性。 DEK 是對稱金鑰，而其維護安全的方式是使用儲存於伺服器之 **master** 資料庫內的憑證或是受到 EKM 模組所保護的非對稱金鑰。   
   
##  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   移動 TDE 保護的資料庫時，您也必須移動用來開啟 DEK 的憑證或非對稱金鑰。 憑證或非對稱金鑰必須安裝在目的地伺服器的 **master** 資料庫中， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 才能存取資料庫檔案。 如需詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)。  
  
-   您必須同時保留憑證檔案和私密金鑰檔案的副本，才能復原憑證。 私密金鑰的密碼不必與資料庫主要金鑰密碼相同。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設會將此處建立的檔案儲存在 **C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA** 。 您的檔案名稱和位置可能會不同。  
  
##  <a name="permissions"></a><a name="Permissions"></a> 權限  
  
-   需要 **master** 資料庫的 **CONTROL DATABASE** 權限，才能建立資料庫主要金鑰。  
  
-   需要 **master** 資料庫的 **CREATE CERTIFICATE** 權限，才能建立保護 DEK 的憑證。  
  
-   需要加密資料庫的 **CONTROL DATABASE** 權限，以及用於加密資料庫加密金鑰之憑證或非對稱金鑰的 **VIEW DEFINITION** 權限。  
  
##  <a name="to-create-a-database-protected-by-transparent-data-encryption"></a><a name="SSMSProcedure"></a> 建立透明資料加密所保護的資料庫  

下列程序示範您必須使用 SQL Server Management Studio 以及 Transact-SQL 建立 TDE 所保護的資料庫。
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSCreate"></a> 使用 SQL Server Management Studio  
  
1.  在 **master** 資料庫中，建立資料庫主要密碼和憑證。 如需詳細資訊，請參閱下面的 **使用 Transact-SQL** 。  
  
2.  在 **master** 資料庫中，建立伺服器憑證的備份。 如需詳細資訊，請參閱下面的 **使用 Transact-SQL** 。  
  
3.  在 [物件總管] 中，以滑鼠右鍵按一下 **[資料庫]** 資料夾，並選取 **[新增資料庫]** 。  
  
4.  在 **[新增資料庫]** 對話方塊的 **[資料庫名稱]** 方塊中，輸入新資料庫的名稱。  
  
5.  在 **[擁有者]** 方塊中，輸入新資料庫擁有者的名稱。 或者，按一下省略符號 **(...)** ，開啟 [選取資料庫擁有者]  對話方塊。 如需有關建立新資料庫的詳細資訊，請參閱＜ [Create a Database](../../../relational-databases/databases/create-a-database.md)＞。  
  
6.  在 [物件總管] 中，按一下加號展開 **[資料庫]** 資料夾。  
  
7.  以滑鼠右鍵按一下建立的資料庫，指向 **[工作]** ，然後選取 **[管理資料庫加密]** 。  
  
     **[管理資料庫加密]** 對話方塊有下列選項。  
  
     **加密演算法**  
     顯示或設定要用於資料庫加密的演算法。 **AES128** 是預設演算法。 這個欄位不能空白。 如需有關加密演算法的詳細資訊，請參閱＜ [Choose an Encryption Algorithm](../../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)＞。  
  
     **使用伺服器憑證**  
     設定由憑證維護安全的加密。 從清單中選取一項。 如果您沒有伺服器憑證的 **VIEW DEFINITION** 權限，此清單就會是空的。 如果選取了憑證方法的加密，這個值就不能是空的。 如需有關憑證的詳細資訊，請參閱＜ [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)＞。  
  
     **使用伺服器非對稱金鑰**  
     設定由非對稱金鑰維護安全的加密。 只會顯示可用的非對稱金鑰。 受到 EKM 模組所保護的非對稱金鑰可以使用 TDE 加密資料庫。  
  
     **將資料庫加密設為開啟**  
     將資料庫改變為開啟 (核取) 或關閉 (不核取) TDE。  
  
8.  完成後，請按一下 **[確定]** 。  

###  <a name="using-transact-sql"></a><a name="TsqlCreate"></a> 使用 Transact-SQL  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql  
    -- Create a database master key and a certificate in the master database.  
    USE master ;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    CREATE CERTIFICATE TestSQLServerCert   
    WITH SUBJECT = 'Certificate to protect TDE key'  
    GO  
    -- Create a backup of the server certificate in the master database.  
    -- The following code stores the backup of the certificate and the private key file in the default data location for this instance of SQL Server   
    -- (C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA).  
  
    BACKUP CERTIFICATE TestSQLServerCert   
    TO FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Create a database to be protected by TDE.  
    CREATE DATABASE CustRecords ;  
    GO  
    -- Switch to the new database.  
    -- Create a database encryption key, that is protected by the server certificate in the master database.   
    -- Alter the new database to encrypt the database using TDE.  
    USE CustRecords;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM = AES_128  
    ENCRYPTION BY SERVER CERTIFICATE TestSQLServerCert;  
    GO  
    ALTER DATABASE CustRecords  
    SET ENCRYPTION ON;  
    GO  
    ```  
  
 如需詳細資訊，請參閱  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-certificate-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
-   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
##  <a name="to-move-a-database-protected-by-transparent-data-encryption"></a><a name="TsqlProcedure"></a> 移動透明資料加密所保護的資料庫 

下列程序示範您必須使用 SQL Server Management Studio 以及 Transact-SQL 移動 TDE 所保護的資料庫。
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSMove"></a> 使用 SQL Server Management Studio  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下上方加密的資料庫，指向 [工作]  ，然後選取 [卸離...]  。  
  
     **[卸離資料庫]** 對話方塊有下列選項。  
  
     **要卸離的資料庫**  
     列出要卸離的資料庫。  
  
     **Database Name**  
     顯示要卸離的資料庫名稱。  
  
     **卸除連接**  
     中斷到指定資料庫的連接。  
  
    > [!NOTE]  
    >  您無法卸離具有使用中連接的資料庫。  
  
     **更新統計資料**  
     依預設，卸離作業會在卸離資料庫時保留任何過時的最佳化統計資料。若要更新現有的最佳化統計資料，請按一下此核取方塊。  
  
     **保留全文檢索目錄**  
     依預設，卸離作業會保留與該資料庫關聯的所有全文檢索目錄。 若要移除這些全文檢索目錄，請清除 **[保留全文檢索目錄]** 核取方塊。 只有當您從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]升級資料庫時，才會出現這個選項。  
  
     **狀態**  
     顯示下列狀態其中之一： **就緒** 或 **未就緒**。  
  
     **訊息**  
     **[訊息]** 資料行可以顯示有關資料庫的資訊，如下所示：  
  
    -   當資料庫涉及複寫時， **[狀態]** 為 **[尚未備妥]** 且 **[訊息]** 資料行會顯示 **[資料庫已複寫]** 。  
  
    -   當資料庫有一或多個使用中的連線時，[狀態]  為 [未就緒]  且 [訊息]  資料行顯示 [ _\<number\_of\_active\_connections\>_ 個使用中的連線]  - 例如：[1 個使用中的連線]  。 您必須選取 **[卸除連接]** 中斷任何使用中的連接之後，才能卸離資料庫。  
  
     若要取得有關訊息的詳細資訊，請按一下超連結文字，以開啟活動監視器。  
  
2.  按一下 [確定]  。  
  
3.  使用 [Windows 檔案總管]，將資料庫檔案從來源伺服器移動或複製到目的地伺服器上相同的位置。  
  
4.  使用 [Windows 檔案總管]，將伺服器憑證和私密金鑰檔案的備份從來源伺服器移動或複製到目的地伺服器上相同的位置。  
  
5.  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的目的地執行個體上，建立資料庫主要金鑰。 如需詳細資訊，請參閱下面的 **使用 Transact-SQL** 。  
  
6.  使用原始伺服器憑證備份檔案重新建立伺服器憑證。 如需詳細資訊，請參閱下面的 **使用 Transact-SQL** 。  
  
7.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 的 [物件總管] 中，以滑鼠右鍵按一下 [資料庫]  資料夾，然後選取 [附加...]  。  
  
8.  在 **[附加資料庫]** 對話方塊中，按一下 **[要附加的資料庫]** 底下的 **[加入]** 。  
  
9. 在 [尋找資料庫檔案 -_server\_name_] 對話方塊中，選取要附加至新伺服器的資料庫檔案，然後按一下 [確定]。  
  
     **[附加資料庫]** 對話方塊有下列選項。  
  
     **[要附加的資料庫]**  
     顯示有關所選資料庫的資訊。  
  
     \<無資料行標頭>  
     顯示指出附加作業之狀態的圖示。 可能的圖示將在以下的 **[狀態]** 描述中加以描述。  
  
     **MDF 檔案位置**  
     顯示選取之 MDF 檔的路徑和檔案名稱。  
  
     **Database Name**  
     顯示資料庫的名稱。  
  
     **附加為**  
     選擇性地針對要附加的資料庫指定不同的名稱。  
  
     **擁有者**  
     提供包含可能的資料庫擁有者的下拉式清單，且您可以選擇性地從中選取不同的擁有者。  
  
     **狀態**  
     根據下表顯示資料庫的狀態。  
  
    |圖示|狀態文字|描述|  
    |----------|-----------------|-----------------|  
    |(無圖示)|(沒有文字)|附加作業尚未啟動或是針對此物件進行暫止。 當對話方塊開啟時，這是預設的動作。|  
    |綠色、指向右方的三角形|進行中|附加作業已啟動，但尚未完成。|  
    |綠色的核取記號|Success|已順利附加物件。|  
    |包含白色十字的紅色圓圈|錯誤|附加作業發生錯誤，且未順利完成。|  
    |包含兩個黑色的象限 (在左方和右方) 以及兩個白色的象限 (在上方和下方)|已停止|附加作業未順利完成，因為使用者已停止作業。|  
    |包含指向逆時針方向之彎曲箭頭的圓圈|已回復|附加作業已順利完成，但是因為在附加其他物件的期間發生了錯誤，所以已將其回復。|  
  
     **訊息**  
     顯示空白訊息或「找不到檔案」超連結。  
  
     **加入**  
     尋找需要的主要資料庫檔案。 使用者選取 .mdf 檔案之後，適用的資訊會自動填入 **[要附加的資料庫]** 方格的對應欄位中。  
  
     **移除**  
     從 **[要附加的資料庫]** 方格中移除選取的檔案。  
  
     **"** _<database_name>_ **" database details**  
     顯示要附加之檔案的名稱。 若要確認或變更檔案的路徑名稱，請按一下 [瀏覽]  按鈕 ( **...** )。  
  
    > [!NOTE]  
    >  如果檔案不存在， **[訊息]** 資料行就會顯示「找不到」。 如果找不到記錄檔，它就存在於其他目錄中，或是已遭刪除。 您必須更新 **[資料庫詳細資料]** 方格中的檔案路徑，以指向正確的位置，或是從方格中移除該記錄檔。 如果找不到 .ndf 資料檔，您就必須更新該檔案在方格中的路徑，以指向正確的位置。  
  
     **原始檔案名稱**  
     顯示屬於資料庫之附加檔案的名稱。  
  
     **檔案類型**  
     指出檔案的類型，即 **資料** 或 **記錄**。  
  
     **目前的檔案路徑**  
     顯示選取之資料庫檔案的路徑。 路徑可以用手動的方式編輯。  
  
     **訊息**  
     顯示空白訊息或 **「找不到檔案」** 超連結。  
  
###  <a name="using-transact-sql"></a><a name="TsqlMove"></a> 使用 Transact-SQL  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql  
    -- Detach the TDE protected database from the source server.   
    USE master ;  
    GO  
    EXEC master.dbo.sp_detach_db @dbname = N'CustRecords';  
    GO  
    -- Move or copy the database files from the source server to the same location on the destination server.   
    -- Move or copy the backup of the server certificate and the private key file from the source server to the same location on the destination server.   
    -- Create a database master key on the destination instance of SQL Server.   
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    -- Recreate the server certificate by using the original server certificate backup file.   
    -- The password must be the same as the password that was used when the backup was created.  
  
    CREATE CERTIFICATE TestSQLServerCert   
    FROM FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        DECRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Attach the database that is being moved.   
    -- The path of the database files must be the location where you have stored the database files.  
    CREATE DATABASE [CustRecords] ON   
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\CustRecords.mdf' ),  
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\CustRecords_log.LDF' )  
    FOR ATTACH ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱  
  
-   [sp_detach_db &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料庫卸離和附加 &#40;SQL Server&#41;](../../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Azure SQL Database 的透明資料加密](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)  
  
  
