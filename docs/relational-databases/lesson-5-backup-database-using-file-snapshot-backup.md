---
title: "第 5 課：使用檔案快照集備份來備份資料庫 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 075262fd0b079d8f4e9f2decab233f6f793dd2df
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="lesson-5-backup-database-using-file-snapshot-backup"></a>第 5 課：使用檔案快照集備份來備份資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在這一課，您將使用檔案快照集備份，在 Azure 虛擬機器中備份 AdventureWorks2014 資料庫，以透過 Azure 快照集執行幾乎即時的備份。 如需檔案快照集備份的詳細資訊，請參閱 [Azure 中資料庫檔案的檔案快照集備份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
  
若要使用快照集檔案備份來備份 AdventureWorks2014 資料庫，請遵循下列步驟：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  開啟新的查詢視窗，並連接到您 Azure 虛擬機器中資料庫引擎的 SQL Server 2016 執行個體。  
  
3.  將下列 Transact-SQL 指令碼複製並貼入查詢視窗中，然後執行此指令碼 (不要關閉此查詢視窗 - 您將在步驟 5 中再次執行此指令碼)。 此系統預存程序可讓您檢視組成指定資料庫之每個檔案的現有檔案快照集備份。 您會發現此資料庫沒有任何檔案快照集備份。  
  
    ```  
  
    -- Verify that no file snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
4.  將下列 Transact-SQL 指令碼複製並貼入查詢視窗中。 適當地修改儲存體帳戶名稱以及您在第 1 課中所指定容器的 URL，然後執行此指令碼。 注意此備份速度有多快。  
  
    ```  
  
    -- Backup the AdventureWorks2014 database with FILE_SNAPSHOT  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Azure.bak'   
       WITH FILE_SNAPSHOT;  
  
    ```  
  
    ![結果窗格，顯示每個資料庫檔案的檔案快照集](../relational-databases/media/2a9320e0-067a-485a-8e0e-636660005e5c.JPG "結果窗格，顯示每個資料庫檔案的檔案快照集")  
  
5.  確認步驟 4 中的指令碼順利執行之後，請再次執行下列指令碼。 請注意，步驟 4 中的檔案快照集備份作業會產生資料和記錄檔的檔案快照集。  
  
    ```  
  
    -- Verify that two file-snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![顯示 2 個快照集的 sys.fn_db_backup_file_snapshots 函式結果](../relational-databases/media/fca1436e-9607-4432-97ee-f66ac2f2108d.JPG "顯示 2 個快照集的 sys.fn_db_backup_file_snapshots 函式結果")  
  
6.  在物件總管中，於您 Azure 虛擬機器的 SQL Server 2016 執行個體中，展開 [資料庫] 節點，並確認 AdventureWorks2014 資料庫已還原至此執行個體 (必要時請重新整理節點)。  
  
7.  在物件總管中，連接到 Azure 儲存體。  
  
8.  依序展開 [容器] 及您在第 1 課中建立的容器，然後確認上述步驟 4 中的 AdventureWorks2014_Azure.bak，與第 3 課中的備份檔案及第 4 課中的資料庫檔案一起出現在此容器中 (必要時請重新整理節點)。  
  
    ![檔案快照集備份顯示在 Azure 容器](../relational-databases/media/181bc970-4af7-4272-a9ae-4bef674f2e02.JPG "檔案快照集備份顯示在 Azure 容器")  
  
**下一課：**  
  
[第 6 課︰使用檔案快照集備份來產生活動和備份記錄](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
## <a name="see-also"></a>另請參閱  
[Azure 中資料庫檔案的檔案快照集備份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
  
  
  
