---
title: 程式設計 AMO OLAP 基本物件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, OLAP
- OLAP [AMO]
- AMO, OLAP
ms.assetid: ad1c970e-c0cb-4687-9563-56ab62c2db5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c6532aadf691121851358e923fc218c08db0fd6a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205348"
---
# <a name="programming-amo-olap-basic-objects"></a>設計 AMO OLAP 基本物件的程式
  建立複雜的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 物件既簡單又直接，但是需要注意細節。 本主題說明 OLAP 基本物件的程式設計詳細資料。 本主題包含下列幾節：  
  
-   [維度物件](#Dim)  
  
-   [Cube 物件](#Cub)  
  
-   [MeasureGroup 物件](#MG)  
  
-   [Partition 物件](#Part)  
  
-   [Aggregation 物件](#AD)  
  
##  <a name="Dim"></a> 維度物件  
 若要管理或是處理維度，請設計 <xref:Microsoft.AnalysisServices.Dimension> 物件的程式。  
  
### <a name="creating-dropping-and-finding-a-dimension"></a>建立、卸除和尋找維度  
 建立 <xref:Microsoft.AnalysisServices.Dimension> 物件需要四個步驟來完成：  
  
1.  建立維度物件並擴展基本的屬性。  
  
     基本屬性是 Name、Dimension Type、Storage Mode、Data Source Binding、Attribute All Member Name 以及其他的維度屬性。  
  
     在建立維度之前，您應該確認維度尚未存在。 如果維度存在，則會先卸除維度並再重建。  
  
2.  建立定義維度的屬性。  
  
     必須先將每個屬性個別加入結構描述才能使用它 (請在範例程式碼結尾找到 CreateDataItem 方法)，然後就可以加入維度的屬性集合。  
  
     在所有的屬性中必須定義索引鍵和名稱。  
  
     應該將維度的主索引鍵屬性定義為 AttributeUsage.Key，以明確設定此屬性是存取維度的索引鍵。  
  
3.  建立使用者將存取以導覽維度的階層。  
  
     當您建立階層時，層級順序是由從上到下所建立的層級順序所定義。 最高層級會先加入階層的層級集合。  
  
4.  使用目前維度的 Update 方法來更新伺服器。  
  
 下列範例程式碼會建立 Product 維度。  
  
```  
static void CreateProductDimension(Database db, string datasourceName)  
{  
    // Create the Product dimension  
    Dimension dim = db.Dimensions.FindByName("Product");  
    if ( dim != null)  
       dim.Drop();  
    dim = db.Dimensions.Add("Product");  
    dim.Type = DimensionType.Products;  
    dim.UnknownMember = UnknownMemberBehavior.Hidden;  
    dim.AttributeAllMemberName = "All Products";  
    dim.Source = new DataSourceViewBinding(datasourceName);  
    dim.StorageMode = DimensionStorageMode.Molap;  
  
    #region Create attributes  
  
    DimensionAttribute attr;  
  
    attr = dim.Attributes.Add("Product Name");  
    attr.Usage = AttributeUsage.Key;  
    attr.Type = AttributeType.Product;  
    attr.OrderBy = OrderBy.Name;  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "EnglishProductName");  
  
    attr = dim.Attributes.Add("Product Line");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLine"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLineName");  
  
    attr = dim.Attributes.Add("Model Name");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ModelName"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Product Line"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Subcategory"));  
  
    attr = dim.Attributes.Add("Subcategory");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "ProductSubcategoryKey"));  
    attr.KeyColumns[0].NullProcessing = NullProcessing.UnknownMember;  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "EnglishProductSubcategoryName");  
    attr.AttributeRelationships.Add(new AttributeRelationship("Category"));  
  
    attr = dim.Attributes.Add("Category");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "ProductCategoryKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "EnglishProductCategoryName");  
  
    attr = dim.Attributes.Add("List Price");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ListPrice"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Size");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Size"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Weight");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Weight"));  
    attr.AttributeHierarchyEnabled = false;  
  
    #endregion  
  
    #region Create hierarchies  
  
    Hierarchy hier;  
  
    hier = dim.Hierarchies.Add("Product Model Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    hier = dim.Hierarchies.Add("Product Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Product Name";  
  
    hier = dim.Hierarchies.Add("Product Model Lines");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Product Line";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    #endregion  
  
    dim.Update();  
}  
  
static DataItem CreateDataItem(DataSourceView dsv, string tableName, string columnName)  
{  
    DataTable dataTable = ((DataSourceView)dsv).Schema.Tables[tableName];  
    DataColumn dataColumn = dataTable.Columns[columnName];  
    return new DataItem(tableName, columnName,  
        OleDbTypeConverter.GetRestrictedOleDbType(dataColumn.DataType));  
}  
  
```  
  
### <a name="processing-a-dimension"></a>處理維度  
 處理維度就像使用 <xref:Microsoft.AnalysisServices.Dimension> 物件的 Process 方法一樣簡單。  
  
 處理維度有可能會影響所有使用維度的 Cube。 如需處理選項的詳細資訊，請參閱[處理的物件&#40;XMLA&#41; ](../../xmla/xml-elements-objects.md)並[多維度模型物件處理](../processing-a-multidimensional-model-analysis-services.md)。  
  
 下列程式碼在提供的資料庫之所有維度中執行累加式更新：  
  
```  
static void UpdateAllDimensions(Database db)  
{  
    foreach (Dimension dim in db.Dimensions)  
        dim.Process(ProcessType.ProcessUpdate);  
}  
```  
  
##  <a name="Cub"></a> Cube 物件  
 若要管理或是處理 Cube，請設計 <xref:Microsoft.AnalysisServices.Cube> 物件的程式。  
  
### <a name="creating-dropping-and-finding-a-cube"></a>建立、卸除和尋找 Cube  
 管理 Cube 類似於管理維度。 建立 <xref:Microsoft.AnalysisServices.Cube> 物件需要四個步驟來完成：  
  
1.  建立 Cube 物件並擴展基本屬性。  
  
     基本屬性是 Name、Storage Mode、Data Source Binding、Default Measure、以及其他的 Cube 屬性。  
  
     在建立 Cube 之前，您應該確認 Cube 不存在。 在此範例中，如果 Cube 存在，會先卸除 Cube 後再重建。  
  
2.  加入 Cube 的維度。  
  
     維度會加入資料庫目前的 Cube 維度集合，在 Cube 中的維度是資料庫維度集合的參考。 每個維度必須個別對應至 Cube。 在範例中，對應的維度提供：資料庫維度的「內部識別碼」、Cube 中維度的「名稱」以及 Cube 中具名維度的「識別碼」。  
  
     在範例程式碼中，請注意 "Date" 維度一共加入三次，每次都使用不同的 Cube 維度名稱加入：Date、Ship Date、Delivery Date。 這些維度稱為「角色扮演」維度。 基底維度是相同的 (Date)，但是在事實資料表中，會以不同的「角色」(Order Date、Ship Date、Delivery Date) 使用維度，請參閱本文稍後的「建立、卸除和尋找 MeasureGroup」，以了解如何定義「角色扮演」維度。  
  
3.  建立使用者將存取以瀏覽 Cube 資料的量值群組。  
  
     量值群組建立將在本文稍後的「建立、卸除和尋找 MeasureGroup」中說明。 此範例以不同的方法來包裝量值群組建立，每個量值群組使用一個方法來包裝。  
  
4.  使用目前 Cube 的 Update 方法來更新伺服器。  
  
     更新方法是與 Update 選項 ExpandFull 搭配使用，以確定完全更新伺服器中的所有物件。  
  
 下列程式碼範例會建立 Adventure Works Cube 的一部分。 程式碼範例並未建立包含在 Adventure Works Analysis Services 專案範例中的所有維度或量值群組。  
  
```  
static void CreateAdventureWorksCube(Database db, string datasourceName)  
{  
    // Create the Adventure Works cube  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    if ( cube != null)  
       cube.Drop();  
    db.Cubes.Add("Adventure Works");  
    cube.DefaultMeasure = "[Reseller Sales Amount]";  
    cube.Source = new DataSourceViewBinding(datasourceName);  
    cube.StorageMode = StorageMode.Molap;  
  
    #region Create cube dimensions  
  
    Dimension dim;  
  
    dim = db.Dimensions.GetByName("Date");  
    cube.Dimensions.Add(dim.ID, "Date", "Order Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Ship Date",  
        "Ship Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Delivery Date",  
        "Delivery Date Key - Dim Time");  
  
    dim = db.Dimensions.GetByName("Customer");  
    cube.Dimensions.Add(dim.ID);  
  
    dim = db.Dimensions.GetByName("Reseller");  
    cube.Dimensions.Add(dim.ID);  
    #endregion  
  
    #region Create measure groups  
  
    CreateSalesReasonsMeasureGroup(cube);  
    CreateInternetSalesMeasureGroup(cube);  
    CreateResellerSalesMeasureGroup(cube);  
    CreateCustomersMeasureGroup(cube);  
    CreateCurrencyRatesMeasureGroup(cube);  
  
    #endregion  
  
    cube.Update(UpdateOptions.ExpandFull);  
}  
```  
  
### <a name="processing-a-cube"></a>處理 Cube  
 處理 Cube 就像使用 <xref:Microsoft.AnalysisServices.Cube> 物件的 Process 方法一樣簡單。 處理 Cube 也會處理 Cube 中的所有量值群組，以及量值群組中的所有資料分割。 在 Cube 中，資料分割是可以處理的唯一物件，就處理的目的而言，量值群組只是資料分割的容器。 處理 Cube 的指定類型會傳播到資料分割。 在內部處理 Cube 和量值群組會解析成維度與資料分割的處理。  
  
 如需處理選項的詳細資訊，請參閱[處理的物件&#40;XMLA&#41;](../../xmla/xml-elements-objects.md)，以及[多維度模型物件處理](../processing-a-multidimensional-model-analysis-services.md)。  
  
 下列程式碼將會在指定資料庫中的所有 Cube 上執行完整的處理：  
  
```  
foreach (Cube cube in db.Cubes)  
             cube.Process(ProcessType.ProcessFull);  
     }  
```  
  
##  <a name="MG"></a>MeasureGroup 物件  
 若要管理或是處理量值群組，請設計 <xref:Microsoft.AnalysisServices.MeasureGroup> 物件的程式。  
  
### <a name="creating-dropping-and-finding-a-measuregroup"></a>建立、卸除和尋找 MeasureGroup  
 管理量值群組類似於管理維度和 Cube。 您可以用下列步驟來完成 <xref:Microsoft.AnalysisServices.MeasureGroup> 物件的建立：  
  
1.  建立量值群組物件並擴展基本的屬性。  
  
     基本屬性包括「名稱」、「儲存模式」、「處理模式」、「預設量值」以及其他量值群組屬性。  
  
     在建立量值群組之前，請先確認量值群組不存在。 在以下範例程式碼中，如果量值群組存在，則會先卸除量值群組後再重新建立。  
  
2.  建立量值群組的量值。 對於所建立的每個量值，會指派下列屬性：名稱、彙總函式、來源資料行、格式化字串。 也可以指派其他屬性。 請注意，在以下範例程式碼中，CreateDataItem 方法會將資料行加入結構描述中。  
  
3.  加入量值群組的維度。  
  
4.  維度會從父 Cube 維度集合加入目前的量值群組維度集合。 只要維度一加入量值群組維度集合，事實資料表的索引鍵資料行就可以對應到維度，這樣便可透過維度瀏覽量值群組。  
  
     在以下範例程式碼中，請參閱 "Mapping dimension and key column from fact table" 之下的程式碼行。 透過將不同的 Surrogate 索引鍵連接到不同名稱之下的相同維度，以實作角色扮演維度。 對於每個角色扮演維度 (Date、Ship Date、Delivery Date)，會有不同的 Surrogate 索引鍵連結到它 (OrderDateKey、ShipDateKey、DueDateKey)。 所有索引鍵都是來自事實資料表 FactInternetSales。  
  
5.  加入量值群組的設計資料分割。  
  
     在以下範例程式碼中，會將資料分割建立包裝在一個方法中。  
  
6.  使用目前量值群組的 Update 方法來更新伺服器。  
  
     在以下範例程式碼中，當更新 Cube 時，會更新所有的量值群組。  
  
 下列範例程式碼將建立包含在 Adventure Works Analysis Services 專案範例的 InternetSales 量值群組。  
  
```  
static void CreateInternetSalesMeasureGroup(Cube cube)  
{  
    // Create the Internet Sales measure group  
    Database db = cube.Parent;  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Internet Sales");  
    if ( mg != null)  
       mg.Drop();  
    mg = cube.MeasureGroups.Add("Internet Sales");  
    mg.StorageMode = StorageMode.Molap;  
    mg.ProcessingMode = ProcessingMode.LazyAggregations;  
    mg.Type = MeasureGroupType.Sales;  
  
    #region Create measures  
  
    Measure meas;  
  
    meas = mg.Measures.Add("Internet Sales Amount");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesAmount");  
  
    meas = mg.Measures.Add("Internet Order Quantity");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderQuantity");  
  
    meas = mg.Measures.Add("Internet Unit Price");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Visible = false;  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "UnitPrice");  
  
    meas = mg.Measures.Add("Internet Total Product Cost");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    //meas.MeasureExpression = "[Internet Total Product Cost] * [Average Rate]";  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "TotalProductCost");  
  
    meas = mg.Measures.Add("Internet Order Count");  
    meas.AggregateFunction = AggregationFunction.Count;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey");  
  
    #endregion  
  
    #region Create measure group dimensions  
  
    CubeDimension cubeDim;  
    RegularMeasureGroupDimension regMgDim;  
    ManyToManyMeasureGroupDimension mmMgDim;  
    MeasureGroupAttribute mgAttr;  
  
    //   Mapping dimension and key column from fact table  
    //      > select dimension and add it to the measure group  
    cubeDim = cube.Dimensions.GetByName("Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
  
    //      > add key column from dimension and map it with   
    //        the surrogate key in the fact table  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);   // this is dimension key column  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderDateKey"));   // this surrogate key in fact table  
  
    cubeDim = cube.Dimensions.GetByName("Ship Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ShipDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Delivery Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "DueDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Customer");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Full Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CustomerKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Product");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Product Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Source Currency");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Currency").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CurrencyKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Sales Reason");  
    mmMgDim = new ManyToManyMeasureGroupDimension();  
    mmMgDim.CubeDimensionID = cubeDim.ID;  
    mmMgDim.MeasureGroupID = cube.MeasureGroups.GetByName("Sales Reasons").ID;  
    mg.Dimensions.Add(mmMgDim);  
  
    cubeDim = cube.Dimensions.GetByName("Internet Sales Order Details");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Sales Order Key").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderNumber"));  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderLineNumber"));  
  
    #endregion  
  
    #region Create partitions  
  
    CreateInternetSalesMeasureGroupPartitions( mg)  
  
    #endregion  
}  
```  
  
### <a name="processing-a-measure-group"></a>處理量值群組  
 處理量值群組就像使用 <xref:Microsoft.AnalysisServices.MeasureGroup> 物件的 Process 方法一樣簡單。 處理量值群組將處理所有屬於量值群組的資料分割。 在內部處理量值群組會解析成處理維度與資料分割。 請參閱[處理資料分割](#ProcPart)本文件中。  
  
 如需處理選項的詳細資訊，請參閱[處理的物件&#40;XMLA&#41;](../../xmla/xml-elements-objects.md)，以及[多維度模型物件處理](../processing-a-multidimensional-model-analysis-services.md)。  
  
 下列程式碼將在提供之 Cube 的所有量值群組中執行完整的處理。  
  
```  
static void FullProcessAllMeasureGroups(Cube cube)  
{  
    foreach (MeasureGroup mg in cube.MeasureGroups)  
        mg.Process(ProcessType.ProcessFull);  
}  
```  
  
##  <a name="Part"></a>分割區物件  
 若要管理或是處理資料分割，請設計 <xref:Microsoft.AnalysisServices.Partition> 物件的程式。  
  
### <a name="creating-dropping-and-finding-a-partition"></a>建立、卸除和尋找資料分割  
 資料分割是可用兩個步驟建立的簡單物件。  
  
1.  建立資料分割物件並擴展基本屬性。  
  
     基本屬性是「名稱」、「儲存模式」、資料分割來源、「配量」以及其他量值群組屬性。 資料分割來源會為目前的資料分割定義 SQL Select 陳述式。 「配量」是一種 MDX 運算式，用以指定 Tuple 或是集合，來分隔包含在目前資料分割中的父量值群組之維度的一部分。 對於 MOLAP 資料分割，會在每次處理資料分割時，自動決定配量。  
  
     在建立資料分割之前，您應該確認資料分割不存在。 在以下範例程式碼中，如果資料分割存在，則會先卸除它後再重新建立。  
  
2.  使用目前資料分割的 Update 方法來更新伺服器。  
  
     在以下範例程式碼中，更新 Cube 時，會更新所有的資料分割。  
  
 下列程式碼範會建立 'InternetSales' 量值群組的資料分割。  
  
```  
static void CreateInternetSalesMeasureGroupPartitions(MeasureGroup mg)  
{  
    Partition part;  
    part = mg.Partitions.FindByName("Internet_Sales_184");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_184");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey <= '184'");  
    part.Slice = "[Date].[Calendar Year].&[2001]";  
    part.Annotations.Add("LastOrderDateKey", "184");  
  
    part = mg.Partitions.FindByName("Internet_Sales_549");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_549");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '184' AND OrderDateKey <= '549'");  
    part.Slice = "[Date].[Calendar Year].&[2002]";  
    part.Annotations.Add("LastOrderDateKey", "549");  
  
    part = mg.Partitions.FindByName("Internet_Sales_914");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_914");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '549' AND OrderDateKey <= '914'");  
    part.Slice = "[Date].[Calendar Year].&[2003]";  
    part.Annotations.Add("LastOrderDateKey", "914");  
}  
```  
  
###  <a name="ProcPart"></a> 處理資料分割  
 處理資料分割就像使用 <xref:Microsoft.AnalysisServices.Partition> 物件的 Process 方法一樣簡單。  
  
 如需處理選項的詳細資訊，請參閱[處理的物件&#40;XMLA&#41; ](../../xmla/xml-elements-objects.md)並[多維度模型物件處理](../processing-a-multidimensional-model-analysis-services.md)。  
  
 下列程式碼範例在指定量值群組的所有資料分割中執行完整的處理。  
  
```  
static void FullProcessAllPartitions(MeasureGroup mg)  
{  
    foreach (Partition part in mg.Partitions)  
        part.Process(ProcessType.ProcessFull);  
}  
```  
  
### <a name="merging-partitions"></a>合併資料分割  
 合併資料分割表示執行任何將促使兩個或更多資料分割變成一個資料分割的作業。  
  
 合併資料分割是 <xref:Microsoft.AnalysisServices.Partition> 物件的方法。 這個命令將一或多個來源資料分割的資料合併至目標資料分割中，然後刪除來源資料分割。  
  
 只能合併符合下列所有準則的資料分割：  
  
-   磁碟分割位於相同的量值群組。  
  
-   資料分割是儲存在相同的模式中 (MOLAP、HOLAP 和 ROLAP)。  
  
-   資料分割會在相同的伺服器上，如果在相同的伺服器上，即可合併遠端資料分割。  
  
 不像在舊版中，在[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]就不需要所有來源資料分割都有相同的彙總設計。  
  
 目標資料分割之彙總結果集在執行合併命令之前的狀態，是相同組的彙總。  
  
 下列程式碼範例會合併指定量值群組的所有資料分割。 資料分割會合併到量值群組的第一個資料分割。  
  
```  
static void MergeAllPartitions(MeasureGroup mg)  
{  
    if (mg.Partitions.Count > 1)  
    {  
        Partition[] partArray = new Partition[mg.Partitions.Count - 1];  
        for (int i = 1; i < mg.Partitions.Count; i++)  
            partArray[i - 1] = mg.Partitions[i];  
        mg.Partitions[0].Merge(partArray);  
        //To have last changes in the server reflected in AMO  
        mg.Refresh();  
    }  
```  
  
##  <a name="AD"></a>Aggregation 物件  
 若要設計彙總並將它套用至一或多個資料分割，請設計 <xref:Microsoft.AnalysisServices.Aggregation> 物件的程式。  
  
### <a name="creating-and-dropping-aggregations"></a>建立和捨棄彙總  
 您可以使用 <xref:Microsoft.AnalysisServices.AggregationDesign> 物件的 DesignAggregations 方法，輕鬆地建立彙總並將它們指派到量值群組或是資料分割。 <xref:Microsoft.AnalysisServices.AggregationDesign> 物件是資料分割的個別物件，<xref:Microsoft.AnalysisServices.AggregationDesign> 物件是包含在 <xref:Microsoft.AnalysisServices.MeasureGroup> 物件中。 可以將彙總設計至指定的最佳化層級 (0 到 100) 或是指定的儲存層級 (位元組)。 多個磁碟分割可以使用相同的彙總設計。  
  
 下列程式碼範例會為提供的量值群組其所有資料分割建立彙總。 會捨棄磁碟分割中任何現有的彙總。  
  
```  
static public String DesignAggregationsOnPartitions(MeasureGroup mg, double optimizationWanted, double maxStorageBytes)  
{  
    double optimization = 0;  
    double storage = 0;  
    long aggCount = 0;  
    bool finished = false;  
    AggregationDesign ad = null;  
    String aggDesignName;  
    String AggregationsDesigned = "";  
    aggDesignName = mg.AggregationPrefix + "_" + mg.Name;  
    ad = mg.AggregationDesigns.Add();  
    ad.Name = aggDesignName;  
    ad.InitializeDesign();  
    while ((!finished) && (optimization < optimizationWanted) && (storage < maxStorageBytes))  
    {  
        ad.DesignAggregations(out optimization, out storage, out aggCount, out finished);  
    }  
    ad.FinalizeDesign();  
    foreach (Partition part in mg.Partitions)  
    {  
        part.AggregationDesignID = ad.ID;  
        AggregationsDesigned += aggDesignName + " = " + aggCount.ToString() + " aggregations designed\r\n\tOptimization: " + optimization.ToString() + "/" + optimizationWanted.ToString() + "\n\r\tStorage: " + storage.ToString() + "/" + maxStorageBytes.ToString() + " ]\n\r";  
     }  
     return AggregationsDesigned;  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices>   
 [AMO 類別簡介](amo-classes-introduction.md)   
 [AMO OLAP 類別](amo-olap-classes.md)   
 [邏輯架構&#40;Analysis Services-多維度資料&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [資料庫物件&#40;Analysis Services-多維度資料&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [多維度模型物件處理](../processing-a-multidimensional-model-analysis-services.md)  
  
  
