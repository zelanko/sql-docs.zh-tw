---
title: 第 8 課： 從記錄備份還原為新的資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7403564eabb8f7e5ff6c26bdce57caefaefa2cc2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830156"
---
# <a name="lesson-8-restore-as-new-database-from-log-backup"></a>第 8 課： 從記錄備份還原為新的資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在這一課，您會從檔案快照集交易記錄備份將 AdventureWorks2014 資料庫還原為新的資料庫。  
  
在此情況下，您會基於商務分析和報告在不同的虛擬機器上執行還原至 SQL Server 執行個體。 還原至不同虛擬機器上的不同執行個體，會基於此目的，將工作負載卸載至專用虛擬機器並進行大小調整，方法是從交易式系統中移除其資源需求。  
  
使用檔案快照集備份從交易記錄備份進行還原十分地快速，而且比使用傳統串流備份還要快。 運用傳統串流備份，您必須使用完整資料庫備份 (可能是差異備份)，以及部分或所有交易記錄備份 (或新的完整資料庫備份)。 不過，使用檔案快照集記錄備份，您只需要最新的記錄備份 (或任何其他記錄備份，或任兩個相鄰記錄備份以將時間點還原至兩個記錄備份時間之間的時間點)。 若要更為清楚，您只需要一個記錄檔案快照集備份組，因為每個檔案快照集記錄備份都會建立每個資料庫檔案的檔案快照集 (每個資料檔案和記錄檔)。  
  
若要使用檔案快照集備份從交易記錄備份將資料庫還原到新的資料庫，請執行下列步驟︰  
  
1.  連接到 SQL Server Management Studio。  
  
2.  開啟新的查詢視窗，並連接到 Azure 虛擬機器中資料庫引擎的 SQL Server 2016 執行個體。  
  
    > [!NOTE]  
    > 如果這是與您之前用於先前課程不同的 Azure 虛擬機器，請確定您遵循 [第 2 課︰使用共用存取簽章建立 SQL Server 認證](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)中的步驟進行。 如果您想要還原至不同的容器，請針對新容器遵循 [第 1 課︰在 Azure 容器上建立預存存取原則和共用存取簽章](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md) 和 [第 2 課︰使用共用存取簽章建立 SQL Server 認證](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md) 中的步驟進行。  
  
3.  將下列 Transact-SQL 指令碼複製並貼入 [查詢] 視窗中。 選取您想要使用的記錄備份檔案。 適當地修改儲存體帳戶名稱以及您在第 1 課中所指定容器的 URL，並提供記錄備份檔案名稱，然後執行此指令碼。  
  
    ```  
  
    -- restore as a new database from a transaction log backup file  
    RESTORE DATABASE AdventureWorks2014_EOM   
        FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<logbackupfile.bak'    
        WITH MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Data.mdf'  
       , MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Log.ldf'  
       , RECOVERY  
    --, REPLACE  
  
    ```  
  
4.  請檢閱輸出，確認還原成功。  
  
5.  在物件總管中，連接到 Azure 儲存體。  
  
6.  展開 [容器]，並展開您在第 1 課所建立的容器 (必要時，請重新整理)，然後確認新的資料和記錄檔出現在容器以及先前課程的 Blob 中。  
  
    ![Azure 容器，顯示新資料庫的資料和記錄檔](../relational-databases/media/e9705083-86bc-4309-a0bf-92c15f174c0a.JPG "Azure 容器，顯示新資料庫的資料和記錄檔")  
  
[第 9 課︰管理備份組和檔案快照集備份](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)  
  
  
  
