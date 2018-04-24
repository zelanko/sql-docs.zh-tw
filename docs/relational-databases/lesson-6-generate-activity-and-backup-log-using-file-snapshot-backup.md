---
title: 第 6 課︰使用檔案快照集備份來產生活動和備份記錄 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9a0c763bb826140ef12e51d32900623d7f82764e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup"></a>第 6 課︰使用檔案快照集備份來產生活動和備份記錄
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在本課程中，您將使用檔案快照集備份，在 AdventureWorks2014 資料庫中產生活動並定期建立交易記錄備份。 如需如何使用檔案快照集備份的詳細資訊，請參閱 [Azure 中資料庫檔案的檔案快照集備份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
若要使用檔案快照集備份，在 AdventureWorks2014 資料庫中產生活動並定期建立交易記錄備份，請遵循下列步驟：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  開啟兩個新的查詢視窗，並將這兩個視窗都連接到 Azure 虛擬機器中資料庫引擎的 SQL Server 2016 執行個體。  
  
3.  將下列 Transact-SQL 指令碼複製並貼入其中一個查詢視窗中，然後執行此指令碼。 請注意，在我們新增步驟 4 的新資料列之前，Production.Location 資料表有 14 個資料列。  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
4.  將下列兩個 Transact-SQL 指令碼複製並分別貼入這兩個查詢視窗中。 適當地修改儲存體帳戶名稱以及您在第 1 課中所指定容器的 URL，然後分別在這兩個查詢視窗中同時執行這些指令碼。 這些指令碼需要大約七分鐘時間才能完成。  
  
    ```  
    -- Insert 30,000 new rows into the Production.Location table in the AdventureWorks2014 database in batches of 75  
    DECLARE @count INT=1, @inner INT;  
    WHILE @count < 400  
       BEGIN  
          BEGIN TRAN;  
             SET @inner =1;  
                WHILE @inner <= 75  
                   BEGIN;  
                      INSERT INTO AdventureWorks2014.Production.Location    
                         (Name, CostRate, Availability, ModifiedDate)   
                            VALUES (NEWID(), .5, 5.2, GETDATE());  
                      SET @inner = @inner + 1;  
                   END;  
          COMMIT;  
       WAITFOR DELAY '00:00:01';   
       SET @count = @count + 1;  
       END;  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
    ```  
    --take 7 transaction log backups with FILE_SNAPSHOT, one per minute, and include the row count and the execution time in the backup file name   
    DECLARE @count INT=1, @device NVARCHAR(120), @numrows INT;  
    WHILE @count <= 7  
       BEGIN  
             SET @numrows = (SELECT COUNT (*) FROM AdventureWorks2014.Production.Location);  
             SET @device = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-' + CONVERT (varchar(10),@numrows) + '-' + FORMAT(GETDATE(), 'yyyyMMddHHmmss') + '.bak';  
             BACKUP LOG AdventureWorks2014 TO URL = @device WITH FILE_SNAPSHOT;  
             SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
          WAITFOR DELAY '00:1:00';   
             SET @count = @count + 1;  
       END;  
    ```  
  
5.  檢閱第一個指令碼的輸出，並注意現在最後的資料列計數是 29,939。  
  
    ![顯示 29,939 的資料列計數](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "顯示 29,939 的資料列計數")  
  
6.  檢閱第二個指令碼的輸出，並注意，每次 BACKUP LOG 陳述式執行時，系統都會建立兩個新的檔案快照集：一個記錄檔的檔案快照集和一個資料檔案的檔案快照集，因此每一個資料庫檔案總共會有兩個檔案快照集。 第二個指令碼完成之後，請注意，現在共有 16 個檔案快照集，每一個資料庫檔案總共有 8 個：一個來自 BACKUP DATABASE 陳述式而另一個是每次執行 BACKUP LOG 陳述式時產生。  
  
    ![結果窗格，顯示取得記錄檔備份時的資料和記錄檔的檔案快照集](../relational-databases/media/acd213b8-895e-425c-bd72-2bf10e65a5ba.JPG "結果窗格，顯示取得記錄檔備份時之資料和記錄檔的檔案快照集")  
  
    ![顯示四個檔案快照集](../relational-databases/media/e7eff77d-85b9-4e52-abd8-e49952c8118a.JPG "顯示四個檔案快照集")  
  
    ![結果窗格，顯示總共 16 個檔案快照集](../relational-databases/media/c3ddff17-a83c-4bf0-a670-a38834f9c922.JPG "結果窗格，顯示總共 16 個檔案快照集")  
  
7.  在物件總管中，連接到 Azure 儲存體。  
  
8.  展開 [容器]，並展開您在第 1 課所建立的容器，並確認其中有顯示 7 個新的備份記錄檔與先前課程的 Blob (您可視需要重新整理)。  
  
    ![Azure 容器，顯示 7 個記錄檔備份 Blob](../relational-databases/media/cfa5a326-87a2-4202-9a04-38bf577d2d0b.JPG "Azure 容器，顯示 7 個記錄檔備份 Blob")  
  
**下一課：**  
  
[第 7 課：將資料庫還原至某個時間點](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
  
