---
title: "BACKUP DATABASE (平行處理資料倉儲) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc87423b3444daf6d44f590c283b52ce948da193
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="backup-database-parallel-data-warehouse"></a>BACKUP DATABASE (平行處理資料倉儲)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  建立[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫的備份，並將備份儲存在應用裝置外、使用者指定的網路位置中。 請搭配 [RESTORE DATABASE &#40;平行處理資料倉儲&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md) 使用此陳述式來進行災害復原，或將資料庫從一個應用裝置複製到另一個應用裝置。  
  
 **在您開始前**，請先參閱[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的＜Acquire and Configure a Backup Server＞(取得並設定備份伺服器)。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中有兩種類型的備份。 「完整資料庫備份」會備份整個[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫。 「差異資料庫備份」僅包含自上次進行完整備份之後所做的變更。 使用者資料庫的備份會包含資料庫使用者及資料庫角色。 master 資料庫的備份會包含登入。  
  
 如需有關[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫備份的詳細資訊，請參閱[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的＜Backup and Restore＞(備份和還原)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
      Create a full backup of a user database or the master database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    [ WITH [ ( ]  <with_options> [ ,...n ]  [ ) ] ]  
[;]  
  
Create a differential backup of a user database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    WITH [ ( ] DIFFERENTIAL   
    [ , <with_options> [ ,...n ] [ ) ]  
[;]  
  
<with_options> ::=  
    DESCRIPTION = 'text'  
    | NAME = 'backup_name'  
  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 要作為備份建立位置的資料庫名稱。 此資料庫可以是 master 資料庫或使用者資料庫。  
  
 TO DISK = '\\\\*UNC_path*\\*backup_directory*'  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]寫入備份檔案時的目的地網路路徑和目錄。 例如 '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'。  
  
-   備份目錄名稱的路徑必須已經存在，且必須以完整通用命名慣例 (UNC) 路徑的形式指定。  
  
-   備份目錄 *backup_directory* 必須是在執行備份命令之前不存在的目錄。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會建立備份目錄。  
  
-   備份目錄的路徑不可以是本機路徑，也不可以是任何[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]應用裝置節點上的位置。  
  
-   UNC 路徑和備份目錄名稱的長度上限是 200 個字元。  
  
-   伺服器或主機必須以 IP 位址的形式指定。  您不能以主機或伺服器名稱的形式指定它。  
  
 DESCRIPTION = **'***text***'**  
 指定備份的文字描述。 文字的長度上限為 255 個字元。  
  
 此描述會儲存在中繼資料中，並且會在使用 RESTORE HEADERONLY 來還原備份標頭時顯示。  
  
 NAME = **'***backup _name***'**  
 指定備份的名稱。 備份名稱可以與資料庫名稱不同。  
  
-   名稱最多可有 128 個字元。  
  
-   不可包含路徑。  
  
-   開頭必須是字母、數字字元或底線 (_)。 允許的特殊字元是底線 (\_)、連字號 (-) 或空格 space ( )。 備份名稱的結尾不可以是空格字元。  
  
-   如果 *backup_name*已經存在於指定的位置中，陳述式將會失敗。  
  
 此名稱會儲存在中繼資料中，並且會在使用 RESTORE HEADERONLY 來還原備份標頭時顯示。  
  
 DIFFERENTIAL  
 指定執行使用者資料庫的差異備份。 如果省略，預設就會是完整資料庫備份。 差異備份的名稱不一定要與完整備份的名稱相符。 為了追蹤差異備份及其對應的完整備份，請考慮使用相同名稱再附加 'full' 或 'diff'。  
  
 例如：  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Permissions  
 需要 **BACKUP DATABASE** 權限或 **db_backupoperator** 固定資料庫角色的成員資格。 新增至 **db_backupoperator** 固定資料庫角色的一般使用者無法備份 master 資料庫。 只有 **sa**、網狀架構系統管理員或 **sysadmin** 固定伺服器角色的成員才能備份 master 資料庫。  
  
 需要具備備份目錄之存取、建立及寫入權限的 Windows 帳戶。 您也必須將 Windows 帳戶名稱和密碼儲存在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中。 若要將這些網路認證新增至[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，請使用 [sp_pdw_add_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 預存程序。  
  
 如需有關管理[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中之認證的詳細資訊，請參閱[安全性](#Security)一節。  
  
## <a name="error-handling"></a>錯誤處理  
 在下列情況下會發生 BACKUP DATABASE 錯誤：  
  
-   使用者權限不足以執行備份。  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]沒有將儲存備份之網路位置的正確權限。  
  
-   資料庫不存在。  
  
-   目標目錄已經存在於網路共用上。  
  
-   目標網路共用無法使用。  
  
-   目標網路共用沒有足夠的空間來進行備份。 BACKUP DATABASE 命令在起始備份之前，未先確認是否有足夠的空間存在，導致在執行 BACKUP DATABASE 時，可能產生磁碟空間不足錯誤。 發生磁碟空間不足問題時，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會復原 BACKUP DATABASE 命令。 若要縮減資料庫大小，請執行 [DBCC SHRINKLOG (Azure SQL 資料倉儲)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)  
  
-   嘗試在交易內啟動備份。  
  
## <a name="general-remarks"></a>一般備註  
 在您執行資料庫之前，請使用 [DBCC SHRINKLOG (Azure SQL 資料倉儲)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) 來縮減資料庫的大小。 
 
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]備份會以多檔案集合的形式儲存在相同的目錄中。  
  
 差異備份所花費的時間通常比完整備份少，因此可以較頻繁地執行。 當多個差異備份都根據相同的完整備份時，每個差異備份都會包含前一個差異備份的所有變更。  
  
 如果您取消 BACKUP 命令，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]將會移除目標目錄及為備份建立的所有檔案。 如果[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]與共用的網路連線中斷，便無法完成復原。  
  
 完整備份和差異備份儲存在個別的目錄中。 系統並未強制執行命名慣例來要求指定完整備份和差異備份彼此互屬。 您可以透過自己的命名慣例來進行此追蹤。 或者，您也可以藉由使用 WITH DESCRIPTION 選項來新增描述，然後使用 RESTORE HEADERONLY 陳述式來擷取描述，以進行此追蹤。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 您無法對 master 資料庫執行差異備份。 僅支援對 master 資料庫執行完整備份。  
  
 備份檔案會以僅適用於使用 [RESTORE DATABASE &#40;平行處理資料倉儲&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)陳述式將備份還原至[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]的格式儲存。  
  
 搭配 BACKUP DATABASE 陳述式的備份無法用來將檔案或使用者資訊傳輸給 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 如需該功能，您可以使用遠端資料表複製功能。 如需詳細資訊，請參閱[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的＜Remote Table Copy＞(遠端資料表複製)。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份技術來備份和還原資料庫。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份選項已預先設定為使用備份壓縮。 您無法設定壓縮、總和檢查碼、區塊大小及緩衝區計數等備份選項。  
  
 在任何指定時間，都只能在應用裝置上執行一個資料庫備份或還原作業。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會將備份或還原命令排入佇列，直到目前的備份或還原命令完成為止。  
  
 用來還原備份的目標應用裝置所擁有的計算節點數目必須至少與來源應用裝置相同。 目標所擁有的計算節點數目可以比來源應用裝置多，但不能比來源應用裝置少。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]不會追蹤備份的位置和名稱，因為備份會儲存在應用裝置外。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]不會追蹤資料庫備份是成功還是失敗。  
  
 只有在上一個完整備份已成功完成的情況下，才會允許執行差異備份。 例如，假設您在星期一建立銷售資料庫的完整備份，且該備份成功完成。 然後，您在星期二建立銷售資料庫的完整備份，但卻失敗。 在發生此失敗之後，您便無法根據星期一的完整備份來建立差異備份。 您必須先建立成功的完整備份，才能建立差異備份。  
  
## <a name="metadata"></a>中繼資料  
 這些動態管理檢視包含所有備份、還原及載入作業的相關資訊。 此資訊在系統重新啟動之後會持續存留。  
  
-   [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>[效能]  
 若要執行備份，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會先備份中繼資料，然後對儲存在計算節點上的資料庫資料執行平行備份。 這會將資料直接從每個計算節點複製到備份目錄。 為了在將資料從計算節點移至備份目錄時達到最佳效能，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會控制同時複製資料的計算節點數目。  
  
## <a name="locking"></a>鎖定  
 在 DATABASE 物件上採用 ExclusiveUpdate 鎖定。  
  
##  <a name="Security"></a> 安全性  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]備份不會儲存在應用裝置上。 因此，您的 IT 小組需負責管理備份安全性的所有層面。 例如，這包括管理備份資料的安全性、用來儲存備份之伺服器的安全性、以及將備份伺服器連線至[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]之網路基礎結構的安全性。  
  
 **管理網路認證**  
  
 對備份目錄的網路存取權是根據標準 Windows 檔案共用安全性。 在執行備份之前，您必須建立或指定一個將用來向備份目錄驗證[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]的 Windows 帳戶。 此 Windows 帳戶必須具備備份目錄之存取、建立及寫入權限。  
  
> [!IMPORTANT]  
>  為了降低您資料的安全性風險，建議您指定一個專門用來執行備份和還原作業的 Windows 帳戶。 請讓此帳戶僅擁有備份位置的權限。  
  
 您必須藉由執行 [sp_pdw_add_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 預存程序，將使用者名稱和密碼儲存在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會使用「Windows 認證管理員」在控制節點及計算節點上，儲存並加密使用者名稱和密碼。 備份認證時，不會使用 BACKUP DATABASE 命令來備份。  
  
 若要從[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]移除網路認證，請參閱 [sp_pdw_remove_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)。  
  
 若要列出儲存在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中的所有網路認證，請使用 [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) 動態管理檢視。  
  
## <a name="examples"></a>範例  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. 新增備份位置的網路認證  
 若要建立備份，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]必須具備備份目錄的讀取/寫入權限。 下列範例示範如何新增使用者的認證。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會儲存這些認證，並使用它們來進行備份和還原作業。  
  
> [!IMPORTANT]  
>  基於安全性考量，建議您建立一個專門用來執行備份的網域帳戶。  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. 移除備份位置的網路認證  
 下列範例示範如何從[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中移除網域使用者的認證。  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. 建立使用者資料庫的完整備份  
 下列範例會建立 Invoices 使用者資料庫的完整備份。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會建立 [Invoices2013] 目錄，並將備份檔案儲存至 \\\10.192.63.147\backups\yearly\Invoices2013Full 目錄。  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. 建立使用者資料庫的差異備份  
 下列範例會建立差異備份，其中包括自上次完整備份 Invoices 資料庫之後所做的所有變更。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會建立 \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff 目錄來儲存檔案。 'Invoices 2013 differential backup' 描述將會與備份的標頭資訊儲存在一起。  
  
 只有在 Invoices 的上一個完整備份已成功完成的情況下，差異備份才會執行成功。  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. 建立 master 資料庫的完整備份  
 下列範例會建立 master 資料庫的完整備份，並將其儲存在 '\\\10.192.63.147\backups\2013\daily\20130722\master' 目錄中。  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. 建立應用裝置登入資訊的備份。  
 master 資料庫會儲存應用裝置登入資訊。 若要備份應用裝置登入資訊，您必須備份 master。  
  
 下列範例會建立 master 資料庫的完整備份。  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>另請參閱  
 [RESTORE DATABASE &#40;平行處理資料倉儲&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  
