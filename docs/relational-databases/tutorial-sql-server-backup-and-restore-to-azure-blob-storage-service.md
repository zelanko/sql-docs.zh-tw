---
title: "教學課程：SQL Server 備份及還原至 Windows Azure Blob 儲存體服務 | Microsoft 文件"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016 Preview
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5de443574ba279fb695f8e6aee9e9238eaae7afc
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>教學課程：SQL Server 備份及還原至 Azure Blob 儲存體服務
本教學課程可協助您了解如何將備份寫入 Azure Blob 儲存體服務以及從中還原。  
  
## <a name="what-you-will-learn"></a>學習內容  
本教學課程會為您示範如何建立儲存體帳戶和 Blob 容器、建立認證以存取儲存體帳戶、將備份寫入 Blob 服務，以及執行簡單還原。 這個教學課程分成四個課程：  
  
[第 1 課：建立 Azure 儲存體物件](http://msdn.microsoft.com/library/74edd1fd-ab00-46f7-9e29-7ba3f1a446c5)  
在這一課，您會建立 Azure 儲存體帳戶和 Blob 容器。  
  
[第 2 課：建立 SQL Server 認證](http://msdn.microsoft.com/library/64f8805c-1ddc-4c96-a47c-22917d12e1ab)  
在這一課，您會建立認證以儲存用來存取 Azure 儲存體帳戶的安全性資訊。  
  
[第 3 課：將完整資料庫備份寫入 Azure Blob 儲存體服務](http://msdn.microsoft.com/library/454c8296-64e9-46ed-b141-5ebfbc8a4fe2)  
在這一課，您會發出 T-SQL 陳述式，以便將 AdventureWorks2012 資料庫的備份寫入 Azure Blob 儲存體服務。  
  
[第 4 課：從完整資料庫備份執行還原](http://msdn.microsoft.com/library/580f76e6-9802-4abc-9043-db6de592c733)  
在這一課，您會發出 T-SQL 陳述式，以便從上一課建立的資料庫備份還原。  
  
### <a name="requirements"></a>需求  
若要完成本教學課程，您必須熟悉 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份與還原概念以及 T-SQL 語法。 若要使用此教學課程，您的系統必須符合下列需求：  
  
-   已安裝 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的執行個體以及 AdventureWorks2012 資料庫。  
  
    SQL Server 執行個體可以採用內部部署，也可以位於 Azure 虛擬機器中。  
  
    您可以使用使用者資料庫來取代 AdventureWorks2012，並且據以修改 tsql 語法。  
  
-   用來發出 BACKUP 或 RESTORE 命令的使用者帳戶，應該位於擁有 **改變任何認證** 權限的 **db_backup 運算子**資料庫角色中。  
  
### <a name="additional-reading"></a>其他閱讀資料  
以下是一些建議閱讀的主題，這些主題可讓您了解針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份使用 Azure Blob 儲存體服務的概念與最佳做法。  
  
1.  [使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [SQL Server 備份至 URL 的最佳做法和疑難排解](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
## <a name="see-also"></a>另請參閱  
[使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)


