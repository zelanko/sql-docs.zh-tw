---
title: 使用卸離與附加來升級資料庫 (Transact-SQL) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database attaching [SQL Server]
- upgrading databases
- database upgrades [SQL Server]
- database detaching [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 99f66ed9-3a75-4e38-ad7d-6c27cc3529a9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 39e9db45723d32fd78eef35c5600d05b54999e61
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749212"
---
# <a name="upgrade-a-database-using-detach-and-attach-transact-sql"></a>使用卸離與附加來升級資料庫 (Transact-SQL)
  本主題描述如何使用卸離和附加作業升級 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的資料庫。 附加至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之後，資料庫可立即使用並自動進行升級。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **升級 SQL Server 資料庫：**  
  
     [使用卸離和附加作業](#SSMSProcedure)  
  
-   **後續操作：**[升級 SQL Server 資料庫之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   您無法附加系統資料庫。  
  
-   若將資料庫的 [跨資料庫擁有權鏈結] 選項設為 0，附加與卸離會停用資料庫的跨資料庫擁有權鏈結。 如需啟用鏈結的資訊，請參閱[跨資料庫擁有權鏈結伺服器組態選項](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)。  
  
-   當附加複製的而非卸離的複寫資料庫時：  
  
    -   如果您附加資料庫到相同伺服器執行個體的升級版本，則必須在附加作業完成後執行 **sp_vupgrade_replication** 以升級複寫。 如需詳細資訊，請參閱 [sp_vupgrade_replication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql)。  
  
    -   如果您附加資料庫到不同的伺服器執行個體 (不論版本為何)，則必須在附加作業完成後執行 **sp_removedbreplication** 以移除複寫。 如需詳細資訊，請參閱 [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)。  
  
###  <a name="Recommendations"></a> 建議  
 建議您不要附加或還原來源不明或來源不受信任的資料庫。 這種資料庫可能包含惡意程式碼，因此可能執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述或實體資料庫結構而造成錯誤。 使用來源不明或來源不受信任的資料庫之前，請先在非實際伺服器的資料庫上執行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) ，同時檢查資料庫中的程式碼，例如預存程序或其他使用者定義程式碼。  
  
##  <a name="SSMSProcedure"></a> 使用卸離和附加來升級資料庫  
  
1.  卸離資料庫。 如需詳細資訊，請參閱 [卸離資料庫](detach-a-database.md)。  
  
2.  另外，也可以移動卸離的資料庫檔案與記錄檔。  
  
     即使您要建立新的記錄檔，仍應連同資料檔案一併移動記錄檔。 在某些情況下，重新附加資料庫需要其現有的記錄檔。 因此，一律保留所有卸離的記錄檔，直到資料庫在沒有這些檔案的情形下成功附加為止。  
  
    > [!NOTE]  
    >  如果您嘗試在不指定記錄檔的情形下附加資料庫，附加作業會在其原始位置中尋找記錄檔。 如果記錄的原始副本仍在原處，則會附加該副本。 若要避免使用原始記錄檔，請指定新記錄檔的路徑，或者移除記錄檔的原始副本 (在將記錄檔複製到新位置後)。  
  
3.  將複製的檔案附加至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體。 如需詳細資訊，請參閱 [Attach a Database](attach-a-database.md)。  
  
## <a name="example"></a>範例  
 下列範例會從舊版 SQL Server 升級資料庫的副本。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會在 [查詢編輯器] 視窗中執行，此視窗連接到附加的伺服器執行個體。  
  
1.  執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式卸離資料庫：  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'MyDatabase';  
    GO  
    ```  
  
2.  使用您選擇的方法，將資料和記錄檔複製到新的位置。  
  
    > [!IMPORTANT]  
    >  針對實際執行的資料庫，將資料庫與交易記錄放在不同的磁碟上。  
  
     若要經由網路將檔案複製到遠端電腦的磁碟，請使用遠端位置的通用命名慣例 (UNC) 名稱。 UNC 名稱的格式為 **\\\\***Servername***\\***Sharename***\\***Path***\\***Filename*。 如同將檔案寫入本機硬碟一樣，您必須將在遠端磁碟讀取或寫入檔案所需的適當權限，授與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體所用的使用者帳戶。  
  
3.  若要附加已移動的資料庫和記錄檔 (選擇性)，請執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyDatabase   
        ON (FILENAME = 'C:\MySQLServer\MyDatabase.mdf'),  
        (FILENAME = 'C:\MySQLServer\Database.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，新附加的資料庫無法立即在 [物件總管] 中可見。 若要檢視資料庫，請在 [物件總管] 中按一下 **[檢視]** ，然後按一下 **[重新整理]**。 在 [物件總管] 中展開 **[資料庫]** 節點時，剛才附加的資料庫就會出現在資料庫清單中。  
  
##  <a name="FollowUp"></a> 後續操作：升級 SQL Server 資料庫之後  
 如果資料庫具有全文檢索索引，升級程序就會根據 **upgrade_option** 伺服器屬性的設定，匯入、重設或重建這些索引。 如果升級選項設定為匯入 (**upgrade_option** = 2) 或重建 (**upgrade_option** = 0)，則全文檢索索引在升級期間將無法使用。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建可能需要十倍以上的時間。 此外，請注意，當升級選項設定為 [匯入] 時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。 若要變更 **upgrade_option** 伺服器屬性的設定，請使用 [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)。  
  
### <a name="database-compatibility-level-after-upgrade"></a>升級後的資料庫相容性層級  
 如果使用者資料庫的相容性層級在升級前為 100 或更高層級，則在升級後仍會保持相同。 如果升級前的相容性層級為 90，則在升級後的資料庫中，相容性層級會設定為 100 (這是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所支援的最低相容性層級)。 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。  
  
### <a name="managing-metadata-on-the-upgraded-server-instance"></a>在升級的伺服器執行個體上管理中繼資料  
 將資料庫附加至另一個伺服器執行個體時，為了提供一致的經驗給使用者和應用程式，您可能需要在其他伺服器執行個體上為資料庫重新建立部分或所有的中繼資料，例如登入、作業和權限。 如需詳細資訊，請參閱 [在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
### <a name="service-master-key-and-database-master-key-encryption-changes-from-3des-to-aes"></a>服務主要金鑰和資料庫主要金鑰加密從 3DES 到 AES 的變化  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本會使用 AES 加密演算法來保護服務主要金鑰 (SMK) 及資料庫主要金鑰 (DMK)。 與舊版中使用的 3DES 相比，AES 是一種較新的加密演算法。 當資料庫第一次連接或還原到新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體時，資料庫主要金鑰複本 (由服務主要金鑰加密) 尚未儲存在伺服器中。 您必須利用 `OPEN MASTER KEY` 陳述式來解密資料庫主要金鑰 (DMK)。 DMK 解密之後，您便可以選擇利用 `ALTER MASTER KEY REGENERATE` 陳述式來提供服務主要金鑰 (SMK) 所加密的 DMK 複本給伺服器，以在未來啟用自動解密。 當資料庫從舊版升級時，應該會重新產生 DMK 以使用較新的 AES 演算法。 如需重新產生 DMK 的詳細資訊，請參閱 [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql)。 重新產生 DMK 金鑰以升級至 AES 所需的時間是取決於 DMK 所保護的物件數目而定。 重新產生 DMK 金鑰以升級至 AES 只需執行一次，且不會影響金鑰循環策略中後續的重新產生。  
  
  
