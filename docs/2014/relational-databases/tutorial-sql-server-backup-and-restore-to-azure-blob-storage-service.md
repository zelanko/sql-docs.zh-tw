---
title: 教學課程： SQL Server 備份及還原至 Windows Azure Blob 儲存體服務 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 65015ec9175bc1e09b97486794f7bdd44d1c1038
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056128"
---
# <a name="tutorial-sql-server-backup-and-restore-to-windows-azure-blob-storage-service"></a>教學課程：SQL Server 備份及還原至 Windows Azure Blob 儲存體服務
  歡迎使用「SQL Server 備份及還原與 Windows Azure Blob 儲存體服務使用者入門」教學課程。 本教學課程可協助您了解如何將備份寫入 Windows Azure Blob 儲存體服務以及從中還原。  
  
## <a name="what-you-will-learn"></a>學習內容  
 本教學課程會為您示範如何建立 Windows 儲存體帳戶和 Blob 容器、建立認證以存取儲存體帳戶、將備份寫入 Blob 服務，以及執行簡單還原。 這個教學課程分成四個課程：  
  
 [第 1 課：建立 Windows Azure 儲存體物件](../tutorials/lesson-1-create-windows-azure-storage-objects.md)  
 在這一課，您會建立 Windows Azure 儲存體帳戶和 Blob 容器。  
  
 [第 2 課：建立 SQL Server 認證](../tutorials/lesson-2-create-a-sql-server-credential.md)  
 在這一課，您會建立認證以儲存用來存取 Windows Azure 儲存體帳戶的安全性資訊。  
  
 [第 3 課：將完整資料庫備份寫入 Windows Azure Blob 儲存體服務](../tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)  
 在這一課，您會發出 T-SQL 陳述式，以便將 AdventureWorks2012 資料庫的備份寫入 Windows Azure Blob 儲存體服務。  
  
 [第 4 課：從完整資料庫備份執行還原](../tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)  
 在這一課，您會發出 T-SQL 陳述式，以便從上一課建立的資料庫備份還原。  
  
### <a name="requirements"></a>需求  
 若要完成本教學課程，您必須熟悉 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份與還原概念以及 T-SQL 語法。 若要使用此教學課程，您的系統必須符合下列需求：  
  
-   已安裝 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的執行個體以及 AdventureWorks2012 資料庫。  
  
     SQL Server 執行個體可以採用內部部署，也可以位於 Windows Azure 虛擬機器中。  
  
     您可以使用使用者資料庫來取代 AdventureWorks2012，並且據以修改 tsql 語法。  
  
-   用來發出 BACKUP 或 RESTORE 命令的使用者帳戶應該位於擁有 **改變任何認證** 權限的 **db_backup 運算子** 資料庫角色中。  
  
### <a name="additional-reading"></a>其他閱讀資料  
 以下是一些建議閱讀的主題，這些主題可讓您了解針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份使用 Windows Azure Blob 儲存體服務的概念與最佳作法。  
  
1.  [SQL Server 備份及還原與 Windows Azure Blob 儲存體服務](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [SQL Server 備份至 URL 的最佳作法和疑難排解](backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
