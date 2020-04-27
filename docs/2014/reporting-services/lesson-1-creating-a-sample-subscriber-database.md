---
title: 第 1 課：建立範例訂閱者資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9e68650b21ee8cddc6258ab64b874bcf51ec1a83
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108543"
---
# <a name="lesson-1-creating-a-sample-subscriber-database"></a>第 1 課：建立範例訂閱者資料庫
  在定義資料驅動訂閱之前，您必須先有提供訂閱資料的資料來源。 在這個步驟中，您將建立一個小型資料庫來儲存這個教學課程所用的訂閱資料。 稍後，當處理訂閱時，報表伺服器會擷取這份資料，並利用它來自訂報表輸出、傳遞選項以及報表呈現格式。  
  
 這一課會假設您[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]要使用來[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]建立資料庫。  
  
### <a name="to-create-a-sample-subscriber-database"></a>若要建立範例訂閱者資料庫  
  
1.  啟動 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]，然後開啟 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的連接。  
  
2.  以滑鼠右鍵按一下 [資料庫]，然後選取 [新增資料庫...]  。  
  
3.  在 [新增資料庫] 對話方塊的 [資料庫名稱] 中，輸入*訂閱者*。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  按一下工具列上的 [新增查詢]  按鈕。  
  
5.  將下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式複製到空的查詢中：  
  
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
  
6.  按一下工具列上的 **[執行]** 。  
  
7.  利用 SELECT 陳述式來確認您已有三個資料列。 例如： `select * from OrderInfo`  
  
## <a name="next-steps"></a>後續步驟  
 您已順利建立驅動報表散發作業的訂閱資料，且每位訂閱者的報表輸出都各不相同。 之後，您要修改將散發給各訂閱者之報表的資料來源屬性。 修改資料來源屬性是為了準備資料驅動訂閱所傳遞的報表。 您也會將報表設計修改為包含訂閱將搭配訂閱者資料使用的參數。 [第2課：修改報告資料來源屬性](lesson-2-modifying-the-report-data-source-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](create-a-data-driven-subscription-ssrs-tutorial.md)   
 [建立資料庫](../relational-databases/databases/create-a-database.md)   
 [建立基本資料表報表 &#40;SSRS 教學課程&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
