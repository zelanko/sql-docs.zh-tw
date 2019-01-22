---
title: 備份與還原-Parallel Data Warehouse |Microsoft Docs
description: 說明資料如何備份及還原的運作方式的 Parallel Data Warehouse (PDW)。 備份和還原作業會用於災害復原。 備份與還原也可用來將資料庫從一個應用裝置複製到另一個應用裝置。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 01/19/2019
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e95415c689fda43c2a9d118713c96d0a1d531904
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2019
ms.locfileid: "54419993"
---
# <a name="backup-and-restore"></a>備份與還原

說明資料如何備份及還原的運作方式的 Parallel Data Warehouse (PDW)。 備份和還原作業會用於災害復原。 備份與還原也可用來將資料庫從一個應用裝置複製到另一個應用裝置。  
    
## <a name="BackupRestoreBasics"></a>備份和還原的基本概念

PDW*資料庫備份*是以格式儲存，這樣就可以使用原始的資料庫還原到設備的設備 」 資料庫的複本。  
  
PDW 資料庫備份會透過[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md) t-sql 陳述式並用於格式化[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)陳述式，就無法使用任何其他用途。 備份只可以還原至應用裝置中，但會使用相同數目或更高的計算節點數目。  
  
<!-- MISSING LINKS
The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  
-->
  
PDW 會使用 SQL Server 備份技術，來備份和還原應用裝置資料庫。 若要使用備份壓縮預先設定 SQL Server 備份的選項。 您無法設定壓縮、總和檢查碼、區塊大小及緩衝區計數等備份選項。  
  
資料庫備份儲存於一或多個備份伺服器的存在您自己的客戶網路中。  PDW 寫入使用者資料庫備份以平行方式直接從計算節點一個備份伺服器，並以平行方式將使用者資料庫備份，直接從備份伺服器還原至計算節點。  
  
備份會在 Windows 檔案系統中，備份的伺服器上儲存為一組檔案。 PDW 資料庫備份只能還原至 PDW。 不過，您也可以使用標準 Windows 檔案備份程序來封存備份伺服器的資料庫備份到另一個位置。 如需有關備份伺服器的詳細資訊，請參閱[取得並設定備份伺服器](acquire-and-configure-backup-server.md)。  
  
## <a name="BackupTypes"></a>資料庫備份類型

有兩種都需要備份的資料類型： 使用者資料庫和系統資料庫 （例如，master 資料庫）。 PDW 不會備份交易記錄檔。  
  
完整資料庫備份是完整的 PDW 資料庫的備份。 這是預設的備份類型。 使用者資料庫的完整備份包含資料庫使用者與資料庫角色。 主要的備份會包含登入。  
  
差異備份中包含的所有變更自上次完整備份。 差異備份所花費的時間通常比完整備份少，因此可以較頻繁地執行。 當多個差異備份根據相同的完整備份時，每個差異會包含的所有變更在先前的差異。  
  
例如，您可以建立完整備份每週和每日差異備份。 若要還原使用者資料庫、 完整備份加上最後一個差異 （如果有的話） 必須還原。  
  
差異備份只有在使用者資料庫上執行。 主要的備份一律是完整備份。  
  
若要備份整個設備，您需要執行的所有使用者資料庫的備份與主要資料庫的備份。  
  
## <a name="BackupProc"></a>資料庫備份程序

下圖顯示資料庫備份期間的資料流。  
  
![PDW 備份程序](media/backup-process.png "PDW 備份程序")  
  
備份程序的運作方式，如下所示：  
  
1.  使用者提交到控制節點的 BACKUP DATABASE tsql 陳述式。  
  
    -   備份是完整或差異備份。  
  
2.  使用者資料庫 （MPP 引擎） 上的 [控制] 節點會建立分散式的查詢計劃來執行平行資料庫備份。  
  
3.  每個節點包含於備份複本要備份的伺服器使用 SQL Server 備份功能其備份檔案。  
  
    -   每個節點會涉及複製一個備份的檔案備份的伺服器。  
  
    -   （完整或差異），才會進行使用者資料庫備份包含備份的資料庫儲存在每個計算節點和備份的資料庫使用者和資料庫角色的一部分。  
  
4.  應用裝置會使用平行的 InfiniBand 網路執行備份。  
  
    -   PDW 以平行方式執行每個完整和差異備份。 不過，多個資料庫備份不會同時執行。 每個備份的要求必須等到先前提交的備份，才能完成。  
  
    -   Master 資料庫的備份只會備份資料從控制節點。 這種備份類型是以序列方式執行。  
  
5.  PDW 資料庫備份是儲存在位於設備之外的目錄中的檔案群組。 目錄名稱指定為網路路徑和目錄名稱。 目錄不能是本機路徑，並不能在應用裝置上。  
  
6.  備份完成之後，您可以使用 Windows 檔案系統備份的目錄複製到另一個位置，如有需要也可以。  
  
    -   備份只能還原至 PDW 應用裝置具有相等或更高的計算節點數目。  
  
    -   您無法變更備份的名稱，然後再執行還原。 備份目錄的名稱必須符合備份的原始名稱的名稱。 備份的原始名稱位於 backup.xml 中檔案的備份目錄。 若要將資料庫還原至不同的名稱，您可以指定 restore 命令中的新名稱。 例如： `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`＞。  
  
## <a name="RestoreModes"></a>資料庫還原模式

完整資料庫還原重新建立 PDW 資料庫使用中的資料庫備份的資料。 先還原完整備份，並選擇性地還原一個差異備份執行資料庫還原。 資料庫還原包括資料庫使用者和資料庫角色。  
  
標頭只還原會傳回資料庫的標頭資訊。 它不會還原到設備的資料。  
  
應用裝置還原為整個應用裝置還原。 這包括還原所有使用者資料庫和 master 資料庫。  
  
## <a name="RestoreProc"></a>還原程序

下圖顯示在資料庫還原期間的資料流。  
  
![還原程序](media/restore-process.png "還原程序")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>還原至具有相同數目的計算節點 * * 的應用裝置  
  
還原資料時，設備會偵測來源應用裝置和目的地應用裝置上的計算節點數目。 如果這兩個應用裝置有相同數目的計算節點，在還原程序的運作方式如下：  
  
1.  使用非應用裝置的備份伺服器上的 Windows 檔案共用上要還原的資料庫備份。 為了達到最佳效能，此伺服器被連線到設備的 InfiniBand 網路。  
  
2.  使用者提交[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)向控制節點的 tsql 陳述式。  
  
    -   完整還原或標頭還原的還原。 完整還原還原完整備份，並選擇性地還原差異備份。  
  
3.  控制節點 （MPP 引擎） 建立的分散式的查詢計劃，才能執行平行資料庫還原。  
  
    -   SQL ServerPDW 以平行方式執行資料庫還原的使用者。 不過，多個資料庫的備份及還原為未同時執行。 MPP 引擎會將放入佇列，每個 restore 陳述式它必須等待先前提交的備份和還原完成的要求。  
  
    -   Master 資料庫的還原作業只會將資料還原到 [控制] 節點中;循序執行還原。  
  
    -   標頭資訊的還原是快速的作業，而且不會還原到計算或控制節點的任何資料。 相反地，控制節點會傳回結果做為查詢輸出。  
  
4.  備份檔案複製到正確的計算節點，以平行方式，通常透過設備 InfiniBand 網路。  
  
5.  每個計算節點還原它的使用者資料庫的部分。 如果還原的任何未完成成功，所有資料庫中移除，並還原未順利完成。  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>還原至具有大量的計算節點的應用裝置  
  
將備份還原至具有較多計算節點的應用裝置時，會讓已配置的資料庫大小依計算節點數目比例成長。  
  
比方說，60 GB 資料庫從還原的 2 個節點的應用裝置 (每個節點 30 GB) 到 6 個節點的設備，SQL Server PDW 就會建立一個 180 GB 資料庫 (6 個節點 30 gb 每個節點） 上 6 個節點的設備。 SQL Server PDW 一開始會將資料庫還原至 2 個節點，以符合來源組態，並再轉散發到所有的 6 節點資料。  
  
轉散發之後, 每個計算節點會包含較少的實際資料以及更多可用空間較小的來源應用裝置上的每個計算節點。 請使用額外的空間將更多資料新增至資料庫。 如果還原的資料庫大小大於您需要您可以使用[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)壓縮資料庫檔案大小。  
  
## <a name="related-tasks"></a>相關工作  
  
|備份和還原工作|描述|  
|---------------------------|---------------|  
|準備伺服器，做為備份伺服器。|[取得並設定備份的伺服器 ](acquire-and-configure-backup-server.md)|  
|備份資料庫。|[備份資料庫](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|將資料庫還原。|[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    

<!-- MISSING LINKS
|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  
-->
