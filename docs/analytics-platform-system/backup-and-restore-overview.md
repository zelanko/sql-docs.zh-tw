---
title: 備份與還原
description: 說明如何將資料備份和還原用於平行處理資料倉儲 (PDW) 。 備份和還原作業是用於嚴重損壞修復。 您也可以使用備份和還原，將資料庫從一個應用裝置複製到另一個應用裝置。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 01/19/2019
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9dd52db9d34519f2b09cbaba880806c17509c84c
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489708"
---
# <a name="backup-and-restore"></a>備份與還原

說明如何將資料備份和還原用於平行處理資料倉儲 (PDW) 。 備份和還原作業是用於嚴重損壞修復。 您也可以使用備份和還原，將資料庫從一個應用裝置複製到另一個應用裝置。  
    
## <a name="backup-and-restore-basics"></a><a name="BackupRestoreBasics"></a>備份與還原的基本概念

PDW *資料庫備份* 是以格式儲存的設備資料庫複本，可用來將原始資料庫還原至設備。  
  
您可以使用 [BACKUP database](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016&preserve-view=true) t-sql 語句來建立 PDW 資料庫備份，並格式化以搭配 [RESTORE database](../t-sql/statements/restore-statements-transact-sql.md?view=aps-pdw-2016&preserve-view=true) 語句使用;它無法用於任何其他用途。 備份只能還原至具有相同數目或更多計算節點數目的設備。  
  
<!-- MISSING LINKS
The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  
-->
  
PDW 使用 SQL Server 備份技術來備份及還原設備資料庫。 SQL Server 備份選項已預先設定為使用備份壓縮。 您無法設定壓縮、總和檢查碼、區塊大小及緩衝區計數等備份選項。  
  
資料庫備份會儲存在您自己的客戶網路中的一或多個備份伺服器上。  PDW 會以平行方式將使用者資料庫備份直接從計算節點寫入至一部備份伺服器，並將使用者資料庫備份從備份伺服器直接還原至計算節點。  
  
備份會以 Windows 檔案系統中的一組檔案的形式儲存在備份伺服器上。 PDW 資料庫備份只能還原到 PDW。 不過，您可以使用標準 Windows 檔案備份程式，將資料庫備份從備份伺服器封存到另一個位置。 如需有關備份伺服器的詳細資訊，請參閱 [取得和設定備份伺服器](acquire-and-configure-backup-server.md)。  
  
## <a name="database-backup-types"></a><a name="BackupTypes"></a>資料庫備份類型

有兩種類型的資料需要備份：使用者資料庫和系統資料庫 (例如 master 資料庫) 。 PDW 不會備份交易記錄。  
  
完整的資料庫備份是整個 PDW 資料庫的備份。 這是預設的備份類型。 使用者資料庫的完整備份包括資料庫使用者和資料庫角色。 Master 的備份包含登入。  
  
差異備份包含上次完整備份之後所做的所有變更。 差異備份所花費的時間通常比完整備份少，因此可以較頻繁地執行。 當多個差異備份是以相同的完整備份為基礎時，每個差異都會包含先前差異中的所有變更。  
  
例如，您可以每週建立完整備份和差異備份。 若要還原使用者資料庫，完整備份加上最後一個差異 (如果存在，則) 需要還原。  
  
只有使用者資料庫支援差異備份。 Master 的備份一律是完整備份。  
  
若要備份整個設備，您必須執行所有使用者資料庫的備份和 master 資料庫的備份。  
  
## <a name="database-backup-process"></a><a name="BackupProc"></a>資料庫備份進程

下圖顯示資料庫備份期間的資料流程。  
  
![PDW 備份進程](media/backup-process.png "PDW 備份進程")  
  
備份程式的運作方式如下：  
  
1.  使用者將 BACKUP DATABASE tsql 語句提交至控制項節點。  
  
    -   備份可以是完整備份或差異備份。  
  
2.  針對使用者資料庫， (MPP 引擎的控制項節點) 會建立分散式查詢計畫來執行平行資料庫備份。  
  
3.  備份中包含的每個節點都會使用 SQL Server 備份功能，將其備份檔案複製到備份伺服器。  
  
    -   相關的每個節點都會將一個備份檔案複製到備份伺服器。  
  
    -    (full 或差異) 的使用者資料庫備份包含每個計算節點上儲存的資料庫部份備份，以及資料庫使用者和資料庫角色的備份。  
  
4.  設備會使用未使用的網路，以平行方式來執行備份。  
  
    -   PDW 會平行執行每個完整和差異備份。 但是，不會同時執行多個資料庫備份。 每個備份要求都必須等待先前提交的備份完成。  
  
    -   Master 資料庫的備份只會備份來自 Control 節點的資料。 這種備份類型是依循序執行。  
  
5.  PDW 資料庫備份是儲存在應用裝置的目錄中的一組檔案。 目錄名稱會指定為網路路徑和目錄名稱。 目錄不可以是本機路徑，也不能在設備上。  
  
6.  備份完成後，您可以使用 Windows 檔案系統將備份目錄複寫到另一個位置（如有需要）。  
  
    -   備份只能還原至有相等或更多計算節點數目的 PDW 設備。  
  
    -   您無法在執行還原之前變更備份的名稱。 備份目錄的名稱必須與備份的原始名稱名稱相符。 備份的原始名稱位於備份目錄內的 backup.xml 檔案中。 若要將資料庫還原為不同的名稱，您可以在 restore 命令中指定新名稱。 例如： `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ` 。  
  
## <a name="database-restore-modes"></a><a name="RestoreModes"></a>資料庫還原模式

完整資料庫還原會使用資料庫備份中的資料重新建立 PDW 資料庫。 資料庫還原的執行方式是先還原完整備份，然後選擇性地還原一個差異備份。 資料庫還原包含資料庫使用者和資料庫角色。  
  
只有標頭的還原會傳回資料庫的標頭資訊。 它不會將資料還原至設備。  
  
設備還原是整個設備的還原。 這包括還原所有使用者資料庫和 master 資料庫。  
  
## <a name="restore-process"></a><a name="RestoreProc"></a>還原程序

下圖顯示資料庫還原期間的資料流程。  
  
![還原流程](media/restore-process.png "還原程序")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>還原至具有相同計算節點數目的設備 * *  
  
還原資料時，設備會偵測來源設備和目的地設備上的計算節點數目。 如果這兩個設備都有相等的計算節點數目，則還原程式的運作方式如下：  
  
1.  您可以在非設備備份伺服器上的 Windows 檔案共用上，取得要還原的資料庫備份。 為了達到最佳效能，此伺服器會連線到設備未經過網路。  
  
2.  使用者將 [RESTORE DATABASE](../t-sql/statements/restore-statements-transact-sql.md?view=aps-pdw-2016&preserve-view=true) tsql 語句提交至控制項節點。  
  
    -   還原可能是完整還原或標頭還原。 完整還原會還原完整備份，然後選擇性地還原差異備份。  
  
3.   (MPP 引擎的控制項節點) 會建立分散式查詢計畫來執行平行資料庫還原。  
  
    -   SQL ServerPDW 會以平行方式執行使用者資料庫的還原。 但是，不會同時執行多個資料庫備份和還原。 MPP 引擎會將每個 restore 語句放入佇列中;它必須等候先前提交的備份和還原要求完成。  
  
    -   Master 資料庫的還原只會將資料還原至控制項節點。還原會以序列方式執行。  
  
    -   還原標頭資訊是一項快速作業，並不會將任何資料還原至計算或控制節點。 相反地，控制節點會以查詢輸出的形式傳回結果。  
  
4.  備份檔案會以平行方式複製到正確的計算節點，通常是透過設備未經過網路。  
  
5.  每個計算節點會還原其使用者資料庫的部分。 如果有任何還原無法順利完成，就會移除所有的資料庫，而且還原作業無法順利完成。  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>還原至具有較多計算節點的設備  
  
將備份還原至具有較多計算節點的應用裝置時，會讓已配置的資料庫大小依計算節點數目比例成長。  
  
例如，從2個節點的應用裝置還原 60 GB 資料庫時 (每個節點 30 GB) 到6個節點的應用裝置時，SQL Server PDW 會在6個節點的應用裝置上建立 180 GB 的資料庫 (6 個節點，每個節點) 為 30 GB。 SQL Server PDW 一開始會將資料庫還原到2個節點以符合來源設定，然後將資料重新發佈至所有6個節點。  
  
在轉散發之後，每個計算節點會包含較小來源設備上每個計算節點的實際資料和更多可用空間。 請使用額外的空間將更多資料新增至資料庫。 如果還原的資料庫大小超過您需要的大小，您可以使用 [ALTER database](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) 來壓縮資料庫檔案大小。  
  
## <a name="related-tasks"></a>相關工作  
  
|備份與還原工作|描述|  
|---------------------------|---------------|  
|準備伺服器做為備份伺服器。|[取得並設定備份伺服器](acquire-and-configure-backup-server.md)|  
|備份資料庫。|[BACKUP DATABASE](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016&preserve-view=true)|  
|還原資料庫。|[還原資料庫](../t-sql/statements/restore-statements-transact-sql.md?view=aps-pdw-2016&preserve-view=true)|    

<!-- MISSING LINKS

|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  

-->
