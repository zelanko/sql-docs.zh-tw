---
title: "教學課程：搭配使用 Azure Blob 儲存體服務和 SQL Server 2016 | Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4ae1e9aef727303d55c79463d822c4f62d3cdae0
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="tutorial-use-azure-blob-storage-service-with-sql-server-2016"></a>教學課程：搭配使用 Azure Blob 儲存體服務和 SQL Server 2016
歡迎使用在 Microsoft Azure Blob 儲存體服務教學課程中使用 SQL Server 2016。 本教學課程可協助您了解如何將 Microsoft Azure Blob 儲存體服務用於 SQL Server 資料檔案和 SQL Server 備份。  
  
Microsoft Azure Blob 儲存體服務的 SQL Server 整合支援一開始是 SQL Server 2012 Service Pack 1 CU2 增強功能，並且已使用 SQL Server 2014 和 SQL Server 2016 進一步加強。 如需功能概觀以及使用此功能的優點，請參閱 [Microsoft Azure 中的 SQL Server 資料檔案](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)。 如需即時的示範，請參閱 [File-Snapshot Backups Demo (檔案快照集備份示範)](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)。  
  
  
**下載**<br /><br />**>>**  若要下載 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]，請前往  **[評估中心](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**。<br /><br />**>>**  有 Azure 帳戶嗎？  接著前往 **[這裡](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** 來加速已安裝 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的虛擬機器。  
  
## <a name="what-you-will-learn"></a>學習內容  
本教學課程會在多項課程中示範如何在 Microsoft Azure Blob 儲存體服務中使用 SQL Server 資料檔案。 每個課程都著重在特定工作，並且應該依序完成課程。 首先，您將學習如何使用預存存取原則和共用存取簽章在 Blob 儲存體中建立新的容器。 然後，您將學習如何建立 SQL Server 認證，以便整合 SQL Server 與 Azure Blob 儲存體。 接下來，您會將資料庫備份至 Blob 儲存體，並將它還原至 Azure 虛擬機器。 您接著將使用 SQL Server 2016 檔案快照集交易記錄備份還原至某個時間點和新的資料庫。 最後，本教學課程將示範如何使用中繼資料系統預存程序和函數，協助您了解和使用檔案快照集備份。  
  
本文假設下列各項：  
  
-   您有已安裝 AdventureWorks2014 複本的 SQL Server 2016 內部部署執行個體。  
  
-   您擁有 Azure 儲存體帳戶。  
  
-   您至少有一部 Azure 虛擬機器已安裝 SQL Server 2016，並且已依照 [Provisioning a SQL Server Virtual Machine on Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-provision-sql-server/) (在 Azure 上佈建 SQL Server 虛擬機器) 來佈建此虛擬機器。 (選擇性) 第二部虛擬機器可以用於[第 8 課：從記錄備份還原為新的資料庫](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)中的案例。  
  
本教學課程分成九個必須依序完成的課程：  
  
**[第 1 課︰在 Azure 容器上建立預存存取原則和共用存取簽章](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
在這一課，您會在新的 Blob 容器上建立原則，也會產生在建立 SQL Server 認證時所使用的共用存取簽章。  
  
**[第 2 課︰使用共用存取簽章建立 SQL Server 認證](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
在這一課，您會使用 SAS 金鑰建立認證以儲存用來存取 Microsoft Azure 儲存體帳戶的安全性資訊。  
  
**[第 3 課：資料庫備份至 URL](../relational-databases/lesson-3-database-backup-to-url.md)**  
在這一課，您可以將內部部署資料庫備份至 Microsoft Azure Blob 儲存體。  
  
**[第 4 課︰從 URL 將資料庫還原至虛擬機器](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
在這一課，您會將資料庫從 Windows Azure Blob 儲存體還原至 Azure 虛擬機器。  
  
**[第 5 課：使用檔案快照集備份來備份資料庫](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)**  
在這一課，您可以使用檔案快照集備份來備份資料庫，以及檢視檔案快照集中繼資料。  
  
**[第 6 課︰使用檔案快照集備份來產生活動和備份記錄](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
在這一課，您可以在資料庫中產生活動、使用檔案快照集備份來執行伺服器記錄備份，以及檢視檔案快照集中繼資料。  
  
**[第 7 課：將資料庫還原至某個時間點](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
在這一課，您可以使用兩個檔案快照集記錄備份，將資料庫還原至某個時間點。  
  
**[第 8 課：從記錄備份還原為新的資料庫](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)**  
在這一課，您可以從檔案快照集記錄備份還原至不同虛擬機器上的新資料庫。  
  
**[第 9 課︰管理備份組和檔案快照集備份](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)**  
在這一課，您可以刪除不必要的備份組，並了解如何刪除孤立的檔案快照集備份 (必要時)。  
  
## <a name="did-this-article-help-you-were-listening"></a>這篇文章對您有幫助嗎？ 我們會持續聽取您的意見  
您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請將您的意見傳送到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Tutorial:%20Using%20the%20Microsoft%20Azure%20Blob%20storage%20service%20with%20SQL%20Server%202016%20databases%20page)  
  
## <a name="see-also"></a>另請參閱  
[Microsoft Azure 中的 SQL Server 資料檔案](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)  
[Azure 中資料庫檔案的檔案快照集備份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[SQL Server 備份至 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
  


