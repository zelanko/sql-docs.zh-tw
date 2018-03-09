---
title: "備份與還原"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "說明資料如何備份和還原運作的 SQL Server Parallel Data Warehouse (PDW)。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: d4669957-270a-4e50-baf3-14324ca63049
caps.latest.revision: 
ms.openlocfilehash: 06863b600ed62d795db82aa5aa3ae5c88578833a
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="backup-and-restore"></a>備份與還原
說明資料如何備份和還原運作的 SQL Server Parallel Data Warehouse (PDW)。 備份和還原作業可用於災害復原。 備份與還原也可用來將資料庫從一個工具複製到另一部應用裝置。  
    
## <a name="BackupRestoreBasics"></a>備份和還原的基本概念  
PDW*資料庫備份*應用裝置資料庫，使其可以用於將原始的資料庫還原至應用裝置的格式儲存的複本。  
  
PDW 資料庫備份會透過[備份資料庫](../t-sql/statements/backup-database-parallel-data-warehouse.md)t-sql 陳述式且用於格式化[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)陳述式，就無法使用用於其他用途。 以相同的數字或更多計算節點只能至應用裝置還原備份。  
  
<!-- MISSING LINKS

The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  

-->
  
PDW 備份與還原應用裝置資料庫使用 SQL Server 備份技術。 若要使用備份壓縮預先設定 SQL Server 備份選項。 您無法設定備份的選項，例如壓縮、 總和檢查碼、 區塊大小和緩衝區計數。  
  
資料庫備份會儲存一或多個備份伺服器上，這存在於客戶網路。  PDW 寫入使用者資料庫備份以平行方式直接來自計算節點一個備份伺服器，並直接從伺服器備份還原使用者資料庫備份，以平行方式，用於運算節點。  
  
在 Windows 檔案系統備份會備份伺服器上儲存為一組檔案。 只能與 PDW 還原 PDW 資料庫備份。 不過，您可以使用標準 Windows 檔案備份程序封存備份的伺服器上資料庫備份至另一個位置。 如需備份伺服器的詳細資訊，請參閱[取得及設定伺服器備份](acquire-and-configure-backup-server.md)。  
  
## <a name="BackupTypes"></a>資料庫備份類型  
有兩種需要備份的資料類型： 使用者資料庫和系統資料庫 （例如，master 資料庫）。 PDW 不會備份交易記錄檔。  
  
完整資料庫備份是整個 PDW 資料庫的備份。 這是預設的備份類型。 使用者資料庫的完整備份包含資料庫使用者與資料庫角色。 備份 master 包含登入。  
  
差異備份中包含的所有變更上次完整備份。 差異備份通常會比完整備份的時間，並且可以更頻繁地執行。 當多個差異備份根據相同的完整備份時，每個差異會包含的所有變更在先前的差異。  
  
例如，您可以建立每週完整備份和每日差異備份。 若要還原使用者資料庫，完整備份和最後一個差異 （如果有的話） 必須還原。  
  
差異備份只支援使用者資料庫。 備份 master 一律是完整備份。  
  
若要備份整個應用裝置，您需要執行的所有使用者資料庫的備份與主要資料庫的備份。  
  
## <a name="BackupProc"></a>資料庫備份程序  
下圖顯示資料流程中的資料庫備份期間。  
  
![PDW 備份程序](media/backup-process.png "PDW 備份程序")  
  
備份程序的運作方式，如下所示：  
  
1.  使用者提交 BACKUP DATABASE tsql 陳述式的控制節點。  
  
    -   此備份是完整或差異備份。  
  
2.  使用者資料庫的控制節點 （MPP 引擎） 建立的分散式的查詢計劃，以執行平行資料庫備份。  
  
3.  備份的複本中涉及的每個節點其備份的檔案備份的伺服器使用 SQL Server 備份功能。  
  
    -   每個節點涉及複製一個備份的檔案備份的伺服器。  
  
    -   （完整或差異） 的使用者資料庫備份包含備份的資料庫儲存在每個計算節點及備份的資料庫使用者與資料庫角色的一部分。  
  
4.  應用裝置會平行使用 InfiniBand 網路中執行備份。  
  
    -   PDW 以平行方式執行的每個完整和差異備份。 不過，多個資料庫備份需要不同時執行。 每個備份的要求必須等候先前提出的備份，才能完成。  
  
    -   Master 資料庫的備份只會備份資料從控制項節點。 這種備份類型是以序列方式執行。  
  
5.  PDW 資料庫備份，則關閉設備所在的目錄中儲存的檔案群組。 目錄名稱指定為網路路徑和目錄名稱。 目錄不可是本機路徑，而且不得應用裝置上。  
  
6.  備份完成之後，您可以使用 Windows 檔案系統備份目錄複製到其他位置，如有需要也可以。  
  
    -   備份只能還原至 PDW 應用裝置具有等於或大於的運算節點數目。  
  
    -   您無法變更之備份的名稱，然後再執行還原。 備份目錄的名稱必須符合之備份的原始名稱的名稱。 備份的原始名稱位於 backup.xml 中的檔案備份的目錄。 若要將資料庫還原至不同的名稱，您可以在 restore 命令中指定新名稱。 例如：`RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`。  
  
## <a name="RestoreModes"></a>資料庫還原模式  
還原完整的資料庫重新建立 PDW 資料庫所使用的資料庫備份中的資料。 藉由先還原完整備份，然後選擇性地還原差異備份被執行資料庫還原。 資料庫還原包括資料庫使用者與資料庫角色。  
  
標頭只還原傳回資料庫的標頭資訊。 它不會還原至應用裝置的資料。  
  
應用裝置還原為整個應用裝置還原。 這包括還原所有使用者資料庫和 master 資料庫。  
  
## <a name="RestoreProc"></a>還原程序  
下圖顯示資料流程中的資料庫還原期間。  
  
![還原程序](media/restore-process.png "還原程序")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>還原至具有相同數目的計算節點 * * 應用裝置  
  
還原資料時，應用裝置會偵測來源應用裝置和目的地應用裝置上的運算節點數目。 如果這兩個裝置中有相同數目的計算節點，在還原程序的運作方式，如下所示：  
  
1.  使用非應用裝置的備份伺服器上的 Windows 檔案共用上要還原的資料庫備份。 為了達到最佳效能，此伺服器通常連接至應用裝置 InfiniBand 網路。  
  
2.  使用者送出[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md) tsql 陳述式的控制節點。  
  
    -   完整還原或標頭還原的還原。 完整還原還原完整備份，並選擇性地還原差異備份。  
  
3.  控制節點 （MPP 引擎） 建立的分散式的查詢計劃，以執行資料庫還原。  
  
    -   SQL ServerPDW 以平行方式執行使用者資料庫的還原。 不過，多個資料庫的備份和還原會同時執行記憶體。 MPP 引擎將放入佇列中; 每個 restore 陳述式必須等候先前提出的備份和還原完成要求。  
  
    -   Master 資料庫的還原作業只會將資料還原到 [控制] 節點中。循序執行還原。  
  
    -   標頭資訊的還原是快速的作業，而且不會還原到 Compute 或控制節點的任何資料。 相反地，[控制] 節點會傳回結果做為查詢輸出。  
  
4.  備份檔案複製到正確的運算節點，以平行方式，通常透過設備 InfiniBand 網路。  
  
5.  每個計算節點還原它的使用者資料庫的部分。 如果還原的任何未完成成功，所有的資料庫移除，還原未順利完成。  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>還原至具有較大數目的運算節點應用裝置  
  
將備份還原到具有較大數目的運算節點的應用裝置會逐漸增加配置的資料庫大小成比例的運算節點數目。  
  
例如，從 2 節點應用裝置 (30 GB，每個節點) 的 60 GB 資料庫還原至 6 節點應用裝置中，SQL Server PDW 就會建立 180 GB 資料庫 （6 節點具有 30 GB 每個節點） 6 節點應用裝置上。 SQL Server PDW 一開始將資料庫還原到比對來源的設定，2 個節點，然後轉散發到所有的 6 節點資料。  
  
轉散發之後每個計算節點會包含實際的資料比較少，較小的來源應用裝置上每個計算節點的更多可用空間。 若要將更多資料加入至資料庫中使用額外的空間。 如果還原的資料庫大小大於您需要您可以使用[ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md)壓縮資料庫檔案大小。  
  
## <a name="related-tasks"></a>相關工作  
  
|備份和還原工作|Description|  
|---------------------------|---------------|  
|準備的伺服器做為備份伺服器。|[取得和設定備份伺服器 ](acquire-and-configure-backup-server.md)|  
|備份資料庫。|[備份資料庫](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|將資料庫還原。|[還原資料庫](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    
<!-- MISSING LINKS
|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  
-->
