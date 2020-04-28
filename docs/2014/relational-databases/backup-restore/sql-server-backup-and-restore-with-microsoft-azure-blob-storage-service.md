---
title: 使用 Azure Blob 儲存體服務 SQL Server 備份和還原 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38c92e397c971f6e9976bb857c63410fa60b7e85
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "75232425"
---
# <a name="sql-server-backup-and-restore-with-azure-blob-storage-service"></a>使用 Azure Blob 儲存體服務的 SQL Server 備份及還原
  本主題介紹[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Azure Blob 儲存體服務](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)的備份與還原。 它也提供使用 Azure Blob 服務來儲存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]備份的優點摘要。  
  
 SQL Server 支援以下列方式將備份儲存到 Azure Blob 儲存體服務：  
  
-   **管理您的 Azure 備份：** 您現在可以使用用來備份至磁片和磁帶的相同方法，將 URL 指定為備份目的地，以備份至 Azure 儲存體。  一如您對於本機儲存體或其他異地選項的處理方式，您可以使用此功能手動備份或設定您自己的備份策略。 此功能又稱為 **SQL Server 備份至 URL**。 如需詳細資訊，請參閱 [SQL Server Backup to URL](sql-server-backup-to-url.md)。 SQL Server 2012 SP1 CU2 或更新版本皆提供此功能。  
  
    > [!NOTE]  
    >  針對 SQL Server 2014 之前的 SQL Server 版本，您可以使用增益集 SQL Server 備份至 Azure 工具，快速且輕鬆地建立 Azure 儲存體的備份。 如需詳細資訊，請參閱＜ [下載中心](https://go.microsoft.com/fwlink/?LinkID=324399)＞。  
  
-   **讓 SQL Server 管理 Azure 的備份：** 設定 SQL Server 來管理單一資料庫或多個資料庫的備份策略與排程備份，或在實例層級設定預設值。 這項功能稱為**[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]**。 如需詳細資訊，請參閱[SQL Server 受控備份至 Azure](sql-server-managed-backup-to-microsoft-azure.md)。 SQL Server 2014 或更新版本皆提供此功能。  
  
## <a name="benefits-of-using-the-azure-blob-service-for-ssnoversion-backups"></a>使用 Azure Blob 服務進行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]備份的優點  
  
-   彈性、可靠且無限制的異地儲存體：將您的備份儲存在 Azure Blob 服務可以是方便、彈性且容易存取的異地選項。 針對您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份建立異地儲存體就像修改現有的指令碼/作業一樣簡單。 異地儲存體通常應該遠離實際執行資料庫位置，防止單一災害同時影響異地和實際執行資料庫位置。 透過選擇異地備援 Blob 儲存體，您就可以在發生可能影響整個地區的災害時，獲得一層額外的保護。 此外，您可以隨時隨地取得備份，輕鬆地針對還原作業進行存取。  
  
-   備份封存： Azure Blob 儲存體服務提供較佳的替代方案，讓您更容易保存備份的常用磁帶選項。 磁帶儲存體可能需要實際運輸至異地設施並採取措施來保護媒體。 將備份存放在 Azure Blob 儲存體提供了立即、高度可用且持久的封存選項。  
  
-   沒有硬體管理的額外負荷： Azure 服務不會產生硬體管理的額外負荷。 Azure 服務會管理硬體，並提供地埋區域備援複寫，以提供備援及硬體故障的防護。  
  
-   目前，針對在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure 虛擬機器中執行的實例，您可以藉由建立連接的磁片來備份至 azure Blob 儲存體服務。 不過，您可以連接到 Azure 虛擬機器的磁片數目有所限制。 超大執行個體的限制為 16 個磁碟，而較小執行個體的限制則更低。 藉由啟用直接備份至 Azure Blob 儲存體，您可以略過16個磁片限制。  
  
     此外，現在儲存在 Azure Blob 儲存體服務中的備份檔案可以直接提供給內部部署[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或在 Azure 虛擬機器中執行的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]另一個，而不需要資料庫附加/卸離或下載並連結 VHD。  
  
-   成本效益：只有使用的服務才要付費。 成為符合成本效益的異地與備份封存選項。 如需詳細資訊和連結，請參閱[Azure 計費考慮](#Billing)一節。  
  
##  <a name="azure-billing-considerations"></a><a name="Billing"></a>Azure 計費考慮：  
 瞭解 Azure 儲存體成本可讓您預測在 Azure 中建立和儲存備份的成本。  
  
 [Azure 定價計算機](https://go.microsoft.com/fwlink/?LinkId=277060)可以協助您預估成本。  
  
 **儲存體** ：費用是根據使用的空間收費，而計算方式採累進費率和備援等級計算。 如需詳細資料與最新資訊，請參閱 **定價詳細資料** 文章的 [資料管理](https://go.microsoft.com/fwlink/?LinkId=277059) 一節。  
  
 **資料傳輸：** Azure 的輸入資料傳輸是免費的。 輸出傳輸則必須支付頻寬使用量的費用，計算方式是根據地區特定的累進費率計算。 如需詳細資料，請參閱＜定價詳細資料＞文章的 [資料傳輸](https://go.microsoft.com/fwlink/?LinkId=277061) 一節。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 備份至 URL 的最佳作法和疑難排解](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [系統資料庫的備份與還原 &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [教學課程： SQL Server 備份和還原至 Azure Blob 儲存體服務](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [SQL Server 備份至 URL](sql-server-backup-to-url.md)  
  
