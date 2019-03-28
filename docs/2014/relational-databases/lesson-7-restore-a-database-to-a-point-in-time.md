---
title: 第 8 課： 將資料庫還原至 Windows Azure 儲存體 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9e0841c3473baf73033f298cfd3c8402ffc3aa19
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532560"
---
# <a name="lesson-8-restore-a-database-to-windows-azure-storage"></a>第 8 課： 將資料庫還原至 Windows Azure 儲存體
  在這一課，您將學習如何在本機上建立備份檔案，然後將它還原到 Windows Azure 儲存體。 請注意，您的資料庫可以位於 Windows Azure 的內部部署或虛擬機器中。 進行這一課並不需要完成第 4、5、6 和 7 課。  
  
 這個課程假設您已完成下列步驟：  
  
-   您擁有 Windows Azure 儲存體帳戶。  
  
-   您已在 Windows Azure 儲存體帳戶下建立容器。  
  
-   您已在容器上建立具有讀取、寫入和列出權限的原則。 您也已經產生 SAS 金鑰。  
  
-   您已在來源電腦上根據共用存取簽章建立 SQL Server 認證。  
  
-   您已在來源電腦上建立資料庫。  
  
 若要將資料庫還原至 Windows Azure 儲存體，可以依照下列步驟進行：  
  
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
  
 若要使用 SQL Server Management Studio 使用者介面還原資料庫，且其中資料和記錄檔指向 Windows Azure 儲存體，請執行下列步驟：  
  
1.  在 **物件總管 中**，按一下 伺服器名稱以展開伺服器樹狀目錄。  
  
2.  依序展開**資料庫**，並選取您的資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 [工作]，然後按一下 [還原]。  
  
4.  在 **一般**頁面上，於**還原**來源區段中，按一下**來源**裝置。  
  
5.  按一下 瀏覽按鈕**來源**裝置 文字方塊中，這會開啟**選取備份裝置** 對話方塊。  
  
6.  在 [備份媒體] 文字方塊中，選取**檔案**，然後按一下**新增**按鈕尋找備份檔案 (.bak)。 按一下 [確定] 。  
  
7.  按一下 **檔案**第一頁。  
  
8.  在 **還原資料庫檔案**區段中下方**還原成**欄位中，輸入下列項目：  
  
     資料檔案，請輸入： `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf`。 如需記錄檔中，輸入： `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf`。  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. 按一下 [確定] 。  
  
 還原完成時，登入管理入口網站。 您應該能夠在容器中看見 .mdf 和 .ldf 檔案，如下所示：  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **下一課：**  
  
 [第 9 課：從 Windows Azure 儲存體還原資料庫](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
