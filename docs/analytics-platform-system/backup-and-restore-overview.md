---
title: 備份與還原
description: 說明如何針對平行處理資料倉儲（PDW）進行資料備份和還原。 備份和還原作業會用於嚴重損壞修復。 備份和還原也可以用來將資料庫從一個應用裝置複製到另一個應用裝置。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 01/19/2019
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 75399480879623a39da542c68f036389c645f6ab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401353"
---
# <a name="backup-and-restore"></a>備份與還原

說明如何針對平行處理資料倉儲（PDW）進行資料備份和還原。 備份和還原作業會用於嚴重損壞修復。 備份和還原也可以用來將資料庫從一個應用裝置複製到另一個應用裝置。  
    
## <a name="backup-and-restore-basics"></a><a name="BackupRestoreBasics"></a>備份與還原的基本概念

PDW*資料庫備份*是設備資料庫的複本，以格式儲存，讓它可以用來將原始資料庫還原至應用裝置。  
  
建立 PDW 資料庫備份時，會使用[BACKUP database](../t-sql/statements/backup-database-parallel-data-warehouse.md) t-sql 語句，並將其格式化以用於[RESTORE database](../t-sql/statements/restore-database-parallel-data-warehouse.md)語句;它無法用於任何其他用途。 備份只能還原至具有相同數目或更多計算節點的設備。  
  
<!-- MISSING LINKS
The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  
-->
  
PDW 使用 SQL Server 備份技術來備份和還原設備資料庫。 SQL Server 備份選項已預先設定為使用備份壓縮。 您無法設定壓縮、總和檢查碼、區塊大小及緩衝區計數等備份選項。  
  
資料庫備份會儲存在一或多個備份伺服器上，並存在於您自己的客戶網路中。  PDW 會以平行方式將使用者資料庫備份直接從計算節點寫入一部備份伺服器，並將使用者資料庫備份從備份伺服器直接還原至計算節點。  
  
備份會儲存在備份伺服器上，做為 Windows 檔案系統中的一組檔案。 PDW 資料庫備份只能還原至 PDW。 不過，您可以使用標準的 Windows 檔案備份程式，將資料庫備份從備份伺服器封存到另一個位置。 如需備份伺服器的詳細資訊，請參閱[取得和設定備份伺服器](acquire-and-configure-backup-server.md)。  
  
## <a name="database-backup-types"></a><a name="BackupTypes"></a>資料庫備份類型

有兩種類型的資料需要備份：使用者資料庫和系統資料庫（例如 master 資料庫）。 PDW 不會備份交易記錄。  
  
完整資料庫備份是整個 PDW 資料庫的備份。 這是預設的備份類型。 使用者資料庫的完整備份包含資料庫使用者和資料庫角色。 Master 的備份包含登入。  
  
差異備份包含上一次完整備份之後的所有變更。 差異備份所花費的時間通常比完整備份少，因此可以較頻繁地執行。 當多個差異備份是以相同的完整備份為基礎時，每個差異都會包含先前差異中的所有變更。  
  
例如，您可以每天建立一次完整備份和差異備份。 若要還原使用者資料庫，需要還原完整備份加上最後一個差異（如果有的話）。  
  
只有使用者資料庫才支援差異備份。 Master 的備份一律是完整備份。  
  
若要備份整個應用裝置，您必須執行所有使用者資料庫的備份，以及 master 資料庫的備份。  
  
## <a name="database-backup-process"></a><a name="BackupProc"></a>資料庫備份進程

下圖顯示資料庫備份期間的資料流程。  
  
![PDW 備份程式](media/backup-process.png "PDW 備份程式")  
  
備份程式的運作方式如下：  
  
1.  使用者將備份資料庫 tsql 語句提交至控制節點。  
  
    -   備份可能是完整或差異備份。  
  
2.  對於使用者資料庫，控制節點（MPP 引擎）會建立分散式查詢計畫來執行平行資料庫備份。  
  
3.  包含在備份中的每個節點都會使用 SQL Server 備份功能，將其備份檔案複製到備份伺服器。  
  
    -   每個涉及的節點都會將一個備份檔案複製到備份伺服器。  
  
    -   使用者資料庫備份（完整或差異）包含儲存在每個計算節點上之資料庫部分的備份，以及資料庫使用者和資料庫角色的備份。  
  
4.  設備會使用不限的網路來平行執行備份。  
  
    -   PDW 會平行執行每個完整和差異備份。 不過，多個資料庫備份不會同時執行。 每個備份要求都必須等候先前提交的備份完成。  
  
    -   Master 資料庫的備份只會從控制節點備份資料。 此備份類型會以序列循序執行。  
  
5.  PDW 資料庫備份是儲存在位於設備外之目錄中的一組檔案。 目錄名稱會指定為網路路徑和目錄名稱。 此目錄不能是本機路徑，也不能在設備上。  
  
6.  備份完成之後，您可以使用 Windows 檔案系統，視需要將備份目錄複寫到另一個位置。  
  
    -   備份只能還原至具有相同或更多計算節點數目的 PDW 應用裝置。  
  
    -   您不能在執行還原之前變更備份的名稱。 備份目錄的名稱必須符合備份原始名稱的名稱。 備份的原始名稱位於備份目錄內的備份 .xml 檔案中。 若要將資料庫還原成不同的名稱，您可以在 restore 命令中指定新的名稱。 例如： `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ` 。  
  
## <a name="database-restore-modes"></a><a name="RestoreModes"></a>資料庫還原模式

完整資料庫還原會使用資料庫備份中的資料重新建立 PDW 資料庫。 資料庫還原的執行方式是先還原完整備份，然後選擇性地還原一個差異備份。 資料庫還原包含資料庫使用者和資料庫角色。  
  
僅標頭還原會傳回資料庫的標頭資訊。 它不會將資料還原到設備。  
  
「設備還原」是整個應用裝置的還原。 這包括還原所有的使用者資料庫和 master 資料庫。  
  
## <a name="restore-process"></a><a name="RestoreProc"></a>還原程式

下圖顯示資料庫還原期間的資料流程。  
  
![還原程序](media/restore-process.png "還原程序")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>還原至具有相同計算節點數目的設備 * *  
  
還原資料時，設備會偵測來源應用裝置和目的地應用裝置上的計算節點數目。 如果這兩個設備的計算節點數目相等，還原程式的運作方式如下所示：  
  
1.  要還原的資料庫備份可在非設備備份伺服器上的 Windows 檔案共用上取得。 為了達到最佳效能，此伺服器會連線到設備不會的網路。  
  
2.  使用者將[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md) tsql 語句提交至控制節點。  
  
    -   還原可能是完整還原或標頭還原。 完整還原會還原完整備份，然後選擇性地還原差異備份。  
  
3.  控制節點（MPP 引擎）會建立分散式查詢計畫，以執行平行資料庫還原。  
  
    -   SQL ServerPDW 會以平行方式執行使用者資料庫的還原。 不過，多個資料庫備份和還原不會同時執行。 MPP 引擎會將每個 restore 語句放入佇列中;它必須等候先前提交的備份和還原要求完成。  
  
    -   Master 資料庫的還原只會將資料還原至控制節點;還原會以序列循序執行。  
  
    -   還原標頭資訊是一項快速作業，不會將任何資料還原至計算或控制節點。 相反地，控制節點會以查詢輸出的形式傳回結果。  
  
4.  備份檔案會以平行方式複製到正確的計算節點，通常是透過設備不會的網路。  
  
5.  每個計算節點都會還原其使用者資料庫的部分。 如果有任何還原未成功完成，則會移除所有的資料庫，而且還原作業會失敗。  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>還原至具有較多計算節點的設備  
  
將備份還原至具有較多計算節點的應用裝置時，會讓已配置的資料庫大小依計算節點數目比例成長。  
  
例如，將 60 GB 的資料庫從2個節點的應用裝置（每個節點 30 GB）還原至6個節點的應用裝置時，SQL Server PDW 會在6個節點的應用裝置上建立 180 GB 的資料庫（每個節點 30 GB 的節點）。 SQL Server PDW 一開始會將資料庫還原至2個節點，以符合來源設定，然後將資料重新散發至所有6個節點。  
  
在重新發佈之後，每個計算節點所包含的實際資料和更多的可用空間，會比較小來源應用裝置上的每個計算節點少。 請使用額外的空間將更多資料新增至資料庫。 如果還原的資料庫大小大於您的需求，您可以使用[ALTER database](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)來壓縮資料庫檔案大小。  
  
## <a name="related-tasks"></a>相關工作  
  
|備份與還原工作|描述|  
|---------------------------|---------------|  
|準備伺服器做為備份伺服器。|[取得並設定備份伺服器](acquire-and-configure-backup-server.md)|  
|備份資料庫。|[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|還原資料庫。|[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    

<!-- MISSING LINKS

|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  

-->
