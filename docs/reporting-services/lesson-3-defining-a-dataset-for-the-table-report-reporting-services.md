---
title: 第 3 課：定義資料表報表的資料集 | Microsoft Docs
description: 在本課程中，了解如何在 SQL Server Reporting Services (SSRS) 中，針對資料表報表定義資料集。
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 272787e124616593c90483735afec702f5d4fb18
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247547"
---
# <a name="lesson-3-define-a-dataset-for-the-table-report---sql-server-reporting-services"></a>第 3 課：定義資料表報表的資料集 - SQL Server Reporting Services

當您為分頁報表定義資料來源之後，就需要定義資料集。 在 [!INCLUDE[ssrsnoversion](../includes/ssrsnoversion-md.md)] 中，報表所用的資料是包含在「資料集」中。 資料集含有指向資料來源的指標和報表要使用的查詢、導出欄位和變數。

使用報表設計師中的查詢設計工具來定義資料集。 在本教學課程中，您將建立一項查詢，可擷取 AdventureWorks2016 資料庫中的銷售訂單資訊。

## <a name="define-a-transact-sql-query-for-report-data"></a>定義報表資料的 Transact-SQL 查詢  

1. 在 [報表資料] 窗格中，選取 [新增] > [資料集...]。[資料集屬性] 對話方塊隨即開啟，並顯示 [查詢] 區段。

    ![vs-data_set_properties_dialog](media/lesson-3-defining-a-dataset-for-the-table-report-reporting-services/vs-dataset-properties-dialog.png)

2. 在 [名稱] 文字方塊中，輸入 "AdventureWorksDataset"。

3. 在該文字方塊下方，選取 [使用內嵌在我的報表中的資料集] 選項按鈕。

4. 從 [資料來源] 下拉式方塊中，選取 AdventureWorks2016。

5. 針對 [查詢類型]，選取 [文字] 選項按鈕。

6. 在 [查詢] 文字方塊中，輸入 (或複製並貼上) 下列 Transact-SQL 查詢。

    ```T-SQL
    SELECT
       soh.OrderDate AS [Date],
       soh.SalesOrderNumber AS [Order],
       pps.Name AS [Subcat],
       pp.Name as [Product],
       SUM(sd.OrderQty) AS [Qty],
       SUM(sd.LineTotal) AS [LineTotal]
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
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'
    ```

7. (選擇性) 選取 [查詢設計工具] 按鈕。 查詢會顯示在以文字為基礎的 [查詢設計工具] 中。 在 [查詢設計工具] 工具列上，選取 ![ssrs_querydesigner_run](media/ssrs-querydesigner-run.png) [執行] 按鈕，以檢視查詢的結果。 在 AdventureWorks2016 資料庫中，顯示的資料集包含 4 個資料表中的 6 個欄位。 查詢會使用別名之類的 Transact-SQL 功能。 例如，SalesOrderHeader 資料表稱為 *soh*。

8. 選取 [確定] 結束 [查詢設計工具]。

9. 選取 [確定] 結束 [資料集屬性] 對話方塊。

[報表資料] 窗格會顯示 AdventureWorksDataset 資料集和欄位。

   ![ssrs_adventureworksdataset](media/ssrs-adventureworksdataset.png)

## <a name="next-steps"></a>後續步驟

您已經成功指定一項擷取報表資料的查詢。 之後，您將要建立報表版面配置。 繼續進行[第 4 課：將資料表新增至報表 &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)。

## <a name="see-also"></a>另請參閱

[查詢設計工具 &#40;SSRS&#41;](../reporting-services/report-data/query-design-tools-ssrs.md)
[SQL Server 連線類型 &#40;SSRS&#41;](../reporting-services/report-data/sql-server-connection-type-ssrs.md)
[教學課程：撰寫 Transact-SQL 陳述式](../t-sql/tutorial-writing-transact-sql-statements.md)
