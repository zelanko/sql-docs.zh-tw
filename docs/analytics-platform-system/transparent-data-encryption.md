---
title: 透明資料加密-Parallel Data Warehouse |Microsoft Docs
description: 透明資料加密 (TDE) Parallel Data Warehouse (PDW) 會執行即時 I/O 加密和解密資料和交易記錄檔和特殊的 PDW 記錄檔。 」
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f30d22725e7d0fd099cf2976af42d74d08a93b22
ms.sourcegitcommit: 2e038db99abef013673ea6b3535b5d9d1285c5ae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2018
ms.locfileid: "39400611"
---
# <a name="transparent-data-encryption"></a>透明資料加密
您可以採取幾個預防措施來維護資料庫安全，例如設計安全的系統、加密機密的資產，以及在資料庫伺服器周圍建立防火牆。 不過，所在實體媒體 （例如磁碟機或備份磁帶） 遭竊的案例中，惡意人士可以只還原或附加資料庫並瀏覽資料。 一個解決方案是加密資料庫中的敏感性資料，並使用憑證來保護用來加密資料的金鑰。 如此可防止沒有金鑰的任何人使用資料，但是這種防護類型必須事先規劃。  
  
*透明資料加密*(TDE) 會執行即時 I/O 加密和解密資料和交易記錄檔和特殊的 PDW 記錄檔。 此加密會使用資料庫加密金鑰 (DEK)，該金鑰儲存於資料庫開機記錄中，以便在復原期間可供使用。 DEK 是對稱金鑰受到使用儲存在 SQL Server PDW 的 master 資料庫中的憑證。 TDE 會保護休眠的資料，也就是資料檔和記錄檔。 它提供了與各個不同業界內建立的許多法令、規章和指導方針相符的能力， 這項功能可讓軟體開發人員使用 AES 和 3DES 加密演算法，而不需要變更現有的應用程式加密資料。  
  
> [!IMPORTANT]  
> TDE 不提供用戶端與 PDW 之間傳輸的資料的加密。 如需如何加密資料之間的用戶端和 SQL Server PDW 的詳細資訊，請參閱[佈建憑證](provision-certificate.md)。  
>   
> TDE 不會加密資料，在移動期間，或使用中。 在 SQL Server PDW 的 PDW 元件之間的內部流量不會加密。 暫時儲存在記憶體緩衝區中的資料不會加密。 若要降低此風險，控制實體存取權和 SQL Server pdw 的連接。  
  
在設定資料庫安全性之後，可以使用正確的憑證將它還原。  
  
> [!NOTE]  
> 當您建立用於 TDE 的憑證時，您應該立即備份它，以及相關聯的私密金鑰。 如果此憑證無法使用或是您必須在另一部伺服器上還原或附加資料庫，您必須同時擁有此憑證和私密金鑰的備份，否則將無法開啟資料庫。 即使資料庫上不再啟用 TDE，還是應該保留加密憑證。 就算資料庫並未加密，交易記錄的某些部分可能仍受到保護，因而有些作業截至資料庫執行完整備份為止或許都需要此憑證。 已經超過到期日的憑證仍然可用來搭配 TDE 加密和解密資料。  
  
資料庫檔案的加密會在頁面層級上執行。 加密資料庫中的頁面會在寫入磁碟前先加密，並在讀入記憶體時進行解密。 TDE 並不會讓加密之資料庫的大小增加。  
  
下圖顯示 TDE 加密金鑰階層：  
  
![顯示階層](media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>使用透明資料加密  
若要使用 TDE，請遵循下列步驟。 前三個步驟時，才進行一次，準備 SQL Server PDW 才能支援 TDE。  
  
1.  Master 資料庫中建立主要金鑰。  
  
2.  使用**sp_pdw_database_encryption**若要在 SQL Server PDW 上啟用 TDE。 這項作業會將暫存資料庫修改以確保未來的暫存資料的保護，而且如果當有任何作用中工作階段具有暫存資料表時，嘗試會失敗。 **sp_pdw_database_encryption** PDW 系統記錄檔中的使用者資料遮罩會開啟。 (如需 PDW 系統記錄檔中的使用者資料遮罩的詳細資訊，請參閱[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)。)  
  
3.  使用[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)來建立可驗證及寫入儲存憑證的備份共用的認證。 如果認證已存在的預定的存放區伺服器，您可以使用現有的認證。  
  
4.  在 master 資料庫中，建立主要金鑰所保護的憑證。  
  
5.  備份儲存體共用的憑證。  
  
6.  在使用者資料庫中，建立資料庫加密金鑰並儲存在 master 資料庫中的憑證來保護它。  
  
7.  使用`ALTER DATABASE`來加密資料庫使用 TDE 的陳述式。  
  
下列範例說明加密`AdventureWorksPDW2012`資料庫使用憑證，名為`MyServerCert`建立的 SQL Server PDW。  
  
**第一個： 上啟用 TDE 的 SQL Server PDW。** 此動作時，才需要一次。  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
-- Add a credential that can write to the share  
-- A credential created for a backup can be used if you wish  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
**第二個： 建立和備份 master 資料庫中的憑證。** 此動作，才需要一次。 您可以有個別的憑證，每個資料庫 （建議），或您可以保護多個資料庫使用一個憑證。  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';  
GO  
  
-- Back up the certificate with private key  
BACKUP CERTIFICATE MyServerCert   
    TO FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'  
    WITH PRIVATE KEY   
    (   
        FILE = '\\SECURE_SERVER\cert\MyServerCert.key',  
        ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>'   
    )   
GO  
```  
  
**最後一個： 建立 DEK，並使用 ALTER DATABASE 來加密使用者資料庫。** 此動作會重複受到 TDE 的每個資料庫。  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_128  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
  
ALTER DATABASE AdventureWorksPDW2012 SET ENCRYPTION ON;  
GO  
```  
  
SQL server 加密和解密作業排定在背景執行緒。 您可以檢視在本文稍後出現的清單中使用的目錄檢視和動態管理檢視這些作業的狀態。  
  
> [!CAUTION]  
> 啟用了 TDE 的資料庫備份檔案也會使用資料庫加密金鑰來加密。 因此，當您要還原這些備份時，保護資料庫加密金鑰的憑證必須可以使用。 這表示，除了備份資料庫以外，您也必須確定可維護伺服器憑證的備份，以免資料遺失。 如果此憑證無法再使用，就會造成資料遺失。  
  
## <a name="commands-and-functions"></a>命令與函數  
TDE 憑證必須由資料庫主要金鑰來加密，才能由下列陳述式所接受。  
  
下表提供 TDE 命令和函數的連結與說明。  
  
|命令或函數|目的|  
|-----------------------|-----------|  
|[建立資料庫加密金鑰](../t-sql/statements/create-database-encryption-key-transact-sql.md)|建立用於加密資料庫的金鑰|  
|[改變資料庫加密金鑰](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|變更用於加密資料庫的金鑰|  
|[卸除資料庫加密金鑰](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|移除用於加密資料庫的金鑰。|  
|[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)|說明用來啟用 TDE 的 **ALTER DATABASE** 選項。|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>目錄檢視和動態管理檢視  
下表顯示 TDE 目錄檢視和動態管理檢視。  
  
|目錄檢視或動態管理檢視|目的|  
|-------------------------------------------|-----------|  
|[sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|顯示資料庫資訊的目錄檢視。|  
|[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|顯示資料庫中之憑證的目錄檢視。|  
|[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|提供每個節點，資料庫和資料庫的加密狀態中使用的加密金鑰的相關資訊的動態管理檢視。|  
  
## <a name="permissions"></a>Permissions  
TDE 的每一項功能和命令都有個別的權限需求，如同之前所示的表格所述。  
  
檢視與 TDE 有關的中繼資料需要`CONTROL SERVER`權限。  
  
## <a name="considerations"></a>考量  
當資料庫加密作業的重新加密掃描正在進行時，對資料庫的維護作業將會停用。  
  
您可以找到資料庫加密使用的狀態**sys.dm_pdw_nodes_database_encryption_keys**動態管理檢視。 如需詳細資訊，請參閱 <<c0>  *目錄檢視和動態管理檢視*稍早在本文中的區段。  
  
### <a name="restrictions"></a>限制  
不允許下列作業期間`CREATE DATABASE ENCRYPTION KEY`， `ALTER DATABASE ENCRYPTION KEY`， `DROP DATABASE ENCRYPTION KEY`，或`ALTER DATABASE...SET ENCRYPTION`陳述式。  
  
-   卸除資料庫。  
  
-   使用`ALTER DATABASE`命令。  
  
-   啟動資料庫備份。  
  
-   正在啟動資料庫還原。  
  
下列的作業或條件會造成`CREATE DATABASE ENCRYPTION KEY`， `ALTER DATABASE ENCRYPTION KEY`， `DROP DATABASE ENCRYPTION KEY`，或`ALTER DATABASE...SET ENCRYPTION`陳述式。  
  
-   `ALTER DATABASE`命令正在執行中。  
  
-   正在執行任何資料備份。  
  
在建立資料庫檔案時，啟用 TDE 時無法使用立即檔案初始化功能。  
  
### <a name="areas-not-protected-by-tde"></a>未受 tde 保護的區域  
TDE 不會保護外部資料表。  
  
TDE 不會保護診斷工作階段。 使用者應該要特別小心不適用於與診斷工作階段時使用中的敏感性參數的查詢。 當不再需要應該卸除揭露敏感性資訊的診斷工作階段。  
  
放在 SQL Server PDW 記憶體中時，會解密 TDE 所保護的資料。 應用裝置上發生特定問題時，會建立記憶體傾印。 傾印檔案代表內容的記憶體問題出現的時間，並可包含機密資料以加密形式。 它們會與其他人共用之前，應該檢閱記憶體傾印的內容。  
  
Master 資料庫不受 TDE。 Master 資料庫不包含使用者資料，但它並未包含資訊，例如登入名稱。  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>透明資料加密和交易記錄  
啟用要使用 TDE 的資料庫會清空虛擬交易記錄，以強制執行下一個虛擬交易記錄檔的其餘部分的效果。 這樣可確保在設定資料庫進行加密之後，交易記錄中不會留下任何純文字。 您可以在 PDW 中的每個節點上找到的記錄檔加密狀態，藉由檢視`encryption_state`中的資料行`sys.dm_pdw_nodes_database_encryption_keys`檢視，如此範例所示：  
  
```sql  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
           ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
在資料庫加密金鑰變更之前寫入交易記錄的所有資料，都會使用之前的資料庫加密金鑰進行加密。  
  
### <a name="pdw-activity-logs"></a>PDW 活動記錄  
SQL Server PDW 會維護一份適用於疑難排解的記錄檔。 （請注意，這不是交易記錄檔、 SQL Server 錯誤記錄檔或 Windows 事件記錄檔）。這些 PDW 活動記錄檔可以包含完整的陳述式，以純文字，其中可以包含使用者資料。 常見的範例**插入**並**更新**陳述式。 使用者資料時，遮罩可以明確地開啟或關閉使用**sp_pdw_log_user_data_masking**。 啟用 SQL Server PDW 上的加密會自動開啟 PDW 活動記錄中的使用者資料遮罩以保護它們。 **sp_pdw_log_user_data_masking**也可用來在不使用 TDE，遮罩陳述式，但是，不建議，因為它會大幅減少 「 Microsoft 支援小組能夠分析問題。  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>透明資料加密和 tempdb 系統資料庫  
Tempdb 系統資料庫會加密啟用加密時使用[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)。 這是必要的任何資料庫才能使用 TDE。 這可能會有相同的執行個體的 SQL Server PDW 上未加密的資料庫效能影響。  
  
## <a name="key-management"></a>金鑰管理  
資料庫加密金鑰 (DEK) 受到儲存在 master 資料庫中的憑證。 這些憑證會受到主要資料庫的資料庫主要金鑰 (DMK)。 DMK 必須保護服務主要金鑰 (SMK)，才能用於 TDE。  
  
系統可以存取金鑰，而不需要人為介入 （例如提供密碼）。 如果沒有憑證，系統會將輸出說明適當的憑證可用之前，無法解密的 DEK 的錯誤。  
  
當轉換成另一個應用裝置資料庫，用來保護其 ' DEK 首先必須還原在目的地伺服器上。 然後可以如往常般還原資料庫。 如需詳細資訊，請參閱 < 標準的 SQL Server 文件，在[將 TDE 保護的資料庫移至另一個 SQL Server](http://technet.microsoft.com/library/ff773063.aspx)。  
  
應該保留用來加密 Dek 的憑證，只要有使用它們的資料庫備份。 憑證的備份必須包含憑證的私密金鑰，因為不含私密金鑰的憑證無法用於還原資料庫。 這些憑證私用金鑰備份會儲存在不同的檔案，必須提供憑證還原有密碼保護。  
  
## <a name="restoring-the-master-database"></a>還原 master 資料庫  
可以使用還原 master 資料庫**DWConfig**，做為災害復原的一部分。  
  
-   如果控制節點沒有變更，這是從中取得備份主要資料庫相同和不變應用裝置上還原 master 資料庫時，請 DMK 及所有憑證都可以讀取而不進行其他動作。  
  
-   如果主要資料庫會還原在不同的應用裝置，或在 master 資料庫的備份之後已變更控制節點，則會需要額外的步驟，以重新產生 DMK。  
  
    1.  開啟 DMK:  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  新增 SMK 的加密：  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  設備重新啟動。  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>升級和取代虛擬機器  
如果 DMK 設備執行升級或取代 VM 上，必須提供 DMK 密碼做為參數。  
  
升級動作的範例。 取代`**********`DMK 密碼。  
  
`setup.exe /Action=ProvisionUpgrade … DMKPassword='**********'  `  
  
將虛擬機器動作的範例。  
  
`setup.exe /Action=ReplaceVM … DMKPassword='**********'  `  
  
在升級期間，如果使用者資料庫已加密，而且未提供 DMK 密碼，將會失敗的升級動作。 期間取代，如果未提供正確的密碼則 DMK 存在時，則作業會略過 DMK 復原步驟。 所有其他的步驟會完成取代 VM 動作中，結尾，但此動作會報告失敗結尾，表示不需要額外的步驟。 安裝程式記錄檔中 (位於**\ProgramData\Microsoft\Microsoft SQL Server Parallel Data Warehouse\100\Logs\Setup\\< 時間戳記 > \Detail-Setup**)，將會顯示下列警告，即將結束。  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!  `
  
在 PDW 中，以手動方式執行這些陳述式並重新啟動設備之後，以復原 DMK:  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
使用中的步驟**還原 master 資料庫**段落復原資料庫，然後再重新啟動該設備。  
  
如果 DMK 之前就已存在，但不是復原動作之後，查詢資料庫時，就會引發下列錯誤訊息。  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>效能影響  
TDE 的效能影響會因為您的資料、 其儲存方式，和 SQL Server PDW 上的工作負載活動類型的類型而有所不同。 當 TDE 所保護，閱讀並再解密資料或加密以及再將資料寫入的 I/O 是 CPU 密集活動，而且同時發生其他 CPU 密集活動時，會有更大的影響。 因為 TDE 加密`tempdb`，TDE 可能會影響未加密的資料庫的效能。 若要取得精確的概略的效能，您應該測試整個系統，與您的資料和查詢活動。  
  
## <a name="related-content"></a>相關內容  
下列連結提供有關 SQL Server 管理的加密方式的一般資訊。 這些文章可協助您了解 SQL Server 加密，但這些文件沒有 SQL Server PDW 的特定資訊，他們會討論 SQL Server PDW 中所沒有的功能。  
  
-   [SQL Server 加密](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [加密階層](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [SQL Server 和資料庫加密金鑰](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>另請參閱  
[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)  
[建立主要金鑰](../t-sql/statements/create-master-key-transact-sql.md)  
[建立資料庫加密金鑰](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
