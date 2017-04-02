---
title: "教學課程：SQL Server 備份及還原至 Windows Azure Blob 儲存體服務 | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016 Preview"
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# 教學課程：SQL Server 備份及還原至 Windows Azure Blob 儲存體服務
歡迎使用「SQL Server 備份及還原與 Windows Azure Blob 儲存體服務使用者入門」教學課程。 本教學課程可協助您了解如何將備份寫入 Windows Azure Blob 儲存體服務以及從中還原。  
  
## 學習內容  
本教學課程會為您示範如何建立 Windows 儲存體帳戶和 Blob 容器、建立認證以存取儲存體帳戶、將備份寫入 Blob 服務，以及執行簡單還原。 這個教學課程分成四個課程：  
  
[第 1 課：建立 Windows Azure 儲存體物件](../Topic/Lesson%201:%20Create%20Windows%20Azure%20Storage%20Objects.md)  
在這一課，您會建立 Windows Azure 儲存體帳戶和 Blob 容器。  
  
[Lesson 2: Create a SQL Server Credential](../Topic/Lesson%202:%20Create%20a%20SQL%20Server%20Credential.md)  
在這一課，您會建立認證以儲存用來存取 Windows Azure 儲存體帳戶的安全性資訊。  
  
[第 3 課：將完整資料庫備份寫入 Windows Azure Blob 儲存體服務](../Topic/Lesson%203:%20Write%20a%20Full%20Database%20Backup%20to%20the%20Windows%20Azure%20Blob%20Storage%20Service.md)  
在這一課，您會發出 T-SQL 陳述式，以便將 AdventureWorks2012 資料庫的備份寫入 Windows Azure Blob 儲存體服務。  
  
[第 4 課：從完整資料庫備份執行還原](../Topic/Lesson%204:%20Perform%20a%20Restore%20From%20a%20Full%20Database%20Backup.md)  
在這一課，您會發出 T-SQL 陳述式，以便從上一課建立的資料庫備份還原。  
  
### 需求  
若要完成本教學課程，您必須熟悉 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份與還原概念以及 T-SQL 語法。 若要使用此教學課程，您的系統必須符合下列需求：  
  
-   已安裝 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]的執行個體以及 AdventureWorks2012 資料庫。  
  
    SQL Server 執行個體可以採用內部部署，也可以位於 Windows Azure 虛擬機器中。  
  
    您可以使用使用者資料庫來取代 AdventureWorks2012，並且據以修改 tsql 語法。  
  
-   用來發出 BACKUP 或 RESTORE 命令的使用者帳戶應該位於擁有**改變任何認證**權限的 **db_backup 運算子**資料庫角色中。  
  
### 其他閱讀資料  
以下是一些建議閱讀的主題，這些主題可讓您了解針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份使用 Windows Azure Blob 儲存體服務的概念與最佳作法。  
  
1.  [使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [SQL Server 備份至 URL 的最佳作法和疑難排解](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
## 另請參閱  
[備份資料庫和記錄](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#databaselog)  
[建立主要檔案群組的完整檔案備份](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#filegroups)  
[還原資料庫和移動檔案](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#restoredbwithmove)  
  
