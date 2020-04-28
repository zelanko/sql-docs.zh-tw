---
title: 第 8 課： 將資料庫還原至 Azure 儲存體 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5b30a9f60f52b8b19875f5fb3c15242ce2c632fd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "70175423"
---
# <a name="lesson-8-restore-a-database-to-azure-storage"></a>第 8 課： 將資料庫還原到 Azure 儲存體
  在這一課，您將學習如何在本機建立備份檔案，然後將它還原到 Azure 儲存體。 請注意，您可以將資料庫置於內部部署或 Azure 虛擬機器中。 進行這一課並不需要完成第 4、5、6 和 7 課。  
  
 這個課程假設您已完成下列步驟：  
  
-   您有 Azure 儲存體帳戶。  
  
-   您已在 Azure 儲存體帳戶底下建立容器。  
  
-   您已在容器上建立具有讀取、寫入和列出權限的原則。 您也已經產生 SAS 金鑰。  
  
-   您已在來源電腦上根據共用存取簽章建立 SQL Server 認證。  
  
-   您已在來源電腦上建立資料庫。  
  
 若要將資料庫還原成 Azure 儲存體，您可以依照下列步驟執行：  
  
1.  在來源電腦中啟動 SQL Server Management Studio。  
  
2.  連接到新建立的資料庫時，開啟查詢視窗。 執行下列陳述式：  
  
    ```sql  
  
    USE TestDB3Restore;   
    GO   
    BACKUP DATABASE TestDB3Restore   
    TO DISK = 'C:\BACKUP\TestDB3Restore.Bak'   
       WITH FORMAT,   
       NAME = 'Full Backup of TestDB3Restore'   
    GO  
  
    ```  
  
3.  接著，在 [查詢] 視窗中複製並執行下列陳述式。  
  
    ```sql  
  
    USE master;   
    GO   
    RESTORE DATABASE TestDB3Restore    
    FROM DISK = 'C:\BACKUP\TestDB3Restore.bak'    
    WITH REPLACE,   
    MOVE 'TestDB3Restore' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore.mdf',     
    MOVE 'TestDB3Restore_log' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore_log.ldf';   
    GO  
  
    ```  
  
     在這個步驟最後，您的容器應該會列出管理入口網站上的資料檔案 (.mdf) 和 (.ldf)。  
  
 若要使用 SQL Server Management Studio 使用者介面來還原具有指向 Azure 儲存體之資料和記錄檔的資料庫，請執行下列步驟：  
  
1.  在**物件總管**中，按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  展開 [**資料庫**]，然後選取您的資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 [工作]****，然後按一下 [還原]****。  
  
4.  在 [**一般**] 頁面的 [**還原**來源] 區段中，按一下 [**來源**裝置]。  
  
5.  按一下 [**來源**裝置] 文字方塊的 [流覽] 按鈕，這會開啟 [**選取備份裝置**] 對話方塊。  
  
6.  在 [備份媒體] 文字方塊中，**選取 [** 檔案]，然後按一下 [**新增**] 按鈕以尋找備份檔案（.bak）。 按一下 [確定]  。  
  
7.  按一下第一頁**上的 [** 檔案]。  
  
8.  在 [將**資料庫檔案還原**為] 區段的 [**還原為**] 欄位底下，輸入下列內容：  
  
     針對 [資料檔案]， `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf`輸入：。 在 [記錄檔] 中`https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf`，輸入：。  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. 按一下 [確定]  。  
  
 還原完成時，登入管理入口網站。 您應該能夠在容器中看見 .mdf 和 .ldf 檔案，如下所示：  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **下一課：**  
  
 [第9課：從 Azure 儲存體還原資料庫](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
