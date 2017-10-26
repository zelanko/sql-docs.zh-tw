---
title: "第 4 課︰從 URL 將資料庫還原至虛擬機器 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 31d30195b648f48b149021a7bf80aba2543a14ea
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-4-restore-database-to-virtual-machine-from-url"></a>第 4 課︰從 URL 將資料庫還原至虛擬機器
在這一課，您會將 AdventureWorks2014 資料庫還原至 AdventureWorks2014 資料庫所在之 Azure 虛擬機器中的 SQL Server 2016 執行個體。  
  
> [!NOTE]  
> 為了簡化本教學課程，我們將使用與資料庫備份時所用的相同資料和記錄檔容器。 在生產環境中，您可能會使用多個容器，通常也可能會使用多個資料檔案。 使用 SQL Server 2016 時，您也可以考慮將備份等量分割到多個 Blob，以提升備份大型資料庫時的備份效能。  
  
若要將 SQL Server 2014 資料庫從 Azure Blob 儲存體還原至 Azure 虛擬機器中的 SQL Server 2016 執行個體，請遵循下列步驟：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  開啟新的查詢視窗，並連接到您 Azure 虛擬機器中資料庫引擎的 SQL Server 2016 執行個體。  
  
3.  將下列 Transact-SQL 指令碼複製並貼入查詢視窗中。 適當地修改儲存體帳戶名稱以及您在第 1 課中所指定容器的 URL，然後執行此指令碼。  
  
    ```  
  
    -- Restore AdventureWorks2014 from URL to SQL Server instance using Azure blob storage for database files  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'   
       WITH  
          MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Data.mdf'  
         ,MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Log.ldf'  
    --, REPLACE  
  
    ```  
  
4.  開啟物件總管，並連接到您的 Azure SQL Server 2016 執行個體。  
  
5.  在物件總管中，展開 [資料庫] 節點，並確認 AdventureWorks2014 資料庫已還原 (必要時請重新整理節點)。  
  
    ![Adventure Works 2014 資料庫還原到虛擬機器中的 SQL Server 2016](../relational-databases/media/311f69a6-8443-4df5-8f30-3103c2472300.JPG "Adventure Works 2014 資料庫還原到虛擬機器中的 SQL Server 2016")  
  
6.  在物件總管中，以滑鼠右鍵按一下 AdventureWorks2014，然後按一下 [屬性] \(完成時按一下 [取消])。  
  
7.  按一下 [檔案]，並確認兩個資料庫檔案的路徑是指向 Azure Blob 容器中的 Blob URL。  
  
    ![資料庫屬性，以 URL 顯示邏輯資料檔案的檔案路徑](../relational-databases/media/cfeee576-6319-460e-9fa2-f0922e02ee23.JPG "資料庫屬性，以 URL 顯示邏輯資料檔案的檔案路徑")  
  
8.  在物件總管中，連接到 Azure 儲存體。  
  
9. 依序展開 [容器] 及您在第 1 課中建立的容器，然後確認上述步驟 3 中的 AdventureWorks2014_Data.mdf 和 AdventureWorks2014_Log.ldf，與第 3 課中的備份檔案一起出現在此容器中 (必要時請重新整理節點)。  
  
    ![Adventure Works 2014 資料和記錄檔在 Azure 容器中會顯示為 Blob](../relational-databases/media/156c7d73-44be-4754-9653-04cccb6c3066.JPG "Adventure Works 2014 資料和記錄檔在 Azure 容器中會顯示為 Blob")  
  
**下一課：**  
  
[第 5 課：使用檔案快照集備份來備份資料庫](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
  

