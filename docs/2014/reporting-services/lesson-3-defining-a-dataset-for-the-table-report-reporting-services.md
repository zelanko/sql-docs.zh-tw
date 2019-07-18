---
title: 第 3 課：定義資料表報表的資料集 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f4c78328e02215520b8d33213e01871f010f62d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108454"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>第 3 課：定義資料表報表的資料集 (Reporting Services)
  當您定義資料來源之後，就需要定義資料集。 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中，報表所用的資料是包含在「資料集」  中。 資料集含有指向資料來源的指標和報表要用的查詢，以及計算的欄位和變數。  
  
 您可以使用報表設計師中的查詢設計工具來設計查詢。 本教學課程中，您將建立可擷取銷售訂單資訊的查詢[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] **2008年**資料庫。  
  
### <a name="to-define-a-transact-sql-query-for-report-data"></a>若要定義報表資料的 Transact-SQL 查詢  
  
1.  在 [報表資料]  窗格中，按一下 [新增]  ，然後按一下 [資料集…]  。 **[資料集屬性]** 對話方塊隨即開啟。  
  
2.  在 [名稱]  方塊中，鍵 **AdventureWorksDataset**。  
  
3.  按一下 [使用內嵌在我的報表中的資料集]  。  
  
4.  請確定您的資料來源，AdventureWorks2012，名稱是**資料來源**文字方塊中，且**查詢類型**會**文字**。  
  
5.  在 [查詢]  方塊中，鍵入 (或複製和貼上) 下列 Transact-SQL 查詢。  
  
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
  
6.  (選擇性) 按一下 [查詢設計工具]  按鈕。 查詢會顯示在以文字為基礎的查詢設計工具中。 您可以按一下 [當成文字編輯]  ，切換到圖形化查詢設計工具。 按一下執行查詢的結果來檢視 **（！）** 查詢設計工具工具列上的按鈕。  
  
     您可以在 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫中看到 4 個不同資料表的 6 個欄位。 查詢會使用別名之類的 Transact-SQL 功能。 例如，SalesOrderHeader 資料表稱為 soh。  
  
     按一下 [確定]  結束查詢設計工具。  
  
7.  按一下 [確定]  結束 [資料集屬性]  對話方塊。  
  
     您的 **AdventureWorksDataset** 資料集和欄位會顯示在 [報表資料] 窗格中。  
  
## <a name="next-task"></a>下一項工作  
 您已順利指定一項擷取報表資料的查詢。 之後，您要建立報表配置。 查看[第 4 課：將資料表新增至報表 &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [查詢設計工具，在報表設計工具的 SQL Server Data Tools &#40;SSRS&#41;](report-data/query-design-tools-ssrs.md)   
 [SQL Server 連接類型 &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)   
 [教學課程：撰寫 Transact-SQL 陳述式](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
