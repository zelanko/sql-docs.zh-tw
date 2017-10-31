---
title: "SQL Server Reporting Services 中的矩形式樹狀結構圖和放射環狀圖表 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/31/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 5e15fa8674a09821becd437e78cfb0bb472e3bc8
ms.openlocfilehash: 50224e926c08951887a6423ab1c95eb7ac23a944
ms.contentlocale: zh-tw
ms.lasthandoff: 10/30/2017

---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>在 Reporting Services 中的矩形式樹狀結構圖和放射環狀圖表
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

SQL Server[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]矩形式樹狀結構圖和放射環狀視覺效果非常適合用來以視覺方式代表階層式資料。 這篇文章是如何新增樹狀圖或放射環狀圖到概觀[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]報表。 發行項也包含可協助您開始使用的 AdventureWorks 範例查詢。  
  
##  <a name="bkmk_treemap_chart"></a>矩形式樹狀結構圖圖表  

矩形式樹狀結構圖圖表區域分割成矩形，代表的不同層級和資料階層的相對大小。 樹狀圖類似樹上的樹枝，從主幹開始，分割為越來越小的分支。 每個矩形會分成較小的矩形代表階層中的下一個層級。 最上層的樹狀圖矩形的排列方式是以最大的矩形中，最小的矩形在右下角圖表左上角。  在矩形中，更高的下一層級也會從左上到右下排列矩形。  

例如，在以下範例樹狀圖的影像，southwest （西南） 的領域是最大而德國是最小值。 Southwest (西南) 當中，Road Bikes (公路自行車) 比 Mountain Bikes (登山自行車) 大。  
 
![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>插入樹狀圖圖表並設定範例 AdventureWorks 資料  
   
> [!NOTE]
> 您可以將圖表加入至報表之前，請建立資料來源和資料集。  範例資料和範例查詢，請參閱[範例 AdventureWorks 資料](#bkmk_sample_data)。  
  
1.  以滑鼠右鍵按一下設計介面，然後選取 **插入** > **圖表**。 選取**矩形式樹狀結構圖**圖示。

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
   
2.  重新調整圖表位置及大小。 若要使用的範例資料，5 英吋寬的圖表是不錯的起點。  
  
3.  從範例資料新增下列欄位：  
  
    * **值**: LineTotal
    * **類別目錄群組**（依下列順序）：
        1. CategoryName
        2. SubcategoryName
    * **數列群組**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  若要最佳化頁面大小的矩形式樹狀結構圖的一般形狀，請將圖例位置設定為底部。  
  
5.  若要新增顯示子類別目錄和行總計的工具提示，以滑鼠右鍵按一下**LineTotal**，然後選取**數列屬性**。  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     設定**工具提示**屬性設為下列值：  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    如需詳細資訊，請參閱[一系列 &#40; 上的 顯示工具提示報表產生器及 SSRS &#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  變更預設圖表標題**分類依領域銷售**。  
  
7.  顯示的標籤值數目會受字型大小、整體圖表區域大小，和特定矩形的大小影響。 若要查看更多標籤，變更**標籤字型**屬性**LineTotal**至**10pt**預設值是從**8pt**。  
  
  
##  <a name="bkmk_sunburst_chart"></a>放射環狀圖表  
 
在放射環狀圖表中，階層被以一系列的圓形。 在中心，是最高層級的階層和階層的較低層級會顯示在中心外環。  最低層級的階層在環形外部。  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>插入放射環狀圖表並設定範例 AdventureWorks 資料  
> [!NOTE] 
> 您可以將圖表加入至報表之前，請建立資料來源和資料集。 範例資料和範例查詢，請參閱[範例 AdventureWorks 資料](#bkmk_sample_data)。  
  
1.  以滑鼠右鍵按一下設計介面，然後選取**插入** > **圖表**。 選取**放射環狀圖**圖示。
     
     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2.  重新調整圖表位置及大小。 若要使用的範例資料，5 英吋寬的圖表是不錯的起點。  
  
3.  從範例資料新增下列欄位：  

    * **值**: LineTotal
    * **類別目錄群組**（依下列順序）：
        1. CategoryName
        2. SubcategoryName
        3. [Salesreasonname]
    * **數列群組**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  若要最佳化放射環狀圖表中的一般形狀的頁面大小，將圖例位置設定為底部。  
  
5.  變更預設圖表標題**分類銷售額與銷售原因的領域，**。  
  
6. 放射環狀圖的類別目錄群組值加入為標籤，設定 標籤屬性**看得見 = true**和**UseValueAsLabel = false**。<br /><br /> 顯示的標籤值會受字型大小、整體圖表區域大小，和特定矩形的大小影響。  若要查看更多標籤，變更**標籤字型**屬性**LineTotal**至**10pt**預設值是從**8pt**。

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7.  如果您想要不同的色彩範圍，請變更圖表的 **Palette** 屬性。  
    
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a>範例 AdventureWorks 資料  
 本節包含範例查詢及建立資料來源和資料集的基本步驟[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]。 如果您的報表已經包含資料來源和資料集，則可以略過本節。  
  
 查詢會傳回 AdventureWorks 銷售訂單詳細資料，包含銷售區域、 產品類別目錄、 產品子類別目錄和銷售原因資料。  
  
1.  **取得資料**。  
  
     此章節中的查詢根據 AdventureWorks 資料庫中，也就是可從 GitHub 下載： [AdventureWorks 2016 完整資料庫備份](https://github.com/Microsoft/sql-server-samples/releases)。  
  
  
2.  **建立資料來源**。  
  
    1.  在下**報表資料**，以滑鼠右鍵按一下**資料來源**，然後選取**加入資料來源**。  
  
    2.  選取 [使用內嵌於報表中的連接] 。  
  
    3.  連接類型 選取**Microsoft SQL Server**。  
  
    4.  輸入您的伺服器和資料庫的連接字串。 例如：  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5.  若要確認連線，請選取**測試連接**按鈕，然後再選取**確定**。  
  
     如需有關建立資料來源的詳細資訊，請參閱[新增並驗證資料連接 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **建立資料集**。  
  
    1. 在下**報表資料**，以滑鼠右鍵按一下**資料集**，然後選取**加入資料集**。  
  
    2. 選取 [使用內嵌在我的報表中的資料集] 。  
  
    3. 選取您建立的資料來源。  
  
    4. 選取**文字**查詢類型，然後複製並貼上下列查詢**查詢**文字方塊：  
  
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
  
     如需有關建立資料集的詳細資訊，請參閱[建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>另請參閱  
* [共用資料集設計檢視 &#40;報表產生器 &#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
* [上一系列 &#40; 顯示工具提示報表產生器及 SSRS &#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)
* [在 Power BI 中的教學課程： 矩形式樹狀結構圖](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)
* [樹狀圖：適用於 Office 的 Microsoft 研究資料視覺效果應用程式](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
<br>  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]


