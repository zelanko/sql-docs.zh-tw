---
title: 第 9 課： 從 Windows Azure 儲存體還原資料庫 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 41fbe4cefb6a759befd8b96ded8487ff54b0a1c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090650"
---
# <a name="lesson-9-restore-a-database-from-windows-azure-storage"></a>第 9 課： 從 Windows Azure 儲存體還原資料庫
  在這一課，您將學習如何從 Windows Azure 儲存體將資料庫備份檔案還原到位於內部部署或 Windows Azure 中虛擬機器上的資料庫。 進行這一課並不需要完成第 4、5、6、7 和 8 課。  
  
 這個課程假設您已完成下列步驟：  
  
-   您已在來源電腦上建立資料庫。  
  
-   您也已使用 Windows Azure 儲存體中建立您的資料庫 (.bak) 的備份[SQL Server 備份及還原與 Windows Azure Blob 儲存體服務](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)功能。 請注意，您將需要在這個步驟中建立另一個 SQL Server 認證。 這個認證會使用儲存體帳戶金鑰。  
  
-   您擁有 Windows Azure 儲存體帳戶。  
  
-   您已在 Windows Azure 儲存體帳戶下建立容器。  
  
-   您已在容器上建立具有讀取、寫入和列出權限的原則。 您也已經產生 SAS 金鑰。  
  
-   您已在電腦上建立 Windows Azure 儲存體整合功能所需的 SQL Server 認證。 請注意，這個認證需要共用存取簽章 (SAS) 金鑰。  
  
 若要從 Windows Azure 儲存體還原資料庫，可以依照下列步驟進行：  
  
1.  啟動 SQL Server Management Studio。 連接到預設執行個體。  
  
2.  按一下 [**新的查詢**標準] 工具列上。  
  
3.  將下列完整指令碼複製並貼入查詢視窗中。 視需要修改指令碼。  
  
     **注意：** 在您執行`RESTORE`陳述式，以在 Windows Azure 儲存體還原資料庫備份 (.bak)，另一部電腦的資料庫執行個體。  
  
    ```sql  
  
    USE master   
    GO   
    -- Create a new database to be backed up.   
    CREATE DATABASE TestDbRestoreFrom;   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    SELECT * from dbo.Table1;   
    GO   
    -- Create a credential to be used by SQL Server Backup and Restore with Windows Azure -----Blob Storage Service.   
    USE master;   
    GO   
    CREATE CREDENTIAL BackupCredential    
    WITH IDENTITY= 'teststorageaccnt',   
    SECRET = 'BO1nH/lWRdnc8TGPlQIXmGLWVCoEa48suYSGiAlC73+S0TX5VXo5/LCm8qiyGCYafDg4ZsueDIV3GQ5RXHaRGw=='    
    GO   
    -- Display the newly created credential   
    SELECT * from sys.credentials   
    -- Create a backup in Windows Azure Storage.   
    BACKUP DATABASE TestDBRestoreFrom    
    TO URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
          WITH CREDENTIAL = 'BackupCredential'    
         ,COMPRESSION   
         ,STATS = 5;   
    GO    
    -- Create a Shared Access Signature credential   
    CREATE CREDENTIAL [https://teststorageaccnt.blob.core.windows.net/testrestorefrom]   
    WITH IDENTITY='SHARED ACCESS SIGNATURE',   
    SECRET = 'sv=2012-02-12&sr=c&si=policy_resfrom&sig=EhVpzLUXjG4ThAMLmVhrnoiCt8IfmD3BsuYiMawGzxc%3D'   
    GO   
    USE master;   
    GO   
    RESTORE DATABASE TestDBRestoreFrom    
    FROM URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
    WITH    
    CREDENTIAL = 'BackupCredential',    
    REPLACE,   
    MOVE 'TestDBRestoreFrom' TO 'C:\Backup\TestDBRestoreFrom.mdf',     
    MOVE 'TestDBRestoreFrom_log' TO 'C:\Backup\TestDBRestoreFrom_log.ldf';   
    GO  
  
    ```  
  
 **教學課程結束：Windows Azure 儲存體服務中的 SQL Server 資料檔案**  
  
  
