---
title: SQL Server Reporting Services 中的樹狀圖與放射環狀圖 | Microsoft Docs
ms.date: 08/31/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c255369e8292aa2b7275a58d5e8375890153a5aa
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/16/2018
ms.locfileid: "51814101"
---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>Reporting Services 中的樹狀圖與放射環狀圖
[!INCLUDE[feedback-stackoverflow-msdn-connect-md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]
SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 樹狀圖和放射環狀視覺效果是以視覺呈現階層資料的絕佳方式。 本文是如何新增樹狀圖或放射環狀圖到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表的概觀。 本文也包含可協助您開始使用的 AdventureWorks 範例查詢。  
  
##  <a name="bkmk_treemap_chart"></a> 樹狀圖圖表  

樹狀圖圖表會將圖表區域分割成矩形，該矩形代表資料階層的不同層級與相對大小。 樹狀圖類似樹上的樹枝，從主幹開始，分割為越來越小的分支。 每個矩形會分成較小的矩形，表示階層中的下一個層級。 最上層的樹狀圖矩形的排列方式是，最大的矩形排列在圖表左上角，最小的矩形在右下角。  在矩形中，更高的下一層級也會從左上到右下排列矩形。  

例如，在以下範例樹狀圖的影像中，Southwest (西南) 的領域最大，而 Germany (德國) 最小。 Southwest (西南) 當中，Road Bikes (公路自行車) 比 Mountain Bikes (登山自行車) 大。  
 
![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>插入樹狀圖圖表並設定範例 Adventureworks 資料  
   
> [!NOTE]
> 在您新增圖表到報表前，請先建立資料來源和資料集。  如需範例資料和範例查詢，請參閱[範例 AdventureWorks 資料](#bkmk_sample_data)。  
  
1.  以滑鼠右鍵按一下設計介面，然後選取 插入 > 圖表。 選取**樹狀圖**圖示。

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
   
2.  重新調整圖表位置及大小。 若要搭配範例資料使用，5 英吋寬的圖表是不錯的起點。  
  
3.  從範例資料新增下列欄位：  
  
    * **值**：LineTotal
    * **類別目錄群組** (依下列順序)：
        1. CategoryName
        2. SubcategoryName
    * **數列群組**：TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  若要對樹狀圖的一般形狀最佳化頁面大小，請將圖例位置設定為底部。  
  
5.  若要新增顯示子類別和總金額的工具提示，以滑鼠右鍵按一下 [LineTotal] 然後選取 [數列屬性]。  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     將 **Tooltip** 屬性設為下列值：  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    如需詳細資訊，請參閱[在數列上顯示工具提示 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)。  
  
6.  將預設圖表標題變更為「按領域分類的銷售量」。  
  
7.  顯示的標籤值數目會受字型大小、整體圖表區域大小，和特定矩形的大小影響。 若要看到更多標籤，將 **LineTotal** 的 **Label Font** 屬性從預設的 **8pt** 變更為 **10pt**。  
  
  
##  <a name="bkmk_sunburst_chart"></a> 放射環狀圖表  
 
在放射環狀圖表中，階層以一系列的圓形表示。 在中心是階層的最高層級，階層的較低層級則會顯示在中心之外的環。  最低層級的階層在環形外部。  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>插入放射環狀圖表並設定範例 Adventureworks 資料  
> [!NOTE] 
> 在您新增圖表到報表前，請先建立資料來源和資料集。 如需範例資料和範例查詢，請參閱[範例 AdventureWorks 資料](#bkmk_sample_data)。  
  
1.  以滑鼠右鍵按一下設計介面，然後選取 [插入] > [圖表]。 選取 [放射環狀圖] 圖示。
     
     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2.  重新調整圖表位置及大小。 若要搭配範例資料使用，5 英吋寬的圖表是不錯的起點。  
  
3.  從範例資料新增下列欄位：  

    * **值**：LineTotal
    * **類別目錄群組** (依下列順序)：
        1. CategoryName
        2. SubcategoryName
        3. SalesReasonName
    * **數列群組**：TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  若要對放射環狀圖表的一般形狀最佳化頁面大小，請將圖例位置設定為底部。  
  
5.  將預設圖表標題變更為「按領域分類的銷售量 (包含銷售原因)」。  
  
6. 若要新增類別群組的值到放射環狀圖作為標籤，請設定標籤屬性 **Visible=true** 和 **UseValueAsLabel=false**。<br /><br /> 顯示的標籤值會受字型大小、整體圖表區域大小，和特定矩形的大小影響。  若要看到更多標籤，將 **LineTotal** 的 **Label Font** 屬性從預設的 **8pt** 變更為 **10pt**。

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7.  如果您想要不同的色彩範圍，請變更圖表的 **Palette** 屬性。  
    
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a> 範例 AdventureWorks 資料  
 本節包含範例查詢及在 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 中建立資料來源和資料集的基本步驟。 如果報表已包含資料來源及資料集，您可以略過本節。  
  
 查詢會傳回 AdventureWorks 銷售訂單詳細資料，包含銷售區域、產品類別、產品子類別和銷售原因資料。  
  
1.  **取得資料**。  
  
     本節中的查詢是以 AdventureWorks 資料庫為基礎，該資料庫可從 GitHub：[AdventureWorks 2016 完整資料庫備份](https://github.com/Microsoft/sql-server-samples/releases)下載取得。  
  
  
2.  **建立資料來源**。  
  
    1.  在 [報表資料] 下，以右鍵按一下 [資料來源] 然後選取 [新增資料來源]。  
  
    2.  選取 [使用內嵌於報表中的連接] 。  
  
    3.  針對連線類型，選取 [Microsoft SQL Server]。  
  
    4.  輸入您的伺服器和資料庫的連接字串。 例如：  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5.  若要確認連線，請選取 [測試連線] 按鈕，然後選取 [確定]。  
  
     如需建立資料來源的詳細資訊，請參閱[新增及驗證資料連線 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
3.  **建立資料集**。  
  
    1. 在 [報表資料] 下，以右鍵按一下 [資料集] 然後選取 [新增資料集]。  
  
    2. 選取 [使用內嵌在我的報表中的資料集] 。  
  
    3. 選取您建立的資料來源。  
  
    4. 選取 [文字] 查詢類型，然後將下列查詢複製並貼上到 [查詢] 文字方塊；  
  
        ```  
        SELECT    Sales.SalesOrderHeader.SalesOrderID, Sales.SalesOrderHeader.OrderDate, Sales.SalesOrderDetail.SalesOrderDetailID, Sales.SalesOrderDetail.ProductID, Sales.SalesOrderDetail.LineTotal,   
                                 Sales.SalesOrderDetail.UnitPrice, Sales.SalesOrderDetail.OrderQty, Production.Product.Name, Production.Product.ProductNumber, Sales.SalesTerritory.TerritoryID, lower(Sales.SalesTerritory.Name) AS TerritoryName,   
                                 Production.ProductSubcategory.Name AS SubcategoryName, Production.ProductCategory.Name AS CategoryName, Sales.SalesReason.SalesReasonID, Sales.SalesReason.Name AS SalesReasonName  
        FROM            Sales.SalesOrderDetail INNER JOIN  
                                 Sales.SalesOrderHeader ON Sales.SalesOrderDetail.SalesOrderID = Sales.SalesOrderHeader.SalesOrderID INNER JOIN  
                                 Production.Product ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID INNER JOIN  
                                 Sales.SalesTerritory ON Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND   
                                 Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID INNER JOIN  
                                 Production.ProductSubcategory ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID INNER JOIN  
                                 Production.ProductCategory ON Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID INNER JOIN  
                                 Sales.SalesOrderHeaderSalesReason ON Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID INNER JOIN  
                                 Sales.SalesReason ON Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID  
        ```  
  
    5. 選取 [確定]。  
  
     如需建立資料集的詳細資訊，請參閱[建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)。  
  
  
## <a name="see-also"></a>另請參閱  
* [共用資料集設計檢視 &#40;報表產生器&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
* [在數列上顯示工具提示 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)
* [教學課程：Power BI 中的樹狀圖](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)
* [樹狀圖：適用於 Office 的 Microsoft 研究資料視覺效果應用程式](https://research.microsoft.com/projects/msrdatavis/treemap.aspx)  
<br>  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

