---
title: RESTORE DATABASE (平行處理資料倉儲) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: 8
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0fb3c753e4bde29eb9b5cbb5f287fc18d03a117a
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37782429"
---
# <a name="restore-database-parallel-data-warehouse"></a>RESTORE DATABASE (平行處理資料倉儲)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  將[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]使用者資料庫從資料庫備份還原到[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 資料庫會從 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)][BACKUP DATABASE &#40;平行處理資料倉儲&#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md) 命令先前所建立備份還原。 您可以使用備份和還原作業來建置災害復原計劃，或將資料庫從一個應用裝置移至另一個應用裝置。  
  
> [!NOTE]  
>  還原 master 時，會包括還原應用裝置登入資訊。 若要還 master，請使用**組態管理員**工具中的[還原 master 資料庫 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)頁面。 能夠存取控制節點的系統管理員將可執行這項作業。  
  
 如需有關[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫備份的詳細資訊，請參閱[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的＜Backup and Restore＞(備份和還原)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
      Restore the master database  
-- Use the Configuration Manager tool.  
  
Restore a full user database backup.  
RESTORE DATABASE database_name   
    FROM DISK = '\\UNC_path\full_backup_directory'  
[;]  
  
Restore a full user database backup and then a differential backup.  
RESTORE DATABASE database_name  
    FROM DISK = '\\UNC_path\differential_backup_directory'   
    WITH [ ( ] BASE = '\\UNC_path\full_backup_directory' [ ) ]   
[;]  
  
Restore header information for a full or differential user database backup.  
RESTORE HEADERONLY   
    FROM DISK = '\\UNC_path\backup_directory'  
[;]  
```  
  
## <a name="arguments"></a>引數  
 RESTORE DATABASE *database_name*  
 指定將使用者資料庫還原至名為 *database_name* 的資料庫。 所還原資料庫的名稱可以與所備份來源資料庫的名稱不同。 *database_name* 不可以是目的地應用裝置上已經存在的資料庫。 如需有關所允許資料庫名稱的更多詳細資料，請參閱[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的＜Object Naming Rules＞(物件命名規則)。  
  
 還原使用者資料庫時，會將完整資料庫備份及視需要將差異備份還原至應用裝置。 還原使用者資料庫時，會包括還原資料庫使用者和資料庫角色。  
  
 FROM DISK = '\\\\*UNC_path*\\*backup_directory*'  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]還原備份檔案時的來源網路路徑和目錄。 例如 FROM DISK = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'。  
  
 *backup_directory*  
 指定包含完整或差異備份的目錄名稱。 例如，您可以在完整或差異備份上執行 RESTORE HEADERONLY 作業。  
  
 *full_backup_directory*  
 指定包含完整備份的目錄名稱。  
  
 *differential_backup_directory*  
 指定包含差異備份的目錄名稱。  
  
-   備份目錄的路徑必須已經存在，且必須以完整通用命名慣例 (UNC) 路徑的形式指定。  
  
-   備份目錄的路徑不可以是本機路徑，也不可以是任何[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]應用裝置節點上的位置。  
  
-   UNC 路徑和備份目錄名稱的長度上限是 200 個字元。  
  
-   伺服器或主機必須以 IP 位址的形式指定。  
  
 RESTORE HEADERONLY  
 指定只傳回一個使用者資料庫備份的標頭資訊。 標頭包含備份的文字描述和備份名稱等。 備份名稱不一定要與儲存備份檔案的目錄同名。  
  
 RESTORE HEADERONLY 結果會比照 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY 結果的模式。 此結果有超過 50 個資料行，這些資料行不會完全供[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]使用。 如需有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY 結果中資料行的描述，請參閱 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 **CREATE ANY DATABASE** 權限。  
  
 需要具備備份目錄之存取和讀取權限的 Windows 帳戶。 您也必須將 Windows 帳戶名稱和密碼儲存在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中。  
  
1.  若要確認認證是否已經存在，請使用 [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)。  
  
2.  若要新增或更新認證，請使用 [sp_pdw_add_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)。  
  
3.  若要從[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]移除認證，請使用 [sp_pdw_remove_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)。  
  
## <a name="error-handling"></a>錯誤處理  
 在下列情況下，RESTORE DATABASE 命令會造成錯誤：  
  
-   目標應用裝置上已經有要還原之資料庫的名稱。 若要避免此問題，請選擇一個唯一的資料庫名稱，或在執行還原之前，先卸除現有的資料庫。  
  
-   備份目錄中有一組無效的備份檔案。  
  
-   登入權限不足以還原資料庫。  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]沒有備份檔案所在網路位置的正確權限。  
  
-   備份目錄的網路位置不存在或無法使用。  
  
-   計算節點或控制節點上的磁碟空間不足。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]在起始還原之前，未先確認應用裝置上是否有足夠的磁碟空間。 因此，在執行 RESTORE DATABASE 陳述式時，可能產生磁碟空間不足錯誤。 發生磁碟空間不足問題時，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會復原還原作業。  
  
-   作為資料庫還原目的地之目標應用裝置的計算節點數目，比備份資料庫時之來源應用裝置的計算節點數目少。  
  
-   從交易內嘗試執行資料庫還原。  
  
## <a name="general-remarks"></a>一般備註  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會追蹤資料庫還原是否成功。 在還原差異資料庫備份之前，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會確認完整資料庫還原已成功完成。  
  
 還原之後，使用者資料庫的資料庫相容性層級相會是 120。 這適用於所有資料庫，不論其原始相容性層級為何。  
  
 **還原至具有大量計算節點的應用裝置**  
將資料庫從較小型應用裝置還原至較大型應用裝置之後，請執行 [DBCC SHRINKLOG (Azure SQL 資料倉儲)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)，因為轉散發會增加交易記錄。  

將備份還原至具有較多計算節點的應用裝置時，會讓已配置的資料庫大小依計算節點數目比例成長。  
  
例如，將 60 GB 資料庫從具有 2 個節點的應用裝置 (每個節點 30 GB) 還原至具有 6 個節點的應用裝置時，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會在具有 6 個節點的應用裝置上建立一個 180 GB 的資料庫 (6 個節點，每個節點 30 GB)。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]一開始會將資料庫還原至 2 個節點以符合來源組態，然後會將資料轉散發至全部 6 個節點。  
  
 在轉散發之後，與較小型的來源應用裝置相比，每個計算節點將會包含較少的實際資料和較多的可用空間。 請使用額外的空間將更多資料新增至資料庫。 如果所還原的資料庫大於您所需的大小，您可以使用 [ALTER DATABASE &#40;平行處理資料倉儲&#41;](../../t-sql/statements/alter-database-transact-sql.md?&tabs=sqlpdw)來縮減資料庫檔案大小。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 就這些限制而言，來源應用裝置是您從中建立資料庫備份的應用裝置，而目標應用裝置則是將作為資料庫還原目的地的應用裝置。  
  
 還原資料庫並不會自動重建統計資料。  
  
 在任何指定時間，在應用裝置上都只能執行一個 RESTORE DATABASE 或 BACKUP DATABASE 陳述式。 如果同時提交多個備份和還原陳述式，應用裝置就會將它們排入佇列，然後一次處理一個陳述式。  
  
 您只能將資料庫備份還原至所擁有計算節點數目等於或大於來源應用裝置的[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]目標應用裝置。 目標應用裝置所擁有的計算節點數目不可以比來源應用裝置少。  
  
 您無法將在具有 SQL Server 2012 PDW 硬體之應用裝置上建立的備份，還原至具有 SQL Server 2008 R2 硬體的應用裝置。 即使原先購買應用裝置時是配備 SQL Server 2008 R2 PDW 硬體，而現在執行的是 SQL Server 2012 PDW 軟體，也適用此限制。  
  
## <a name="locking"></a>鎖定  
 在 DATABASE 物件上採用獨佔鎖定。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-restore-examples"></a>A. 簡單的 RESTORE 範例  
 下列範例會將完整資料庫備份還原至 `SalesInvoices2013` 資料庫。 備份檔案會儲存在 \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full 目錄中。 SalesInvoices2013 資料庫不可以是目標應用裝置上已經存在的資料庫，否則此命令會因發生錯誤而失敗。  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>B. 還原完整和差異備份  
 下列範例會先將完整備份還原至 SalesInvoices2013 資料庫，然後再將差異備份還原至該資料庫  
  
 還原資料庫完整備份時，會從儲存在 '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full' 目錄中的完整備份還原。 如果還原順利完成，系統就會將差異備份還原至 SalesInvoices2013 資料庫。  差異備份會儲存在 '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff' 目錄中。  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. 還原備份標頭  
 此範例會還原資料庫備份 '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full' 的標頭資訊。 此命令會為 Invoices2013Full 備份產生一列資訊。  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 您可以使用此標頭資訊來檢查備份的內容，或在嘗試還原備份之前，先確認目標還原應用裝置與來源備份應用裝置相容。  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP DATABASE &#40;平行處理資料倉儲&#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  
