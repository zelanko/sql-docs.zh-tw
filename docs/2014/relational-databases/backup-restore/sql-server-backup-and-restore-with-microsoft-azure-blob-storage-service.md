---
title: SQL Server 備份及還原與 Windows Azure Blob 儲存體服務 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
caps.latest.revision: 28
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38e20e433b7fed2e34750c300ee7e1489d6df665
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193548"
---
# <a name="sql-server-backup-and-restore-with-windows-azure-blob-storage-service"></a>SQL Server 備份及還原與 Windows Azure Blob 儲存體服務
  本主題將介紹[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]備份，以及從中還原[Windows Azure Blob 儲存體服務](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)。 本主題也會提供使用 Windows Azure Blob 服務來儲存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份的優點摘要。  
  
 SQL Server 可以下列方式將備份儲存到 Windows Azure BLOB 儲存服務：  
  
-   **管理 Windows Azure 的備份：** 使用相同的方法，用來備份到磁碟和磁帶，您現在即可備份至 Windows Azure 儲存體所指定 URL 做為備份目的地。  一如您對於本機儲存體或其他異地選項的處理方式，您可以使用此功能手動備份或設定您自己的備份策略。 此功能又稱為 **SQL Server 備份至 URL**。 如需詳細資訊，請參閱＜ [SQL Server Backup to URL](sql-server-backup-to-url.md)＞。 SQL Server 2012 SP1 CU2 或更新版本皆提供此功能。  
  
    > [!NOTE]  
    >  若是使用 SQL Server 2014 之前的 SQL Server 版本，則可使用增益集 SQL Server 備份至 Windows Azure 工具，快速而輕鬆地建立要儲存到 Windows Azure 儲存體的備份。 如需詳細資訊，請參閱＜ [下載中心](http://go.microsoft.com/fwlink/?LinkID=324399)＞。  
  
-   **讓 SQL Server 管理 Windows Azure 的備份：** 設定 SQL Server 管理的備份策略及排程備份單一資料庫或多個資料庫，或執行個體層級設定預設值。 這項功能指**[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]**。 如需詳細資訊，請參閱[SQL Server Managed Backup to Windows Azure](sql-server-managed-backup-to-microsoft-azure.md)。 SQL Server 2014 或更新版本皆提供此功能。  
  
## <a name="benefits-of-using-the-windows-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份使用 Windows Azure Blob 服務的優點  
  
-   彈性、可靠且沒有限制的異地儲存體：將您的備份儲存在 Windows Azure Blob 服務上可能會成為一種方便、彈性且容易存取的異地選項。 針對您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份建立異地儲存體就像修改現有的指令碼/作業一樣簡單。 異地儲存體通常應該遠離實際執行資料庫位置，防止單一災害同時影響異地和實際執行資料庫位置。 透過選擇異地備援 Blob 儲存體，您就可以在發生可能影響整個地區的災害時，獲得一層額外的保護。 此外，您可以隨時隨地取得備份，輕鬆地針對還原作業進行存取。  
  
-   備份封存：Windows Azure Blob 儲存體服務提供了較佳的替代方案，有效取代封存備份的常用磁帶選項。 磁帶儲存體可能需要實際運輸至異地設施並採取措施來保護媒體。 將您的備份儲存在 Windows Azure Blob 儲存體中，即可提供立即、高可用性且耐用的封存選項。  
  
-   沒有硬體管理的負擔：Windows Azure 服務不會產生任何硬體管理的負擔。 Windows Azure 服務會管理硬體並提供地理複寫以產生備援效果，防止硬體故障。  
  
-   目前，對於在 Windows Azure 虛擬機器中執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體而言，備份至 Windows Azure Blob 儲存體服務可以透過建立附加磁碟來完成。 不過，您可以附加至 Windows Azure 虛擬機器的磁碟數目有所限制。 超大執行個體的限制為 16 個磁碟，而較小執行個體的限制則更低。 只要啟用直接備份至 Windows Azure Blob 儲存體的功能，您就可以忽略 16 個磁碟的限制。  
  
     此外，目前儲存在 Windows Azure Blob 儲存體服務中的備份檔案可以直接提供給內部部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或在 Windows Azure 虛擬機器中執行的其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用，完全不需要進行資料庫附加/卸離，或是下載並附加 VHD。  
  
-   成本效益：只有使用的服務才要付費。 成為符合成本效益的異地與備份封存選項。 請參閱[Windows Azure 計費考量](#Billing)一節以取得詳細資訊和連結。  
  
##  <a name="Billing"></a> Windows Azure 計費考量：  
 了解 Windows Azure 儲存體成本可讓您預測在 Windows Azure 中建立和儲存備份的成本。  
  
 [Windows Azure 定價計算機](http://go.microsoft.com/fwlink/?LinkId=277060)可以協助您預估成本。  
  
 **儲存體** ：費用是根據使用的空間收費，而計算方式採累進費率和備援等級計算。 如需詳細資料與最新資訊，請參閱 **定價詳細資料** 文章的 [資料管理](http://go.microsoft.com/fwlink/?LinkId=277059) 一節。  
  
 **資料傳輸：** 至 Windows Azure 的輸入的資料傳輸為免費。 輸出傳輸則必須支付頻寬使用量的費用，計算方式是根據地區特定的累進費率計算。 如需詳細資料，請參閱＜定價詳細資料＞文章的 [資料傳輸](http://go.microsoft.com/fwlink/?LinkId=277061) 一節。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 備份至 URL 的最佳作法和疑難排解](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [系統資料庫的備份與還原 &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [教學課程： SQL Server 備份及還原至 Windows Azure Blob 儲存體服務](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [SQL Server 備份至 URL](sql-server-backup-to-url.md)  
  
  
