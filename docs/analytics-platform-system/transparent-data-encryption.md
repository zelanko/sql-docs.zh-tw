---
title: 透明資料加密
description: 適用于平行處理資料倉儲（PDW）的透明資料加密（TDE）會執行資料和交易記錄檔的即時 i/o 加密和解密，以及特殊的 PDW 記錄檔。」
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e75230ed175c6fbf1b0a2492265bbe12067060ca
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399937"
---
# <a name="transparent-data-encryption"></a>透明資料加密
您可以採取數個預防措施來協助保護資料庫，例如設定安全系統、加密機密資產，以及建置圍繞資料庫伺服器的防火牆。 不過，在實體媒體（例如磁片磁碟機或備份磁帶）遭竊的案例中，惡意人士可以直接還原或附加資料庫，然後流覽資料。 其中一個解決方案就是將資料庫中的敏感性資料加密，然後使用憑證來保護用來加密資料的金鑰。 如此可防止沒有金鑰的任何人使用資料，但是這種防護類型必須事先規劃。  
  
*透明資料加密*（TDE）會執行資料和交易記錄檔的即時 i/o 加密和解密，以及特殊的 PDW 記錄檔。 加密會使用資料庫加密金鑰 (DEK)，此金鑰會儲存在資料庫開機記錄中，以在復原期間提供可用性。 DEK 是使用儲存在 SQL Server PDW 之 master 資料庫中的憑證來保護的對稱金鑰。 TDE 可以保護「待用」資料，亦即資料和記錄檔。 它提供遵守各種產業中所確立的眾多法律、規定及指導方針的功能。 這項功能可讓軟體發展人員使用 AES 和3DES 加密演算法來加密資料，而不需要變更現有的應用程式。  
  
> [!IMPORTANT]  
> TDE 不會針對在用戶端與 PDW 之間進行的資料提供加密。 如需如何在用戶端與 SQL Server PDW 之間加密資料的詳細資訊，請參閱布建[憑證](provision-certificate.md)。  
>   
> TDE 不會在移動或使用中時加密資料。 SQL Server PDW 內的 PDW 元件之間的內部流量不會加密。 暫時儲存在記憶體緩衝區中的資料不會加密。 若要降低此風險，請控制實體存取和與 SQL Server PDW 的連接。  
  
在設定資料庫安全性之後，可以使用正確的憑證將它還原。  
  
> [!NOTE]  
> 當您建立 TDE 的憑證時，您應該立即將它備份，連同相關聯的私密金鑰。 如果此憑證無法使用或是您必須在另一部伺服器上還原或附加資料庫，您必須同時擁有此憑證和私密金鑰的備份，否則將無法開啟資料庫。 即使資料庫上不再啟用 TDE，還是應該保留加密憑證。 就算資料庫並未加密，交易記錄的某些部分可能仍受到保護，因而有些作業截至資料庫執行完整備份為止或許都需要此憑證。 已經超過到期日的憑證仍然可用來搭配 TDE 加密和解密資料。  
  
資料庫檔案的加密會在頁面層級執行。 加密資料庫中的頁面會在寫入磁碟前先加密，並在讀入記憶體時進行解密。 TDE 並不會讓加密之資料庫的大小增加。  
  
下圖顯示 TDE 加密的金鑰階層：  
  
![顯示階層](media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>使用透明資料加密  
若要使用 TDE，請遵循下列步驟。 前三個步驟只會在準備 SQL Server PDW 以支援 TDE 時執行一次。  
  
1.  在 master 資料庫中建立主要金鑰。  
  
2.  使用**sp_pdw_database_encryption** ，在 SQL Server PDW 上啟用 TDE。 這項作業會修改暫存資料庫，以確保未來暫存資料的保護，並在有任何使用中會話有臨時表時嘗試失敗。 **sp_pdw_database_encryption**會開啟 pdw 系統記錄中的使用者資料遮罩。 （如需有關 PDW 系統記錄中使用者資料遮罩的詳細資訊，請參閱[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)）。  
  
3.  使用[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)建立認證，此認證可驗證及寫入將儲存憑證備份的共用。 如果預定的存放區伺服器已有認證，您可以使用現有的認證。  
  
4.  在 master 資料庫中，建立受主要金鑰保護的憑證。  
  
5.  將憑證備份至儲存體共用。  
  
6.  在使用者資料庫中，建立資料庫加密金鑰，並使用儲存在 master 資料庫中的憑證來保護它。  
  
7.  使用`ALTER DATABASE`語句，使用 TDE 來加密資料庫。  
  
下列範例說明如何使用名`AdventureWorksPDW2012`為`MyServerCert`的憑證（在 SQL Server PDW 中建立）來加密資料庫。  
  
**第一：在 SQL Server PDW 上啟用 TDE。** 此動作只需要一次。  
  
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
  
**第二個：在 master 資料庫中建立並備份憑證。** 此動作只需要一次。 您可以為每個資料庫擁有個別的憑證（建議選項），也可以使用一個憑證來保護多個資料庫。  
  
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
  
**最後：建立 DEK，並使用 ALTER DATABASE 來加密使用者資料庫。** 此動作會針對 TDE 所保護的每個資料庫重複執行。  
  
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
  
加密和解密作業會在背景執行緒上 SQL Server 進行排程。 您可以使用本文稍後出現的清單中的目錄檢視和動態管理檢視，來查看這些作業的狀態。  
  
> [!CAUTION]  
> 啟用了 TDE 的資料庫備份檔案也會使用資料庫加密金鑰來加密。 因此，當您要還原這些備份時，保護資料庫加密金鑰的憑證必須可以使用。 這表示，除了備份資料庫以外，您也必須確定可維護伺服器憑證的備份，以免資料遺失。 如果此憑證無法再使用，就會造成資料遺失。  
  
## <a name="commands-and-functions"></a>命令與函數  
TDE 憑證必須由資料庫主要金鑰來加密，才能由下列陳述式所接受。  
  
下表提供 TDE 命令和函數的連結與說明。  
  
|命令或函數|目的|  
|-----------------------|-----------|  
|[建立資料庫加密金鑰](../t-sql/statements/create-database-encryption-key-transact-sql.md)|建立用於加密資料庫的金鑰|  
|[ALTER DATABASE 加密金鑰](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|變更用於加密資料庫的金鑰|  
|[卸載資料庫加密金鑰](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|移除用於加密資料庫的金鑰。|  
|[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)|說明用來啟用 TDE 的 **ALTER DATABASE** 選項。|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>目錄檢視和動態管理檢視  
下表顯示 TDE 目錄檢視和動態管理檢視。  
  
|目錄檢視或動態管理檢視|目的|  
|-------------------------------------------|-----------|  
|[sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|顯示資料庫資訊的目錄檢視。|  
|[sys. 憑證](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|顯示資料庫中之憑證的目錄檢視。|  
|[sys. dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|動態管理檢視，可提供每個節點的資訊、資料庫中使用的加密金鑰，以及資料庫的加密狀態。|  
  
## <a name="permissions"></a>權限  
TDE 的每一項功能和命令都有個別的權限需求，如同之前所示的表格所述。  
  
若要查看與 TDE 相關的元`CONTROL SERVER`資料，則需要許可權。  
  
## <a name="considerations"></a>考量  
當資料庫加密作業的重新加密掃描正在進行時，對資料庫的維護作業將會停用。  
  
您可以使用**dm_pdw_nodes_database_encryption_keys**動態管理檢視來尋找資料庫加密的狀態。 如需詳細資訊，請參閱本文前面的*目錄檢視和動態管理檢視*一節。  
  
### <a name="restrictions"></a>限制  
在`CREATE DATABASE ENCRYPTION KEY`、、 `ALTER DATABASE ENCRYPTION KEY` `DROP DATABASE ENCRYPTION KEY`或`ALTER DATABASE...SET ENCRYPTION`語句期間，不允許下列作業。  
  
-   卸除資料庫。  
  
-   使用`ALTER DATABASE`命令。  
  
-   啟動資料庫備份。  
  
-   啟動資料庫還原。  
  
下列作業或條件會`CREATE DATABASE ENCRYPTION KEY`導致、 `ALTER DATABASE ENCRYPTION KEY` `DROP DATABASE ENCRYPTION KEY`、或`ALTER DATABASE...SET ENCRYPTION`語句無法執行。  
  
-   正在`ALTER DATABASE`執行命令。  
  
-   正在執行任何資料備份。  
  
在建立資料庫檔案時，啟用 TDE 時無法使用立即檔案初始化功能。  
  
### <a name="areas-not-protected-by-tde"></a>未受到 TDE 保護的區域  
TDE 不會保護外部資料表。  
  
TDE 不會保護診斷會話。 當使用診斷會話時，使用者應該小心不要使用敏感性參數進行查詢。 當您不再需要機密資訊時，就應該將它們放在診斷會話中。  
  
受到 TDE 保護的資料會在放置於 SQL Server PDW 記憶體時進行解密。 設備上發生特定問題時，會建立記憶體傾印。 傾印檔案代表問題外觀時的記憶體內容，而且可能包含未加密格式的機密資料。 記憶體傾印的內容應該先經過檢查，然後再與其他人共用。  
  
Master 資料庫未受到 TDE 的保護。 雖然 master 資料庫不包含使用者資料，但它確實包含登入名稱之類的資訊。  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>透明資料加密和交易記錄  
啟用資料庫以使用 TDE 的效果，是將虛擬交易記錄的其餘部分清空，以強制下一個虛擬交易記錄。 這樣可確保在設定資料庫進行加密之後，交易記錄中不會留下任何純文字。 您可以藉由在`encryption_state` `sys.dm_pdw_nodes_database_encryption_keys`視圖中查看資料行，在每個 PDW 節點上尋找記錄檔加密的狀態，如下列範例所示：  
  
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
SQL Server PDW 會維護一組用於疑難排解的記錄。 （請注意，這不是交易記錄檔、SQL Server 的錯誤記錄檔或 Windows 事件記錄檔）。這些 PDW 活動記錄可以包含純文字的完整語句，其中有些可以包含使用者資料。 一般範例包括**INSERT**和**UPDATE**語句。 使用者資料的遮罩可以使用**sp_pdw_log_user_data_masking**明確地開啟或關閉。 在 SQL Server PDW 上啟用加密會自動開啟 PDW 活動記錄中的使用者資料遮罩，以保護它們。 **sp_pdw_log_user_data_masking**也可以在不使用 TDE 時用來遮罩語句，但不建議這麼做，因為它會大幅降低 Microsoft 支援服務小組分析問題的能力。  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>透明資料加密和 tempdb 系統資料庫  
當使用[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)啟用加密時，會加密 tempdb 系統資料庫。 在任何資料庫可以使用 TDE 之前，都必須這麼做。 這可能會對相同 SQL Server PDW 實例上未加密的資料庫造成效能上的影響。  
  
## <a name="key-management"></a>金鑰管理  
資料庫加密金鑰（DEK）是由儲存在 master 資料庫中的憑證所保護。 這些憑證是由 master 資料庫的資料庫主要金鑰（DMK）所保護。 DMK 必須受到服務主要金鑰（SMK）的保護，才能用於 TDE。  
  
系統可以存取金鑰，而不需要人為介入（例如提供密碼）。 如果憑證無法使用，系統會輸出錯誤，說明 DEK 無法解密，直到有適當的憑證可用為止。  
  
將資料庫從一個應用裝置移到另一個時，用來保護其 ' DEK ' 的憑證必須先在目的地伺服器上還原。 然後，可以照常還原資料庫。 如需詳細資訊，請參閱[將 TDE 保護的資料庫移至另一個 SQL Server](https://technet.microsoft.com/library/ff773063.aspx)的標準 SQL Server 檔。  
  
只要有使用它們的資料庫備份，就應該保留用來加密 Dek 的憑證。 憑證備份必須包含憑證私密金鑰，因為如果沒有私密金鑰，憑證就無法用於資料庫還原。 這些憑證私密金鑰備份會儲存在個別的檔案中，並受到必須提供以進行憑證還原的密碼所保護。  
  
## <a name="restoring-the-master-database"></a>還原 master 資料庫  
在嚴重損壞修復過程中，您可以使用**DWConfig**來還原 master 資料庫。  
  
-   如果控制節點尚未變更，也就是說，如果在建立 master 資料庫備份的相同和未變更的應用裝置上還原 master 資料庫，DMK 和所有憑證都將可讀取，而不需執行其他動作。  
  
-   如果在不同的應用裝置上還原 master 資料庫，或在備份 master 資料庫之後變更了控制節點，則需要額外的步驟，才能重新產生 DMK。  
  
    1.  開啟 DMK：  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  新增 SMK 的加密：  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  重新開機設備。  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>升級和取代虛擬機器  
如果 DMK 存在於執行升級或取代 VM 的設備上，則必須提供 DMK 密碼做為參數。  
  
升級動作的範例。 將`**********`取代為您的 DMK 密碼。  
  
`setup.exe /Action=ProvisionUpgrade ... DMKPassword='**********'`  
  
取代虛擬機器之動作的範例。  
  
`setup.exe /Action=ReplaceVM ... DMKPassword='**********'`  
  
在升級期間，如果使用者 DB 已加密，而且未提供 DMK 密碼，升級動作將會失敗。 在 [取代] 期間，如果 DMK 存在時未提供正確的密碼，此作業將會略過 DMK 復原步驟。 所有其他步驟都將在「取代 VM」動作結束時完成，但動作會在結束時回報失敗，以指出需要額外的步驟。 在安裝記錄檔（位於**\ProgramData\Microsoft\Microsoft SQL Server Parallel Data Warehouse\100\Logs\Setup\\<時間戳記> \detail-setup**）中，會在結尾附近顯示下列警告。  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!`
  
在 PDW 中手動執行這些語句，然後重新開機設備，以便復原 DMK：  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
使用**還原 Master 資料庫**段落中的步驟來復原資料庫，然後重新開機設備。  
  
如果 DMK 之前已存在，但在動作之後未復原，將會在查詢資料庫時引發下列錯誤訊息。  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>效能影響  
TDE 的效能影響會因您擁有的資料類型、儲存方式，以及 SQL Server PDW 上的工作負載活動類型而有所不同。 受到 TDE 保護時，讀取和解密資料或加密然後寫入資料的 i/o 是需要大量 CPU 的活動，並會在同時發生其他需要大量 CPU 的活動時產生更大的影響。 由於 TDE 會`tempdb`加密，因此 TDE 可能會影響未加密之資料庫的效能。 若要取得更精確的效能概念，您應該使用您的資料和查詢活動來測試整個系統。  
  
## <a name="related-content"></a>相關內容  
下列連結包含有關 SQL Server 如何管理加密的一般資訊。 這些文章可協助您瞭解 SQL Server 加密，但這些文章沒有 SQL Server PDW 特有的資訊，而且會討論 SQL Server PDW 中不存在的功能。  
  
-   [SQL Server 加密](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [加密階層](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [SQL Server 和資料庫加密金鑰](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>另請參閱  
[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)  
[建立主要金鑰](../t-sql/statements/create-master-key-transact-sql.md)  
[建立資料庫加密金鑰](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[備份憑證](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys. 憑證](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[sys. dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
