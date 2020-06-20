---
title: 第4課：在 Azure 儲存體中建立資料庫 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3e95616b2b001dff4b2d375800fe4bbaf315a214
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025123"
---
# <a name="lesson-4-create-a-database-in-azure-storage"></a>第 4 課：在 Azure 儲存體中建立資料庫
  在這一課，您將瞭解如何使用 Azure 中的 SQL Server 資料檔案功能來建立資料庫。 請注意，開始進行這一課之前，您必須先完成第 1、2 和 3 課。 第3課是非常重要的步驟，因為您必須先將 Azure 儲存體容器及其相關聯的原則名稱和 SAS 金鑰等資訊儲存在第4課的 SQL Server 認證存放區中。  
  
 對於資料或記錄檔所使用的每一個儲存體容器，您必須建立名稱符合容器路徑的 SQL Server 認證。 然後，您可以在 Azure 儲存體中建立新的資料庫。  
  
 這個課程假設您已完成下列步驟：  
  
-   您有 Azure 儲存體帳戶。  
  
-   您已在 Azure 儲存體帳戶底下建立容器。  
  
-   您已在容器上建立具有讀取、寫入和列出權限的原則。 您也已經產生 SAS 金鑰。  
  
-   您已在來源電腦上建立 SQL Server 認證。  
  
 若要使用 Azure 儲存體功能中的 SQL Server 資料檔案在 Azure 中建立資料庫，請遵循下列步驟：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  在 [物件總管] 中連接到已安裝的 Database Engine 執行個體。  
  
3.  在 [標準] 工具列上，按一下 [新增查詢]。  
  
4.  將下列範例複製並貼入查詢視窗中，並視需要修改。 請注意，FILENAME 欄位會參考儲存體容器中資料庫檔案的 URI 路徑，該路徑的開頭必須為 https。  
  
    ```  
  
    --Create a database that uses a SQL Server credential    
    CREATE DATABASE TestDB1    
    ON   
    (NAME = TestDB1_data,   
       FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf')   
     LOG ON   
    (NAME = TestDB1_log,   
        FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
    GO  
  
    ```  
  
     將一些資料加入您的資料庫中。  
  
    ```  
  
    USE TestDB1;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
5.  若要查看內部部署 SQL Server 中的新 TestDB1，請重新整理 [物件總管] 中的資料庫。  
  
6.  同樣地，若要查看儲存體帳戶中新建立的資料庫，請透過 SQL Server Management Studio (SSMS) 連接到儲存體帳戶。 如需如何使用 SQL Server Management Studio 連接到 Azure 儲存體的相關資訊，請遵循下列步驟：  
  
    1.  首先，取得儲存體帳戶資訊。 登入管理入口網站。 然後，按一下 **[儲存體]** 並選擇您的儲存體帳戶。 選取儲存體帳戶後，按一下頁面底部的 **[管理存取金鑰]** 。 這樣會開啟類似的對話方塊視窗：  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-1.gif "SQL 14 CTP2")  
  
    2.  將 [**儲存體帳戶名稱**] 和 [**主要存取金鑰**] 值複製到 SSMS 中的 [**連接到 Azure 儲存體**] 對話方塊視窗。 然後按一下 **[連接]**。 這樣就會將有關儲存體帳戶容器的資訊帶到 SSMS 中，如下列螢幕擷取畫面所示：  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2.gif "SQL 14 CTP2")  
  
 下列螢幕擷取畫面示範內部部署和 Azure 儲存體環境中新建立的資料庫。  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2b.gif "SQL 14 CTP2")  
  
 **注意：** 如果容器中有任何作用中的資料檔案參考，則任何嘗試刪除相關聯 SQL Server 認證的動作都會失敗。 同樣地，如果 Blob 中特定資料庫檔案上已有租用，而您想要將它刪除，則必須先中斷 Blob 上的租用。 若要中斷租用，您可以使用 [租用 Blob](https://msdn.microsoft.com/library/azure/ee691972.aspx)。  
  
 使用這項新功能就可以設定 SQL Server，讓所有 CREATE DATABASE 陳述式都預設為具備雲端能力的資料庫。 換句話說，您可以在 SQL Server Management Studio 伺服器實例屬性中設定預設資料和記錄檔位置，因此每當您建立資料庫時，所有資料庫檔案（.mdf、.ldf）都會在 Azure 儲存體中建立為分頁 blob。  
  
 若要使用 SQL Server Management Studio 使用者介面在 Azure 儲存體中建立資料庫，請執行下列步驟：  
  
1.  在 [物件總管] 中，連接到 SQL Server Database Engine 的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [資料庫]，然後按一下 [新增資料庫]。  
  
3.  在 [新增資料庫] 對話方塊視窗中，輸入資料庫名稱。  
  
4.  變更主要資料與交易記錄檔的預設值，然後在 [資料庫檔案] 方格中按一下適當的資料格，並輸入新的值。 另外，指定檔案位置的路徑。 針對 Path 輸入儲存體容器的 URL 路徑，例如 `https://teststorageaccnt.blob.core.windows.net/testcontainer/`。 針對 FileName 輸入資料庫檔案 (.mdf、.ldf) 的實體檔案名稱。  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-4.gif "SQL 14 CTP2")  
  
     如需詳細資訊，請參閱 [將資料或記錄檔加入資料庫](databases/add-data-or-log-files-to-a-database.md)。  
  
5.  保留所有其他預設值。  
  
6.  按一下 [確定]。  
  
 若要查看內部部署 SQL Server 中的新 TestDB1，請重新整理 [物件總管] 中的資料庫。 同樣地，若要查看儲存體帳戶中新建立的資料庫，請依照本課程先前的說明，透過 SQL Server Management Studio (SSMS) 連接到儲存體帳戶。  
  
 **下一課：**  
  
 [第5課：&#40;選擇性&#41; 使用 TDE 加密您的資料庫](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
  
