---
title: "第 3 課：定義資料表報表的資料集 (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
caps.latest.revision: "53"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.openlocfilehash: c610c2cba4f004a35d1d90aceb9288b995587c74
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>第 3 課：定義資料表報表的資料集 (Reporting Services)
當您定義資料來源之後，就需要定義資料集。 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中，報表所用的資料是包含在「資料集」中。 資料集含有指向資料來源的指標和報表要用的查詢，以及計算的欄位和變數。  
  
使用報表設計師中的查詢設計工具來設計資料集。 在此教學課程中，您將建立一項查詢來擷取 [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 資料庫中的銷售訂單資訊。  
  
### <a name="to-define-a-transact-sql-query-for-report-data"></a>若要定義報表資料的 Transact-SQL 查詢  
  
1.  在 [報表資料] 窗格中，按一下 [新增]，然後按一下 [資料集…]。 **[資料集屬性]** 對話方塊隨即開啟。  
  
2.  在 [名稱] 方塊中，鍵 **AdventureWorksDataset**。  
  
3.  按一下 [使用內嵌在我的報表中的資料集]。  
  
4.  選取您在上一課 ( [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]) 中建立的資料來源。   
5. 在 [查詢類型] 中，選取 [文字]。  
  
6.  在 [查詢] 方塊中，鍵入 (或複製和貼上) 下列 Transact-SQL 查詢。  
  
    ```  
    SELECT   
       soh.OrderDate AS [Date],   
       soh.SalesOrderNumber AS [Order],   
       pps.Name AS Subcat, pp.Name as Product,    
       SUM(sd.OrderQty) AS Qty,  
       SUM(sd.LineTotal) AS LineTotal  
    FROM Sales.SalesPerson sp   
       INNER JOIN Sales.SalesOrderHeader AS soh   
          ON sp.BusinessEntityID = soh.SalesPersonID  
       INNER JOIN Sales.SalesOrderDetail AS sd   
          ON sd.SalesOrderID = soh.SalesOrderID  
       INNER JOIN Production.Product AS pp   
          ON sd.ProductID = pp.ProductID  
       INNER JOIN Production.ProductSubcategory AS pps   
          ON pp.ProductSubcategoryID = pps.ProductSubcategoryID  
       INNER JOIN Production.ProductCategory AS ppc   
          ON ppc.ProductCategoryID = pps.ProductCategoryID  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,   
       soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'  
    ```  
  
7.  (選擇性) 按一下 [查詢設計工具] 按鈕。 查詢會顯示在以文字為基礎的查詢設計工具中。 您可以按一下 [當成文字編輯]，切換到圖形化查詢設計工具。 在查詢設計工具工具列上，按一下 [執行] ![ssrs_querydesigner_run](../reporting-services/media/ssrs-querydesigner-run.png)  按鈕，藉以檢視查詢的結果。  
  
    您可以在 [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 資料庫中看到 4 個不同資料表的 6 個欄位。 查詢會使用別名之類的 Transact-SQL 功能。 例如，SalesOrderHeader 資料表稱為 *soh*。  
  
8.  按一下 [確定] 結束查詢設計工具。  
  
9.  按一下 [確定] 結束 [資料集屬性] 對話方塊。  
  
    您的 **AdventureWorksDataset** 資料集和欄位會顯示在 [報表資料] 窗格中。  
    ![ssrs_adventureworksdataset](../reporting-services/media/ssrs-adventureworksdataset.png)  
  
## <a name="next-task"></a>下一項工作  
您已順利指定一項擷取報表資料的查詢。 之後，您要建立報表配置。 請參閱[第 4 課：將資料表新增至報表 &#40;Reporting Services&#41;](../reporting-services/lesson-4-adding-a-table-to-the-report-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
[查詢設計工具 &#40;SSRS&#41;](../reporting-services/report-data/query-design-tools-ssrs.md)  
[SQL Server 連接類型 &#40;SSRS&#41;](../reporting-services/report-data/sql-server-connection-type-ssrs.md)  
[教學課程：撰寫國際性通用的 Transact-SQL 陳述式](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
  

