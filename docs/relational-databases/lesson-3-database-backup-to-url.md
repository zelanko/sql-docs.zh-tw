---
title: "第 3 課：資料庫備份至 URL | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 83414948fcd1f8db58f2e6a66f948a5427d0c999
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-3-database-backup-to-url"></a>第 3 課：資料庫備份至 URL
在這一課，您會將內部部署 SQL Server 2016 執行個體中的 AdventureWorks2014 資料庫，備份至您在 [第 1 課︰在 Azure 容器上建立預存存取原則和共用存取簽章](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)中建立的 Azure 容器。  
  
> [!NOTE]  
> 如果您想要將 SQL Server 2012 SP1 CU2 或更新版本的資料庫或 SQL Server 2014 資料庫備份至此 Azure 容器，您可以使用 [這裡](https://technet.microsoft.com/en-US/library/dn435916(v=sql.120).aspx) 所記載之已被取代的語法，透過 WITH CREDENTIAL 語法備份至 URL。  
  
若要將資料庫備份至 Blob 儲存體，請遵循下列步驟：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  開啟新的查詢視窗，並連接到您 Azure 虛擬機器中資料庫引擎的 SQL Server 2016 執行個體。  
  
3.  將下列 Transact-SQL 指令碼複製並貼入查詢視窗中。 適當地修改儲存體帳戶名稱以及您在第 1 課中所指定容器的 URL，然後執行此指令碼。  
  
    ```  
  
    -- To permit log backups, before the full database backup, modify the database to use the full recovery model.  
    USE master;  
    ALTER DATABASE AdventureWorks2014  
       SET RECOVERY FULL;  
  
    -- Back up the full AdventureWorks2014 database to the container that you created in Lesson 1  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'  
  
    ```  
  
4.  開啟物件總管，並使用您的儲存體帳戶和帳戶金鑰連接到 Azure 儲存體。  
  
5.  依序展開 [容器] 及您在第 1 課中建立的容器，然後確認上述步驟 3 中的備份會出現在此容器中。  
  
    ![內部部署備份檔案在 Azure 容器中會顯示為 Blob](../relational-databases/media/0d060e51-012f-4c61-ab8d-16d461d0ffad.JPG "內部備份檔案在 Azure 容器中會顯示為 Blob")  
  
**下一課：**  
  
[第 4 課︰從 URL 將資料庫還原至虛擬機器](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  

