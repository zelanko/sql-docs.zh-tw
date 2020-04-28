---
title: 透明資料加密 (TDE) | Microsoft 文件
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption
- database encryption key, about
- TDE
- database encryption key
- TDE, about
- Transparent Data Encryption, about
- encryption [SQL Server], transparent data encryption
ms.assetid: c75d0d4b-4008-4e71-9a9d-cee2a566bd3b
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 018cc6fa8b85c4a1b09ab53a6a1a94d8a7670bae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176758"
---
# <a name="transparent-data-encryption-tde"></a>透明資料加密 (TDE)
  *透明資料加密* (TDE) 會加密 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 資料檔案，一般稱之為靜止的加密資料。 您可以採取數個預防措施來協助保護資料庫，例如設定安全系統、加密機密資產，以及建置圍繞資料庫伺服器的防火牆。 不過，在實體媒體 (例如磁碟機或備份磁帶) 遭竊的案例中，惡意人士可能會直接還原或附加資料庫，然後瀏覽資料。 一個解決方案是加密資料庫中的敏感性資料，並使用憑證來保護用來加密資料的金鑰。 如此可防止沒有金鑰的任何人使用資料，但是這種防護類型必須事先規劃。

 TDE 會執行資料和記錄檔的即時 I/O 加密和解密。 加密會使用資料庫加密金鑰 (DEK)，此金鑰會儲存在資料庫開機記錄中，以在復原期間提供可用性。 DEK 是對稱金鑰，而其維護安全的方式是使用儲存於伺服器之 master 資料庫內的憑證或是受到 EKM 模組所保護的非對稱金鑰。 TDE 會保護休眠的資料，也就是資料檔和記錄檔。 它提供了與各個不同業界內建立的許多法令、規章和指導方針相符的能力， 如此可讓軟體開發人員使用 AES 和 3DES 加密演算法加密資料，而不需要變更現有的應用程式。

> [!IMPORTANT]
>  TDE 不會提供跨通訊通道的加密。 如需如何跨通訊通道加密資料的詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。
> 
>  **相關主題：**
> 
>  -   [Azure SQL Database 的透明資料加密](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md)
> -   [將 TDE 保護的資料庫移至另一個 SQL Server](move-a-tde-protected-database-to-another-sql-server.md)
> -   [使用 EKM 啟用 TDE](enable-tde-on-sql-server-using-ekm.md)

## <a name="about-tde"></a>關於 TDE
 資料庫檔案的加密會在頁面層級執行。 加密資料庫中的頁面會在寫入磁碟前先加密，並在讀入記憶體時進行解密。 TDE 並不會讓加密之資料庫的大小增加。

 **適用于的資訊[!INCLUDE[ssSDS](../../../includes/sssds-md.md)]**

 在搭配使用 TDE 與 [!INCLUDE[sqldbesa](../../../includes/sqldbesa-md.md)] V12 ([某些區域處於預覽階段](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)) 時， [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]會自動為您建立儲存在主要資料庫中的伺服器層級憑證。 若要在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 上移動 TDE 資料庫，您必須解密資料庫、移動資料庫，然後在目的地 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]上重新啟用 TDE。 如需在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]上使用 TDE 的逐步解說，請參閱 [Transparent Data Encryption with Azure SQL Database](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md)＞。

 TDE 狀態預覽即使在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 版本系列 V12 已宣佈為目前處於公開可用狀態的地理區域也適用。 在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 宣佈 TDE 從預覽版升級至 GA 前， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 的 TDE 並不適用於生產資料庫。 如需有關 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] V12 的詳細資訊，請參閱 [Azure SQL Database 的新功能](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/)。

 **適用於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的資訊**

 在設定資料庫安全性之後，可以使用正確的憑證將它還原。 如需有關憑證的詳細資訊，請參閱＜ [SQL Server Certificates and Asymmetric Keys](../sql-server-certificates-and-asymmetric-keys.md)＞。

 當啟用 TDE 時，您應該立即備份憑證以及與此憑證有關的私密金鑰。 如果此憑證無法使用或是您必須在另一部伺服器上還原或附加資料庫，您必須同時擁有此憑證和私密金鑰的備份，否則將無法開啟資料庫。 即使資料庫上不再啟用 TDE，還是應該保留加密憑證。 就算資料庫並未加密，交易記錄的某些部分可能仍受到保護，因而有些作業截至資料庫執行完整備份為止或許都需要此憑證。 已經超過到期日的憑證仍然可用來搭配 TDE 加密和解密資料。

 **加密階層**

 下圖顯示 TDE 加密的架構。 在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]上使用 TDE 時，只有資料庫層級項目 (資料庫加密金鑰) 和 ALTER DATABASE 部分是使用者可設定的。

 ![顯示主題中所描述的階層。](../../../database-engine/media/tde-architecture.gif "顯示主題中所描述的階層。")

## <a name="using-transparent-data-encryption"></a>使用透明資料加密
 若要使用 TDE，請遵循下列步驟。

||
|-|
|**適用於**： [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。|

-   建立主要金鑰

-   建立或取得受到主要金鑰保護的憑證

-   建立資料庫加密金鑰，並使用憑證保護它

-   設定資料庫使用加密

 下列範例說明如何使用 `AdventureWorks2012` 伺服器上安裝的憑證來加密和解密 `MyServerCert`資料庫。

```
USE master;
GO
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';
go
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';
go
USE AdventureWorks2012;
GO
CREATE DATABASE ENCRYPTION KEY
WITH ALGORITHM = AES_128
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;
GO
ALTER DATABASE AdventureWorks2012
SET ENCRYPTION ON;
GO
```

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]會將加密和解密作業排定在背景執行緒上。 您可以使用本主題稍後出現之清單內的目錄檢視和動態管理檢視，以檢視這些作業的狀態。

> [!CAUTION]
>  啟用了 TDE 的資料庫備份檔案也會使用資料庫加密金鑰來加密。 因此，當您要還原這些備份時，保護資料庫加密金鑰的憑證必須可以使用。 這表示，除了備份資料庫以外，您也必須確定可維護伺服器憑證的備份，以免資料遺失。 如果此憑證無法再使用，就會造成資料遺失。 如需詳細資訊，請參閱 [SQL Server Certificates and Asymmetric Keys](../sql-server-certificates-and-asymmetric-keys.md)。

## <a name="commands-and-functions"></a>命令與函數
 TDE 憑證必須由資料庫主要金鑰來加密，才能由下列陳述式所接受。 如果只由密碼加密，下列陳述式將會拒絕它們當做加密程式。

> [!IMPORTANT]
>  如果在 TDE 使用這些憑證之後，更改這些憑證使其受到密碼保護，將會造成資料庫重新啟動之後無法存取。

 下表提供 TDE 命令和函數的連結與說明。

|命令或函數|目的|
|-------------------------|-------------|
|[CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)|建立用於加密資料庫的金鑰|
|[ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-encryption-key-transact-sql)|變更用於加密資料庫的金鑰|
|[DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-transact-sql)|移除用於加密資料庫的金鑰。|
|[ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)|說明用來啟用 TDE 的 `ALTER DATABASE` 選項。|

## <a name="catalog-views-and-dynamic-management-views"></a>目錄檢視和動態管理檢視
 下表顯示 TDE 目錄檢視和動態管理檢視。

|目錄檢視或動態管理檢視|目的|
|---------------------------------------------|-------------|
|[sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)|顯示資料庫資訊的目錄檢視。|
|[sys.certificates &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-certificates-transact-sql)|顯示資料庫中之憑證的目錄檢視。|
|[sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)|提供了用於資料庫之加密金鑰及資料庫之加密狀態相關資訊的動態管理檢視。|

## <a name="permissions"></a>權限
 TDE 的每一項功能和命令都有個別的權限需求，如同之前所示的表格所述。

 檢視與 TDE 有關的中繼資料將需要憑證的 VIEW DEFINITION 權限。

## <a name="considerations"></a>考量
 當資料庫加密作業的重新加密掃描正在進行時，對資料庫的維護作業將會停用。 您可以使用資料庫的單一使用者模式設定來執行維護作業。 如需詳細資訊，請參閱 [將資料庫設定為單一使用者模式](../../databases/set-a-database-to-single-user-mode.md)。

 您可以使用 sys.dm_database_encryption_keys 動態管理檢視來尋找資料庫加密的狀態。 如需詳細資訊，請參閱本主題前面的＜目錄檢視和動態管理檢視＞一節。

 在 TDE 中，資料庫內的所有檔案和檔案群組都會加密。 如果資料庫內有任何檔案群組標示為 READ ONLY，則資料庫加密作業將會失敗。

 如果在資料庫鏡像或記錄傳送中使用資料庫，這兩個資料庫都會加密。 記錄交易在這兩者之間傳送時將會加密。

> [!IMPORTANT]
>  當設定資料庫進行加密時，所有新的全文檢索索引都會加密。 之前建立的全文檢索索引將會在升級期間匯入，而且一旦資料載入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]之後，這些索引將會使用 TDE。 在資料行上啟用全文檢索索引會造成該資料行的資料在全文檢索索引掃描期間，以純文字格式寫入磁碟上。 我們建議您不要在敏感性加密資料上建立全文檢索索引。

 加密資料的壓縮比大幅低於對等的未加密資料。 如果使用 TDE 來加密資料庫，則備份壓縮將無法大幅壓縮備份儲存體。 因此，不建議您同時使用 TDE 與備份壓縮。

### <a name="restrictions"></a>限制
 在初始資料庫加密、金鑰變更或資料庫解密期間，不允許以下作業：

-   從資料庫中的檔案群組卸除檔案

-   卸除資料庫

-   讓資料庫離線

-   卸離資料庫

-   將資料庫或檔案群組轉換成 READ ONLY 狀態

 在執行 CREATE DATABASE ENCRYPTION KEY、ALTER DATABASE ENCRYPTION KEY、DROP DATABASE ENCRYPTION KEY 或 ALTER DATABASE...SET ENCRYPTION 陳述式期間，不允許下列作業。

-   從資料庫中的檔案群組卸除檔案。

-   卸除資料庫。

-   讓資料庫離線。

-   卸離資料庫。

-   將資料庫或檔案群組轉換成 READ ONLY 狀態。

-   使用 ALTER DATABASE 命令。

-   啟動資料庫或資料庫檔案備份。

-   啟動資料庫或資料庫檔案還原。

-   建立快照集。

 下列作業或條件會讓 CREATE DATABASE ENCRYPTION KEY、ALTER DATABASE ENCRYPTION KEY、DROP DATABASE ENCRYPTION KEY 或 ALTER DATABASE...SET ENCRYPTION 陳述式無法執行。

-   資料庫是唯讀的，或是具有任何唯讀的檔案群組。

-   正在執行 ALTER DATABASE 命令。

-   正在執行任何資料備份。

-   資料庫處於離線或還原狀況。

-   快照集正在進行中。

-   資料庫維護工作。

 在建立資料庫檔案時，啟用 TDE 時無法使用立即檔案初始化功能。

 為了利用非對稱金鑰加密資料庫加密金鑰，非對稱金鑰必須位在可延伸金鑰管理提供者上。

### <a name="transparent-data-encryption-and-transaction-logs"></a>透明資料加密和交易記錄
 讓資料庫使用 TDE 會產生讓虛擬交易記錄的其餘部分歸零的結果，以強制使用下一個虛擬交易記錄。 這樣可確保在設定資料庫進行加密之後，交易記錄中不會留下任何純文字。 您可以尋找記錄檔加密的狀態，其方式是檢視 `encryption_state` 檢視中的 `sys.dm_database_encryption_keys` 資料行，如以下範例所示：

```
USE AdventureWorks2012;
GO
/* The value 3 represents an encrypted state 
   on the database and transaction logs. */
SELECT *
FROM sys.dm_database_encryption_keys
WHERE encryption_state = 3;
GO
```

 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 記錄檔架構的詳細資訊，請參閱 [&#40;SQL Server&#41;](../../logs/the-transaction-log-sql-server.md)。

 在資料庫加密金鑰變更之前寫入交易記錄的所有資料，都會使用之前的資料庫加密金鑰進行加密。

 當資料庫加密金鑰已經修改兩次之後，您就必須先執行記錄備份，然後才能再次修改資料庫加密金鑰。

### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>透明資料加密和 tempdb 系統資料庫
 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上的任何其他資料庫是使用 TDE 進行加密，則 tempdb 系統資料庫將會加密。 這可能會對於相同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體上未加密的資料庫造成效能上的影響。 如需 tempdb 系統資料庫的詳細資訊，請參閱 [tempdb 資料庫](../../databases/tempdb-database.md)。

### <a name="transparent-data-encryption-and-replication"></a>透明資料加密和複寫
 複寫不會自動使用加密形式來複寫啟用 TDE 之資料庫內的資料。 如果您想要保護散發資料庫和訂閱者資料庫，必須個別啟用 TDE。 快照式複寫及異動複寫和合併式複寫之資料的初始散發都可以將資料儲存在未加密的中繼檔案中，例如 bcp 檔案。  在異動複寫或合併式複寫期間，可以啟用加密來保護通訊通道。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。

### <a name="transparent-data-encryption-and-filestream-data"></a>透明資料加密和 FILESTREAM DATA
 即使啟用了 TDE，FILESTREAM 資料也不會加密。

### <a name="transparent-data-encryption-and-buffer-pool-extension"></a>透明資料加密和緩衝集區擴充
 使用 TDE 將資料庫加密時，與緩衝集區擴充 (BPE) 相關的檔案未受到加密。 您必須針對 BPE 相關檔案使用 Bitlocker 或 EFS 等檔案系統層級加密工具。

## <a name="transparent-data-encryption-and-in-memory-oltp"></a>透明資料加密和記憶體中 OLTP
 TDE 可在具有記憶體中 OLTP 物件的資料庫上啟用。 如果啟用 TDE，則會加密記憶體中 OLTP 記錄。 啟用 TDE 時，並不會加密 MEMORY_OPTIMIZED_DATA 檔案群組中的資料。

## <a name="see-also"></a>另請參閱
 [將 TDE 保護的資料庫移至另一個 SQL Server](move-a-tde-protected-database-to-another-sql-server.md) [使用 EKM](enable-tde-on-sql-server-using-ekm.md) [透明資料加密 Azure SQL Database](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md) [SQL Server 加密](sql-server-encryption.md) [SQL Server 和資料庫加密金鑰 &#40;](sql-server-and-database-encryption-keys-database-engine.md)資料庫引擎&#41;資訊安全中心 SQL Server 資料庫引擎和[Azure SQL Database](../security-center-for-sql-server-database-engine-and-azure-sql-database.md) [FILESTREAM &#40;](../../blob/filestream-sql-server.md) SQL Server&#41;，以啟用 TDE


