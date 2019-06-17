---
title: 第 6 課：將資料庫移轉來源機器內部部署至目的地電腦在 Windows Azure 中 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1a5787a3f5aecd746ac9aafd5850e6109ebcd999
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090684"
---
# <a name="lesson-6-migrate-a-database-from-a-source-machine-on-premises-to-a-destination-machine-in-windows-azure"></a>第 6 課：在 Windows Azure 中將資料庫從內部部署來源電腦移轉至目的地電腦
  這一課假設您已有另一部 SQL Server，它可能位於 Windows Azure 中的另一部內部部署電腦或虛擬機器中。 如需如何在 Windows Azure 中建立 SQL Server 虛擬機器的詳細資訊，請參閱[佈建在 Windows Azure 上的 SQL Server 虛擬機器](http://www.windowsazure.com/manage/windows/common-tasks/install-sql-server/)。 在 Windows Azure 中佈建 SQL Server 虛擬機器之後，請確定您可以透過另一部電腦上的 SQL Server Management Studio 連接到這個虛擬機器中的 SQL Server 執行個體。  
  
 這個課程同樣假設您已完成下列步驟：  
  
-   您擁有 Windows Azure 儲存體帳戶。  
  
-   您已在 Windows Azure 儲存體帳戶下建立容器。  
  
-   您已在容器上建立具有讀取、寫入和列出權限的原則。 您也已經產生 SAS 金鑰。  
  
-   您已在來源電腦上建立 SQL Server 認證。  
  
-   您已在 Windows Azure 中建立一部目的地 SQL Server 虛擬機器。 我們建議您藉由選取包含 SQL Server 2014 的平台映像來建立它。  
  
 若要將資料庫從內部部署 SQL Server 移轉至 Windows Azure 中的另一部虛擬機器，可以依照下列步驟執行：  
  
1.  在來源電腦上 (在本教學課程中為內部部署電腦)，於 SQL Server Management Studio 中開啟查詢視窗。 卸離資料庫，藉由執行下列陳述式將它移至另一部電腦：  
  
    ```  
    -- Detach the database in the source machine   
    USE master  
    EXEC sp_detach_db 'TestDB1', 'true';  
    ```  
  
2.  如果您需要將資料庫傳送至目的地電腦，則必須先備妥目的地電腦。 若要準備目的地電腦，您需要先在目的地電腦上建立 SQL Server 認證。 如果它是加密的資料庫，則同樣需要從來源電腦將憑證匯入至目的地電腦。  
  
    1.  若要在目的地電腦上建立 SQL Server 認證，請遵循下列步驟：  
  
        1.  透過來源電腦上的 SQL Server Management Studio 連接到目的地電腦。  或者，直接在目的地電腦上啟動 SQL Server Management Studio。  
  
        2.  在 標準 工具列中，按一下 **新的查詢**。  
  
        3.  將下列範例複製並貼入查詢視窗中，並視需要修改。 下列陳述式會建立 SQL Server 認證來儲存您的儲存體容器的共用存取憑證。  
  
            ```sql  
  
            USE master   
            GO   
            CREATE CREDENTIAL [http://teststorageaccnt.blob.core.windows.net/testcontainer]   
            WITH IDENTITY='SHARED ACCESS SIGNATURE',   
            SECRET = 'your SAS key'   
            GO  
  
            ```  
  
        4.  若要查看所有可用的認證，可以在查詢視窗中執行下列陳述式：  
  
            ```sql  
            SELECT * from sys.credentials   
            ```  
  
        5.  連接到目的地伺服器時，開啟查詢視窗，並執行：  
  
            ```sql  
  
            -- Create a master key and a server certificate   
            USE master   
            GO   
            CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01'; -- You may use a different password.   
            GO   
            CREATE CERTIFICATE MySQLCert   
            FROM FILE = 'C:\certs\MySQLCert.CER'   
            WITH PRIVATE KEY   
            (   
            FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
            DECRYPTION BY PASSWORD = 'MySQLKey01'   
            );   
            GO  
  
            ```  
  
             這個步驟結束時，目的地電腦已匯入備份自來源電腦的加密憑證。 接著，您可以在目的地電腦中附加資料檔案。  
  
    2.  然後使用 FOR ATTACH 選項建立資料庫，其中資料和記錄檔會指向 Windows Azure 儲存體中現有的檔案。 在查詢視窗中，執行下列陳述式：  
  
        ```sql  
  
        --Create a database on the destination server   
        CREATE DATABASE TestDB1onDest   
        ON   
        (NAME = TestDB1_data,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf' )   
        LOG ON   
         (NAME = TestDB1_log,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
        FOR ATTACH   
        GO  
  
        ```  
  
    3.  在 [物件總管] 中按一下 [資料庫]，然後以滑鼠右鍵按一下 [重新整理]。 您應該能夠看到列出的新建立資料庫 TestDB1onDest。  
  
    4.  接著在查詢視窗中執行下列陳述式：  
  
        ```sql  
  
        USE TestDB1onDest   
        SELECT * FROM Table1;   
        GO  
  
        ```  
  
         這樣應該會列出您在第 4 課中輸入的所有資料。  
  
 請注意，加密的資料庫已傳送到另一個計算執行個體，且未移動任何資料。  
  
 若要使用 SQL Server Management Studio 使用者介面建立資料庫，且其中資料和記錄檔指向 Windows Azure 儲存體中現有的檔案，請執行下列步驟：  
  
1.  在物件總管  中，連接到 SQL Server Database Engine 的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [資料庫]  ，然後按一下 [新增資料庫]  。 然後，以滑鼠右鍵按一下 [TestDB1]。 按一下 [工作]，然後按一下 [卸離]。 在 [卸離] 對話方塊視窗中，選取 [卸除連接]。 按一下 [確定]  。  
  
3.  連接到具有 SQL Server 2014 CTP2 或更新版本的目的地電腦。 若要準備目的地電腦，您需要在目的地電腦上建立 SQL Server 認證，並指向放置 TestDB1 的相同容器。 如果您要在同一部電腦上重新附加，則不需要建立另一個認證。  
  
4.  在 **物件總管 中**，以滑鼠右鍵按一下**資料庫**，按一下 **附加**。  
  
5.  在 [**附加資料庫**來指定要附加的資料庫] 對話方塊中，按一下**新增**。 在 [**尋找資料庫檔案**] 對話視窗：  
  
     資料庫資料檔案位置，請輸入： `https://teststorageaccnt.blob.core.windows.net/testcontainer/`。  
  
     檔案名稱 中輸入： `TestDB1Data.mdf`。  
  
6.  按一下 [確定]  。  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-6-7.gif "SQL 14 CTP2")  
  
 **下一課：**  
  
 [第 7 課：將資料檔案移至 Windows Azure 儲存體](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
  
