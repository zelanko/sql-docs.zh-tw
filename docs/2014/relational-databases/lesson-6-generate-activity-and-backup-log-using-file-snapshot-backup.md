---
title: 第 7 課： 將資料檔案移至 Windows Azure 儲存體 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 44bc025ce3eb536e10f4c77410ea487e59f006ee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37162709"
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
  
    ```tsql  
  
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
  
    ```tsql  
  
    -- In the following statement, modify the path specified in FILENAME to   
    -- the new location of the file in Windows Azure Storage container.   
    ALTER DATABASE TestDB1Alter    
        MODIFY FILE ( NAME = TestDB1Alter,    
                    FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontaineralter/TestDB1AlterData.mdf');   
    GO  
  
    ```  
  
3.  當您執行此程式碼時，會看到此訊息：「系統目錄中已修改了檔案 "TestDB1Alter"。 資料庫下次啟動時將會使用新路徑」。  
  
4.  然後將資料庫設為離線。  
  
    ```tsql  
  
    ALTER DATABASE TestDB1Alter SET OFFLINE;   
    GO  
  
    ```  
  
5.  現在，您必須使用下列方法之一，將資料檔複製到 Windows Azure 儲存體： [AzCopy 工具](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)、 [Put Page](https://msdn.microsoft.com/library/azure/ee691975.aspx)、 [儲存體用戶端程式庫參考](https://msdn.microsoft.com/library/azure/dn261237.aspx)，或協力廠商儲存體總管工具。  
  
     **重要事項：** 使用這項新的增強功能時，請務必確定您建立的是分頁 Blob，而不是區塊 Blob。  
  
6.  然後將資料庫設為線上。  
  
    ```tsql  
  
    ALTER DATABASE TestDB1Alter SET ONLINE;   
    GO  
  
    ```  
  
 **下一課：**  
  
 [第 8 課：將資料庫還原至 Windows Azure 儲存體](lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
