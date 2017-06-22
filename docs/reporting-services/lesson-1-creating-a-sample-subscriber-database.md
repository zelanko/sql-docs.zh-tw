---
title: "第 1 課： 建立範例訂閱者資料庫 |Microsoft 文件"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4d862dc34dcbb81ce8d50cfac53d81a80f47d29c
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---

# <a name="lesson-1-creating-a-sample-subscriber-database"></a>第 1 課：建立範例訂閱者資料庫

在此 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 教學課程中，您將建立小型「訂閱者」資料庫來儲存訂閱資料，以供資料驅動訂閱使用。 當處理訂閱時，報表伺服器會擷取這份資料，並利用它來自訂報表輸出。 例如，資料列會包含要用於篩選的特定訂單號碼，以及產生的報表在建立時將使用的檔案格式。  
  
這一課會假設您使用[!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)]建立 SQL Server 資料庫。  
  
### <a name="to-create-a-sample-subscriber-database"></a>若要建立範例訂閱者資料庫  
  
1.  啟動 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]，然後開啟 [!INCLUDE[ssDEnoversion_md](../includes/ssdenoversion-md.md)] 執行個體的連接。  
  
2.  以滑鼠右鍵按一下 [資料庫]，然後選取 [新增資料庫...]。  
  
3.  在 [新增資料庫] 對話方塊的 [資料庫名稱] 中，輸入*訂閱者*。 
4. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  按一下工具列上的 [新增查詢] 按鈕。  
  
6.  將下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式複製到空的查詢中：  
  
    ```  
    Use Subscribers  
    CREATE TABLE [dbo].[OrderInfo] (  
        [SubscriptionID] [int] NOT NULL PRIMARY KEY ,  
        [Order] [nvarchar] (20) NOT NULL,  
        [FileType] [bit],  
        [Format] [nvarchar] (20) NOT NULL ,  
    ) ON [PRIMARY]  
    GO  
  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('1', 'so43659', '1', 'IMAGE')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('2', 'so43664', '1', 'MHTML')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('3', 'so43668', '1', 'PDF')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('4', 'so71949', '1', 'Excel')  
    GO  
    ```  
  
7.  按一下**！執行**工具列上。  
  
8.  利用 SELECT 陳述式來確認您已有三個資料列。 例如： `select * from OrderInfo`  
  
## <a name="next-steps"></a>後續步驟  
+ 您已順利建立驅動報表散發作業的訂閱資料，且每位訂閱者的報表輸出都各不相同。 
+ 接下來，您將修改要使用預存認證之報表的資料來源屬性。 
+ 您也會將報表設計修改為包含訂閱將搭配訂閱者資料使用的參數。 [第 2 課：修改報表資料來源屬性](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)。  

## <a name="next-steps"></a>後續的步驟

[建立資料驅動訂閱](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[建立資料庫](../relational-databases/databases/create-a-database.md)  
[建立基本資料表報表](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
