---
title: "還原資料庫 (Parallel Data Warehouse) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4cd72d13f4c953f9b15963655d437709bfc71fa7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="restore-database-parallel-data-warehouse"></a>還原資料庫 (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  還原[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]使用者資料庫從資料庫備份至[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]應用裝置。 從先前所建立的備份還原資料庫[!INCLUDE[ssPDW](../../includes/sspdw-md.md)][備份資料庫 &#40;平行資料倉儲 &#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)命令。 使用備份和還原作業來建立災害復原方案，或將資料庫從一個裝置移到另一個。  
  
> [!NOTE]  
>  還原 master 包含還原應用裝置登入資訊。 若要還原 master，請使用[還原 master 資料庫 &#40;TRANSACT-SQL &#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)頁面**Configuration Manager**工具。 具有存取權的控制節點的系統管理員才能執行此作業。  
  
 如需有關[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]資料庫備份，請參閱 「 備份和還原 」 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 指定使用者資料庫還原到資料庫，呼叫*database_name*。 已還原的資料庫可以有不同的名稱與來源資料庫備份。 *database_name*不能已存在於目的地應用裝置上的資料庫。 如需詳細資訊允許資料庫名稱，請參閱 < 物件命名規則 > 中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 還原使用者資料庫會還原完整資料庫備份，然後再應用裝置選擇性地還原差異備份。 使用者資料庫還原包括還原資料庫使用者與資料庫角色。  
  
 FROM DISK = '\\\\*UNC_path*\\*backup_directory*'  
 網路路徑及從中目錄[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]將還原的備份檔案。 例如，FROM DISK = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'。  
  
 *backup_directory*  
 指定包含完整或差異備份的目錄名稱。 例如，您可以執行完整或差異備份的 RESTORE HEADERONLY 運算。  
  
 *full_backup_directory*  
 指定包含完整備份的目錄名稱。  
  
 *differential_backup_directory*  
 指定包含差異備份的目錄名稱。  
  
-   路徑] 和 [備份目錄必須存在，而且必須指定為完整的通用命名慣例 (UNC) 路徑。  
  
-   備份目錄的路徑不能是本機路徑，它不能是任何位置[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]應用裝置節點。  
  
-   備份目錄名稱與 UNC 路徑的最大長度為 200 個字元。  
  
-   必須指定伺服器或主機，IP 位址。  
  
 RESTORE HEADERONLY  
 指定要傳回只有一個使用者資料庫備份的標頭資訊。 欄位標頭包含備份的備份名稱的文字描述。 備份名稱不需要儲存備份檔案的目錄名稱相同。  
  
 RESTORE HEADERONLY 的結果會模仿[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]RESTORE HEADERONLY 的結果。 結果將會有超過 50 個資料行，並非所有供[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 如需中的資料行的描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]RESTORE HEADERONLY 的結果，請參閱[RESTORE HEADERONLY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要**CREATE ANY DATABASE**權限。  
  
 需要 Windows 帳戶具有存取和讀取從備份目錄的權限。 您也必須儲存的 Windows 帳戶名稱和密碼[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
1.  若要確認憑證已經存在，請使用[sys.dm_pdw_network_credentials &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
2.  若要新增或更新的認證，請使用[sp_pdw_add_network_credentials &#40;SQL 資料倉儲 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
3.  若要移除認證從[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用[sp_pdw_remove_network_credentials &#40;SQL 資料倉儲 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
## <a name="error-handling"></a>錯誤處理  
 RESTORE DATABASE 命令會產生錯誤，在下列情況下：  
  
-   已還原資料庫的名稱存在於目標裝置上。 若要避免這個問題，選擇唯一的資料庫名稱，或卸除現有資料庫，然後再執行還原。  
  
-   沒有備份目錄中的檔案備份組無效。  
  
-   登入權限還不夠來還原資料庫。  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]沒有正確的權限的備份檔案的所在位置的網路位置。  
  
-   備份目錄的網路位置不存在，或無法使用。  
  
-   沒有足夠的磁碟空間的計算節點上控制節點。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]不會確認足夠的磁碟空間存在應用裝置上啟動還原之前。 因此，就能夠在執行 RESTORE DATABASE 陳述式時產生出的磁碟空間時發生錯誤。 磁碟空間不足時，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]回復還原。  
  
-   還原資料庫的目標裝置具有比從備份資料庫的來源應用裝置的計算節點較少。  
  
-   資料庫還原會嘗試從，在交易內。  
  
## <a name="general-remarks"></a>一般備註  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]追蹤資料庫還原的成功。 還原差異資料庫備份之前先[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]確認已順利完成完整資料庫還原。  
  
 還原之後，使用者資料庫會具有資料庫相容性層級 120。 這是不論其原始的相容性層級的所有資料庫，則為 true。  
  
 **還原至具有較大數目的運算節點應用裝置**  
執行[DBCC SHRINKLOG （Azure SQL 資料倉儲）](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)之後從較大到小工具還原資料庫，因為重新發佈將會增加交易記錄檔。  

將備份還原到具有較大數目的運算節點的應用裝置會逐漸增加配置的資料庫大小成比例的運算節點數目。  
  
例如，還原 60 GB 資料庫時從 2 節點應用裝置 (30 GB，每個節點) 至 6 節點應用裝置， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 6 節點應用裝置上建立 180 GB 資料庫 （6 節點具有 30 GB 每個節點）。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]一開始將資料庫還原到比對來源的設定，2 個節點，然後轉散發到所有的 6 節點資料。  
  
 轉散發之後每個計算節點會包含實際的資料比較少，較小的來源應用裝置上每個計算節點的更多可用空間。 若要將更多資料加入至資料庫中使用額外的空間。 如果還原的資料庫大小大於您需要您可以使用[ALTER DATABASE &#40;平行資料倉儲 &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)壓縮資料庫檔案大小。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 關於這些限制和限制，來源應用裝置會是建立資料庫備份，與目標應用裝置是資料庫將還原應用裝置的應用裝置。  
  
 還原資料庫，不會自動重建統計資料。  
  
 只有一個 RESTORE DATABASE 或 BACKUP DATABASE 陳述式可以在任何給定時間的應用裝置上執行。 應用裝置同時提交多個備份和還原陳述式，如果將它們放入佇列，其中一個處理一次。  
  
 您只能還原資料庫備份來[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]目標的應用裝置，具有相同數目或更多的運算節點比來源應用裝置。 目標裝置不能有比來源應用裝置的計算節點較少。  
  
 您無法還原已建立具有 SQL Server 2012 PDW 應用裝置具有 SQL Server 2008 R2 的硬體硬體應用裝置的備份。 如此即使原本購買 SQL Server 2008 R2 PDW 硬體應用裝置，並且現在正在執行 SQL Server 2012 PDW 軟體。  
  
## <a name="locking"></a>鎖定  
 資料庫物件上採用獨佔鎖定。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-restore-examples"></a>A. 簡單的 RESTORE 範例  
 下列範例會還原完整備份，以便`SalesInvoices2013`資料庫。 備份檔案儲存在\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full 目錄。 SalesInvoices2013 資料庫不能已存在於目標應用裝置或此命令將會失敗，發生錯誤。  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>B. 還原完整和差異備份  
 下列範例會還原完整的然後差異備份到 SalesInvoices2013 資料庫  
  
 從儲存在完整備份還原完整資料庫備份 '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full' 目錄。 如果順利完成還原，差異備份還原到 SalesInvoices2013 資料庫。  差異備份會儲存在 '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff' 目錄。  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. 還原備份標頭  
 這個範例會還原資料庫備份的標頭資訊 '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'。 命令會產生一個資料列的 Invoices2013Full 備份的資訊。  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 若要檢查的備份時，內容，或請確定目標還原應用裝置，與來源備份裝置相容，再嘗試還原備份，您可以使用的標頭資訊。  
  
## <a name="see-also"></a>請參閱＜  
 [備份資料庫 &#40;平行資料倉儲 &#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  
