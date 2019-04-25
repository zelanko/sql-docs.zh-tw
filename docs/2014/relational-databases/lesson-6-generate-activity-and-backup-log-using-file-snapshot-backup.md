---
title: 第 7 課：將資料檔案移至 Windows Azure 儲存體 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 45004f8544efc0f0cc02292dbe28fdd75d6dc1de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743254"
---
# <a name="lesson-7-move-your-data-files-to-windows-azure-storage"></a>第 7 課：將資料檔案移至 Windows Azure 儲存體
  在這一課，您將學習如何將資料檔案移至 Windows Azure 儲存體 (而不是您的 SQL Server 執行個體)。 進行這一課並不需要完成第 4、5 和 6 課。  
  
 若要將資料檔案移至 Windows Azure 儲存體，您可以使用 `ALTER DATABASE` 陳述式，因為它可幫助您變更資料檔案的位置。  
  
 這個課程假設您已完成下列步驟：  
  
-   您擁有 Windows Azure 儲存體帳戶。  
  
-   您已在 Windows Azure 儲存體帳戶下建立容器。  
  
-   您已在容器上建立具有讀取、寫入和列出權限的原則。 您也已經產生 SAS 金鑰。  
  
-   您已在來源電腦上建立 SQL Server 認證。  
  
 接著，使用下列步驟將資料檔案移至 Windows Azure 儲存體：  
  
1.  首先，在來源電腦中建立測試資料庫，並在其中加入一些資料。  
  
    ```sql  
  
    USE master;   
    CREATE DATABASE TestDB1Alter;   
    GO   
    USE TestDB1Alter;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
2.  請執行下列程式碼：  
  
    ```sql  
  
    -- In the following statement, modify the path specified in FILENAME to   
    -- the new location of the file in Windows Azure Storage container.   
    ALTER DATABASE TestDB1Alter    
        MODIFY FILE ( NAME = TestDB1Alter,    
                    FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontaineralter/TestDB1AlterData.mdf');   
    GO  
  
    ```  
  
3.  當您執行此動作時，您會看到此訊息：「 系統目錄中已修改的檔案"TestDB1Alter"。 新的路徑將用於的下次啟動資料庫。 」  
  
4.  然後將資料庫設為離線。  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET OFFLINE;   
    GO  
  
    ```  
  
5.  現在，您需要將資料檔案複製到 Windows Azure 儲存體中，使用其中一種下列方法：[AzCopy 工具](https://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)， [Put Page](https://msdn.microsoft.com/library/azure/ee691975.aspx)，[儲存體用戶端程式庫參考](https://msdn.microsoft.com/library/azure/dn261237.aspx)，或協力廠商儲存體總管工具。  
  
     **重要：** 當使用這個新的增強功能，請務必確定您建立分頁 blob 不是區塊 blob。  
  
6.  然後將資料庫設為線上。  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET ONLINE;   
    GO  
  
    ```  
  
 **下一課：**  
  
 [第 8 課：將資料庫還原至 Windows Azure 儲存體](lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
