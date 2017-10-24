---
title: "備份資料庫 (Parallel Data Warehouse) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4fb36fd89c02ff9ddd5bc33825a387b53ab6e174
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="backup-database-parallel-data-warehouse"></a>備份資料庫 (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  建立的備份[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫，並將關閉應用裝置的備份儲存在使用者指定的網路位置。 使用此陳述式與[還原資料庫 &#40;平行資料倉儲 &#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)災害復原，或將資料庫複製到另一個應用裝置。  
  
 **開始之前**，請參閱中的 < 取得和設定備份伺服器 > [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 有兩種類型的備份中[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 A*完整資料庫備份*是整個備份[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫。 A*差異資料庫備份*只包含自上次完整備份之後所做的變更。 使用者資料庫的備份包含資料庫使用者與資料庫角色。 Master 資料庫的備份會包含登入。  
  
 如需有關[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫備份，請參閱 「 備份和還原 」 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 建立備份的資料庫名稱。 資料庫可以是主要資料庫或使用者資料庫。  
  
 磁碟 = '\\\\*UNC_path*\\*backup_directory*'  
 網路路徑及目錄的[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]將寫入備份檔案。 例如，'\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'。  
  
-   備份目錄名稱的路徑必須存在，而且必須指定為完整的通用命名慣例 (UNC) 路徑。  
  
-   備份目錄中， *backup_directory*，必須存在才能執行備份命令。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]將建立備份目錄。  
  
-   備份目錄的路徑不能是本機路徑，它不能是任何位置[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]應用裝置節點。  
  
-   備份目錄名稱與 UNC 路徑的最大長度為 200 個字元。  
  
-   必須指定伺服器或主機，IP 位址。  您無法指定它做為主機或伺服器名稱。  
  
 描述 = **'***文字***'**  
 指定備份的文字描述。 文字的最大長度為 255 個字元。  
  
 描述儲存在中繼資料，而且 RESTORE HEADERONLY 還原備份標頭時，會顯示。  
  
 名稱 = **'***備份 b***'**  
 指定之備份的名稱。 備份名稱可以不同的資料庫名稱。  
  
-   名稱最多可有 128 個字元。  
  
-   不能包含路徑。  
  
-   必須以字母或數字字元或底線 (_) 開頭。 允許的特殊字元是底線 (\_)、 連字號 （-） 或空格 （）。 備份名稱結尾不能是空格字元。  
  
-   如果陳述式將會失敗*backup_name*已存在於指定的位置。  
  
 這個名稱儲存在中繼資料，並且使用 RESTORE HEADERONLY 還原備份標頭時，將會顯示。  
  
 DIFFERENTIAL  
 指定要執行的使用者資料庫的差異備份。 如果省略，預設值是完整資料庫備份。 差異備份的名稱不必符合完整備份的名稱。 追蹤的差異和其相對應的完整備份，請考慮使用 'full' 或 '差異' 附加與相同的名稱。  
  
 例如：  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Permissions  
 需要**BACKUP DATABASE**權限或成員資格**db_backupoperator**固定的資料庫角色。 無法備份 master 資料庫，向上而是由一般使用者加入至**db_backupoperator**固定的資料庫角色。 Master 資料庫可以只備份的**sa**、 網狀架構系統管理員或屬於**sysadmin**固定的伺服器角色。  
  
 需要 Windows 帳戶具有存取、 建立和寫入備份目錄的權限。 您也必須儲存的 Windows 帳戶名稱和密碼[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 若要加入至這些網路認證[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用[sp_pdw_add_network_credentials &#40;SQL 資料倉儲 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)預存程序。  
  
 如需有關管理認證中的[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，請參閱[安全性](#Security)> 一節。  
  
## <a name="error-handling"></a>錯誤處理  
 在下列情況下的備份資料庫錯誤：  
  
-   找不到足以執行備份的使用者權限。  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]沒有正確的權限來儲存備份的網路位置。  
  
-   資料庫不存在。  
  
-   在網路共用上的目標目錄已經存在。  
  
-   無法使用目標網路共用。  
  
-   目標網路共用沒有足夠空間可供備份。 備份資料庫命令不會確認在起始的備份，讓您可以執行備份的資料庫時產生出的磁碟空間錯誤之前有足夠的磁碟空間。 磁碟空間不足時，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]回復 BACKUP DATABASE 命令。 若要減少資料庫的大小，請執行[DBCC SHRINKLOG （Azure SQL 資料倉儲）](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)  
  
-   嘗試啟動交易內的備份。  
  
## <a name="general-remarks"></a>一般備註  
 執行資料庫備份之前，請使用[DBCC SHRINKLOG （Azure SQL 資料倉儲）](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)減少資料庫的大小。 
 
 A[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]備份都會儲存為一組相同的目錄內的多個檔案。  
  
 差異備份通常會比完整備份的時間，並且可以更頻繁地執行。 當多個差異備份根據相同的完整備份時，每個差異會包含的所有變更先前的差異備份中。  
  
 如果您取消備份命令，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]也會移除的目標目錄和備份所建立的任何檔案。 如果[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]失去網路連線至共用，無法完成復原。  
  
 完整備份及差異備份會儲存在個別的目錄中。 指定完整備份及差異備份一起屬於不會強制執行命名慣例。 您可以透過您自己的命名慣例來追蹤。 或者，您可以追蹤這可加入描述，使用具有描述選項，然後使用 RESTORE HEADERONLY 陳述式來擷取說明。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 您無法執行差異備份 master 資料庫。 支援只能在 master 資料庫進行完整備份。  
  
 備份檔案儲存格式僅適用於還原至備份[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]應用裝置使用[還原資料庫 &#40;平行資料倉儲 &#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)陳述式。  
  
 使用 BACKUP DATABASE 陳述式備份不能將資料或使用者資訊傳送到 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 如需該功能，您可以使用遠端資料表複製功能。 如需詳細資訊，請參閱 「 遠端資料表複製 」 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]備份來備份和還原資料庫的技術。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要使用備份壓縮預先設定備份選項。 您無法設定備份的選項，例如壓縮、 總和檢查碼、 區塊大小和緩衝區計數。  
  
 只有一個資料庫備份或還原可以在任何指定時間執行的應用裝置上。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會將佇列 backup 或 restore 命令，直到目前的備份或還原命令已完成。  
  
 還原備份的目標應用裝置必須與來源應用裝置數目，至少計算節點。 目標可以有多個計算節點比來源應用裝置，但不能有較少的計算節點。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]未追蹤位置和名稱的備份，因為備份會儲存為關閉設備。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]未追蹤成功或失敗的資料庫備份。  
  
 如果上個完整備份已順利完成，才允許差異備份。 例如，假設您在上星期一建立 Sales 資料庫的完整備份，而且備份成功完成。 在星期二，您建立在 Sales 資料庫的完整備份，然後它就會失敗。 此失敗之後，您無法再建立差異備份星期一的完整備份為基礎。 您必須建立差異備份之前先建立成功的完整備份。  
  
## <a name="metadata"></a>中繼資料  
 這些動態管理檢視包含所有備份、 還原的相關資訊和載入作業。 資訊會保留在系統重新啟動。  
  
-   [sys.pdw_loader_backup_runs &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>效能  
 若要執行備份，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]第一個備份中繼資料，然後執行平行備份儲存在計算節點上的資料庫資料。 資料是直接從每個計算節點複製到備份目錄。 若要達成最佳效能將資料從運算節點移到備份目錄中，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]控制要同時複製資料的計算節點的數目。  
  
## <a name="locking"></a>鎖定  
 資料庫物件上，會採用 ExclusiveUpdate 鎖定。  
  
##  <a name="Security"></a> 安全性  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]備份不會儲存應用裝置上。 因此，您的 IT 團隊必須負責管理備份安全性的各個層面。 比方說，這包括管理備份資料的安全性、 用來儲存備份，伺服器的安全性和連接到備份伺服器的網路基礎結構的安全性[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]應用裝置。  
  
 **管理網路認證**  
  
 備份目錄的網路存取根據標準的 Windows 檔案共用的安全性。 之前執行的備份，您必須建立或指定要用於驗證的 Windows 帳戶[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]備份目錄。 此 windows 帳戶必須擁有存取、 建立和寫入備份目錄的權限。  
  
> [!IMPORTANT]  
>  若要減少資料的安全性風險，建議您指定一個 Windows 帳戶，只為了執行備份和還原作業。 允許此帳戶擁有權限的備份位置和其他無處可去。  
  
 您需要儲存使用者名稱和密碼[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]執行[sp_pdw_add_network_credentials &#40;SQL 資料倉儲 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)預存程序。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]使用 Windows 認證管理員存放區並加密使用者名稱和密碼的控制節點和計算節點上。 認證不會備份資料庫命令一起備份。  
  
 若要移除網路認證從[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，請參閱[sp_pdw_remove_network_credentials &#40;SQL 資料倉儲 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
 若要列出所有的網路認證儲存在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用[sys.dm_pdw_network_credentials &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)動態管理檢視。  
  
## <a name="examples"></a>範例  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. 新增備份位置的網路認證  
 若要建立備份，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]必須擁有備份目錄的讀取/寫入權限。 下列範例會示範如何新增使用者的認證。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]將會儲存這些認證和使用它們來進行備份和還原作業。  
  
> [!IMPORTANT]  
>  基於安全性理由，我們建議您建立僅用於執行備份的一個網域帳戶。  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. 移除備份位置的網路認證  
 下列範例示範如何移除的網域使用者的認證[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. 建立使用者資料庫的完整備份  
 下列範例會建立發票使用者資料庫的完整備份。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]將建立 Invoices2013 目錄，並會將儲存備份檔案，以\\\10.192.63.147\backups\yearly\Invoices2013Full 目錄。  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. 建立使用者資料庫的差異備份  
 下列範例會建立差異備份，其中包括發票資料庫的最後一個完整備份之後所做的所有變更。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]將建立\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff 目錄，它會儲存檔案。 描述 「 發票 2013年差異備份 」 將儲存備份的標頭資訊。  
  
 如果發票的最後一個完整備份已順利完成，才會成功執行差異備份。  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. 建立 master 資料庫的完整備份  
 下列範例會建立在 master 資料庫的完整備份，並將它儲存在目錄 '\\\10.192.63.147\backups\2013\daily\20130722\master'。  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. 建立備份的應用裝置登入資訊。  
 Master 資料庫儲存應用裝置登入資訊。 備份您要備份 master 的登入應用裝置資訊。  
  
 下列範例會建立在 master 資料庫的完整備份。  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>另請參閱  
 [還原資料庫 &#40;平行資料倉儲 &#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  

