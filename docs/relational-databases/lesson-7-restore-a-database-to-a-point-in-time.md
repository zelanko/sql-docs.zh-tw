---
title: "第 7 課：將資料庫還原至某個時間點 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
caps.latest.revision: "13"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 479f890cd6623b457b53cc0024691f9169937538
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-7-restore-a-database-to-a-point-in-time"></a>第 7 課：將資料庫還原至某個時間點
在這一課，您會將 AdventureWorks2014 資料庫還原至兩個交易記錄備份之間的某個時間點。  
  
使用傳統備份時，為了完成時間點還原，您必須使用完整資料庫備份 (可能是差異備份)，以及您想要還原的時間點之前及剛好超過此時間點的所有交易記錄檔。 使用檔案快照集備份時，您只需要兩個相鄰的記錄備份檔案，這兩個檔案會提供您想要還原的時間點之前時間範圍的目標張貼內容。 您只需要兩個記錄檔案快照集備份組，因為每個記錄備份都會建立每個資料庫檔案的檔案快照集 (每個資料檔案和記錄檔)。  
  
若要將資料庫從檔案快照集備份組還原至指定的時間點，請遵循下列步驟：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  開啟新的查詢視窗，並連接到您的 Azure 虛擬機器中資料庫引擎的 SQL Server 2016 執行個體。  
  
3.  將下列 Transact-SQL 指令碼複製並貼入查詢視窗中，然後執行此指令碼。 確認 Production.Location 資料表有 29,939 個資料列，再將它還原至步驟 5 中有較少資料列的時間點。  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location  
  
    ```  
  
    ![顯示 29,939 的資料列計數](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "顯示 29,939 的資料列計數")  
  
4.  將下列 Transact-SQL 指令碼複製並貼入 [查詢] 視窗中。 選取兩個相鄰的記錄備份檔案，並將檔案名稱轉換成此指令碼所需的日期和時間。 適當地修改儲存體帳戶名稱以及您在第 1 課中所指定容器的 URL，提供第一個和第二個備份檔案名稱，提供 "June 26, 2015 01:48 PM" 格式的 STOPAT 時間，然後執行此指令碼。 此指令碼需要幾分鐘才能完成  
  
    ```  
  
    -- restore and recover to a point in time between the times of two transaction log backups, and then verify the row count  
    ALTER DATABASE AdventureWorks2014 SET SINGLE_USER WITH ROLLBACK IMMEDIATE;  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<firstbackupfile>.bak'   
       WITH NORECOVERY,REPLACE;  
    RESTORE LOG AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<secondbackupfile>.bak'    
       WITH RECOVERY, STOPAT = 'June 26, 2015 01:48 PM';  
    ALTER DATABASE AdventureWorks2014 set multi_user;  
    -- get new count  
    SELECT COUNT (*) FROM AdventureWorks2014.Production.Location ;  
  
    ```  
  
5.  檢閱輸出。 請注意，還原後的資料列計數為 18,389，也就是介於記錄備份 5 和 6 之間的資料列計數 (您的資料列計數會有所不同)。  
  
    ![結果窗格，顯示時間點還原之後的資料列計數](../relational-databases/media/4a0c6d8b-e2ed-4e93-bd7a-ade22a4aecc6.JPG "結果窗格，顯示時間點還原之後的資料列計數")  
  
**下一課：**  
  
[第 8 課：從記錄備份還原為新的資料庫](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
  
