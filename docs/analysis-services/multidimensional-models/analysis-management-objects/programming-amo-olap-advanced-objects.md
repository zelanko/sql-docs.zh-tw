---
title: "設計 AMO OLAP 進階物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, OLAP
- OLAP [AMO]
- AMO, OLAP
ms.assetid: b75f35a7-32df-4f22-983d-324aa98e15a9
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dedfe7e17d6f8fd0be0bb769b9891880a83b2eba
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="programming-amo-olap-advanced-objects"></a>設計 AMO OLAP 進階物件的程式
  本主題說明 OLAP 進階物件的分析管理物件 (AMO) 程式設計詳細資料。 本主題包含下列幾節：  
  
-   [動作物件](#Action)  
  
-   [Kpi 物件](#KPI)  
  
-   [檢視方塊物件](#Persp)  
  
-   [ProactiveCaching 物件](#PC)  
  
-   [翻譯物件](#Transl)  
  
##  <a name="Action"></a>動作物件  
 動作類別是用以在瀏覽 Cube 的某些區域時，建立主動式回應。 動作物件可以使用 AMO 來定義，但是是從瀏覽資料的用戶端應用程式來使用這些物件。 動作可以屬於不同類型，而且必須據其類型來建立。 動作可以是：  
  
-   鑽研動作，該動作會傳回一組資料列，這些資料列表示動作發生所在之 Cube 中選定資料格的基礎資料。  
  
-   報表動作，該動作會從與動作發生所在之 Cube 中選定區段有關的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 內傳回報表。  
  
-   標準動作，該動作會傳回與動作發生所在之 Cube 中選定區段有關的動作元素 (URL、HTML、DataSet、RowSet 和其他元素)。  
  
 建立動作物件需要下列步驟：  
  
1.  建立衍生的動作物件並擴展基本屬性。  
  
     下列為基本屬性：動作類型、Cube 的目標類型或區段、可以使用動作之所在 Cube 的目標或特定區域、標題，以及標題是 MDX 運算式的位置。  
  
2.  擴展動作類型的特定屬性。  
  
     三種類型的動作各有不同的屬性，請參閱以下程式碼範例以了解參數。  
  
3.  將動作加入 Cube 集合並更新 Cube。 動作不是可更新的物件。  
  
 測試這個動作需要不同的程式應用程式。 您可以在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中測試動作。 首先，您必須安裝[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]範例，請參閱[處理多維度模型 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 下列範例程式碼將會從 Adventure Works Analysis Services 專案範例複寫三種不同的動作。 您可以區分這些動作，因為使用下列範例所介紹的這些動作，是以 "My" 開頭。  
  
```  
static public void CreateActions(Cube cube)  
{  
    #region Adding a drillthrough action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Reseller Details"))  
        cube.Actions.Remove("My Drillthrough Action",true);  
  
    //Create a Drillthrough action  
    DrillThroughAction dtaction = new DrillThroughAction("My Reseller Details", "My Drillthrough Action");  
  
    //Define the Action  
    dtaction.Type = ActionType.DrillThrough;  
    dtaction.TargetType = ActionTargetType.Cells;  
    dtaction.Target = "MeasureGroupMeasures(\"Reseller Sales\")";  
    dtaction.Caption = "My Drillthrough...";  
    dtaction.CaptionIsMdx = false;  
  
    #region create drillthrough action specifics  
    //Adding Drillthrough columns  
    //Adding Measure columns to the drillthrough  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Reseller Sales");  
    MeasureBinding mb1 = new MeasureBinding();  
    mb1.MeasureID = mg.Measures.FindByName( "Reseller Sales Amount").ID;  
    dtaction.Columns.Add(mb1);  
  
    MeasureBinding mb2 = new MeasureBinding();  
    mb2.MeasureID = mg.Measures.FindByName("Reseller Order Quantity").ID;  
    dtaction.Columns.Add(mb2);  
  
    MeasureBinding mb3 = new MeasureBinding();  
    mb3.MeasureID = mg.Measures.FindByName("Reseller Unit Price").ID;  
    dtaction.Columns.Add(mb3);  
  
    //Adding Dimension Columns to the drillthrough  
    CubeAttributeBinding cb1 = new CubeAttributeBinding();  
    cb1.CubeID = cube.ID;  
    cb1.CubeDimensionID = cube.Dimensions.FindByName("Reseller").ID;  
    cb1.AttributeID = "Reseller Name";  
    cb1.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb1);  
  
    CubeAttributeBinding cb2 = new CubeAttributeBinding();  
    cb2.CubeID = cube.ID;  
    cb2.CubeDimensionID = cube.Dimensions.FindByName("Product").ID;  
    cb2.AttributeID = "Product Name";  
    cb2.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb2);  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(dtaction);  
    #endregion  
  
    #region Adding a Standard action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My City Map"))  
        cube.Actions.Remove("My Action", true);  
  
    //Create a Drillthrough action  
    StandardAction stdaction = new StandardAction("My City Map", "My Action");  
  
    //Define the Action  
    stdaction.Type = ActionType.Url;  
    stdaction.TargetType = ActionTargetType.AttributeMembers;  
    stdaction.Target = "[Geography].[City]";  
    stdaction.Caption = "\"My View Map for \" + [Geography].[City].CurrentMember.Member_Caption + \"...\"";  
    stdaction.CaptionIsMdx = true;  
  
    #region create standard action specifics  
    stdaction.Expression = "\"http://maps.msn.com/home.aspx?plce1=\" + " +  
        "[Geography].[City].CurrentMember.Name + \",\" + " +  
        "[Geography].[State-Province].CurrentMember.Name + \",\" + " +  
        "[Geography].[Country].CurrentMember.Name + " +  
        "\"&regn1=\" + " +  
        "Case " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Australia] " +  
                "Then \"3\" " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Canada] " +  
                "Or [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[United States] " +  
                "Then \"0\" " +  
                "Else \"1\" " +  
        "End ";  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(stdaction);  
  
    #endregion  
  
    #region Adding a Reporting action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Sales Reason Comparisons"))  
        cube.Actions.Remove("My Report Action", true);  
  
    //Create a Report action  
    ReportAction rsaction = new ReportAction("My Sales Reason Comparisonsp", "My Report Action");  
  
    //Define the Action  
    rsaction.Type = ActionType.Report;  
    rsaction.TargetType = ActionTargetType.AttributeMembers;  
    rsaction.Target = "[Product].[Category]";  
    rsaction.Caption = "\"My Sales Reason Comparisons for \" + [Product].[Category].CurrentMember.Member_Caption + \"...\"";  
    rsaction.CaptionIsMdx = true;  
  
    #region create Report action specifics  
    rsaction.ReportServer = "MyRSSamplesServer";  
    rsaction.Path = "ReportServer?/AdventureWorks Sample Reports/Sales Reason Comparisons";  
    rsaction.ReportParameters.Add("ProductCategory", "UrlEscapeFragment( [Product].[Category].CurrentMember.UniqueName )");  
    rsaction.ReportFormatParameters.Add("rs:Command", "Render");  
    rsaction.ReportFormatParameters.Add("rs:Renderer", "HTML5");  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(rsaction);  
  
    #endregion  
}  
```  
  
##  <a name="KPI"></a>Kpi 物件  
 關鍵效能指標 (KPI) 是用來評估商務成就的計算集合，這些計算與 Cube 中的量值群組相關聯。 <xref:Microsoft.AnalysisServices.Kpi> 物件可以使用 AMO 來定義，但是是從瀏覽資料的用戶端應用程式來使用這些物件。  
  
 建立 <xref:Microsoft.AnalysisServices.Kpi> 物件需要下列步驟：  
  
1.  建立 <xref:Microsoft.AnalysisServices.Kpi> 物件並擴展基本屬性。  
  
     下列是基本屬性清單：「描述」、「顯示資料夾」、「相關聯的量值群組」以及「值」。 「顯示資料夾」會告訴用戶端應用程式一般使用者在哪裡可以找到 KPI。 「相關聯的量值群組」指出應參考所有 MDX 計算之量值群組。 「值」將效能指標的實際值顯示成 MDX 運算式。  
  
2.  定義 KPI 標記：目標、狀態和趨勢。  
  
     指標是應該在 -1 到 1 之間評估的 MDX 運算式，但為定義指標值範圍的瀏覽應用程式。  
  
3.  當您在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中瀏覽 KPI 時，會將小於 -1 的值視為 -1，並將大於 1 的值視為 1。  
  
4.  定義圖形影像。  
  
     圖形影像是字串值，可做為用戶端應用程式中的參考使用，以識別要顯示之影像的正確集合。 圖形影像字串也會定義顯示函數的行為。 通常範圍會分成奇數的狀態、從良好到不良，並且會從該集合指派每個狀態一個影像。  
  
     如果您使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 瀏覽 KPI，則視名稱而定，會將指標範圍分成三個狀態或是五個狀態。 此外，有些反轉範圍的名稱，-1 代表「良好」，而 1 則代表「不良」。 在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中，範圍中的三個狀態如下所示：  
  
    -   不良 = -1 到 -0.5  
  
    -   沒有問題 = -0.4999 to -0.4999  
  
    -   良好 = 0.50 到 1  
  
     在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中，範圍內有五個狀態，如下所示：  
  
    -   不良 = -1 到 -0.75  
  
    -   危險 = -0.7499 到 -0.25  
  
    -   沒有問題 = -0.2499 到 0.2499  
  
    -   引發 = 0.25 到 0.7499  
  
    -   良好 = 0.75 到 1  
  
 下表列出與其影像關聯之用法、名稱和狀態數目。  
  
|影像使用量|影像名稱|狀態的數目|  
|-----------------|----------------|----------------------|  
|狀態|圖形|3|  
|狀態|號誌燈|3|  
|狀態|道路標誌|3|  
|狀態|量測計|3|  
|狀態|反向量測計|5|  
|狀態|溫度計|3|  
|狀態|圓柱|3|  
|狀態|笑臉|3|  
|狀態|變異箭頭|3|  
|趨勢|標準箭頭|3|  
|趨勢|狀態箭頭|3|  
|趨勢|反向狀態箭頭|5|  
|趨勢|笑臉|3|  
  
1.  將 KPI 加入 Cube 集合並更新 Cube，因為 KPI 不是可更新的物件。  
  
 測試 KPI 需要不同的程式應用程式。 您可以在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中測試您的 KPI。  
  
 下列範例程式碼會為包括在 Adventure Works Analysis Services 專案範例中的 Adventure Works Cube，在 "Financial Perpective/Grow Revenue" 資料夾中建立 KPI。  
  
```  
static public void CreateKPIs(Cube cube)  
{  
    Kpi kpi = cube.Kpis.Add("My Internet Revenue", "My Internet Revenue");  
    kpi.Description = "(My) Revenue achieved through direct sales via Interner";  
    kpi.DisplayFolder = "\\Financial Perspective\\Grow Revenue";  
    kpi.AssociatedMeasureGroupID = "Internet Sales";  
    kpi.Value = "[Measures].[Internet Sales Amount]";  
    #region Goal  
    kpi.Goal = "Case" +  
               "     When IsEmpty" +  
               "          (" +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          )" +   
               "     Then [Measures].[Internet Sales Amount]" +  
               "     Else 1.10 *" +  
               "          (" +  
               "            [Measures].[Internet Sales Amount]," +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          ) " +  
               " End";  
    #endregion  
    #region Status  
    kpi.Status = "Case" +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .95 " +  
                 "   Then 1 " +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) <  .95 " +  
                 "        And  " +  
                 "        KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .85 " +  
                 "   Then 0 " +  
                 "   Else -1 " +  
                 "End";  
    #endregion  
    #region Trend  
    kpi.Trend = "Case " +  
                "    When VBA!Abs " +  
                "         ( " +  
                "           KpiValue( \"Internet Revenue\" ) -  " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           ) / " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           )   " +  
                "         ) <=.02  " +  
                "    Then 0 " +  
                "    When KpiValue( \"Internet Revenue\" ) -  " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         ) / " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         )  >.02 " +  
                "    Then 1 " +  
                "    Else -1 " +  
                "End";  
    #endregion  
    kpi.TrendGraphic = "Standard Arrow";  
    kpi.StatusGraphic = "Cylinder";  
}.  
```  
  
##  <a name="Persp"></a>檢視方塊物件  
 <xref:Microsoft.AnalysisServices.Perspective> 物件可以使用 AMO 來定義，但是是從瀏覽資料的用戶端應用程式來使用這些物件。  
  
 建立 <xref:Microsoft.AnalysisServices.Perspective> 物件需要下列步驟：  
  
1.  建立 <xref:Microsoft.AnalysisServices.Perspective> 物件並擴展基本屬性。  
  
     下列是基本屬性的清單：「名稱」、「預設量值」、「描述」和註解。  
  
2.  從一般使用者應該看到的父 Cube，加入所有的物件。  
  
     加入 Cube 維度 (屬性和階層)、量值群組 (量值和量值群組)、動作、KPI 和計算。  
  
3.  將檢視方塊加入 Cube 集合並更新 Cube，因為檢視方塊不是可更新的物件。  
  
 測試檢視方塊需要不同的程式應用程式。 您可以在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中測試您的檢視方塊。  
  
 下列程式碼範會為提供的 Cube 建立名為 "Direct Sales" 的檢視方塊。  
  
```  
static public void CreatePerspectives(Cube cube)  
{  
    Perspective perspective = cube.Perspectives.Add("Direct Sales", "Direct Sales");  
    CubeDimension dim1 = cube.Dimensions.GetByName("Date");  
    PerspectiveDimension pdim1 = perspective.Dimensions.Add(dim1.DimensionID);  
    pdim1.Attributes.Add("Date");  
    pdim1.Attributes.Add("Calendar Year");  
    pdim1.Attributes.Add("Fiscal Year");  
    pdim1.Attributes.Add("Calendar Quarter");  
    pdim1.Attributes.Add("Fiscal Quarter");  
    pdim1.Attributes.Add("Calendar Month Number");  
    pdim1.Attributes.Add("Fiscal Month Number");  
    pdim1.Hierarchies.Add("Calendar Time");  
    pdim1.Hierarchies.Add("Fiscal Time");  
  
    CubeDimension dim2 = cube.Dimensions.GetByName("Product");  
    PerspectiveDimension pdim2 = perspective.Dimensions.Add(dim2.DimensionID);  
    pdim2.Attributes.Add("Product Name");  
    pdim2.Attributes.Add("Product Line");  
    pdim2.Attributes.Add("Model Name");  
    pdim2.Attributes.Add("List Price");  
    pdim2.Attributes.Add("Size");  
    pdim2.Attributes.Add("Weight");  
    pdim2.Hierarchies.Add("Product Model Categories");  
    pdim2.Hierarchies.Add("Product Categories");  
  
    PerspectiveMeasureGroup pmg = perspective.MeasureGroups.Add("Internet Sales");  
    pmg.Measures.Add("Internet Sales Amount");  
    pmg.Measures.Add("Internet Order Quantity");  
    pmg.Measures.Add("Internet Unit Price");  
  
    pmg = perspective.MeasureGroups.Add("Reseller Sales");  
    pmg.Measures.Add("Reseler Sales Amount");  
    pmg.Measures.Add("Reseller Order Quantity");  
    pmg.Measures.Add("Reseller Unit Price");  
  
    PerspectiveAction pact = perspective.Actions.Add("Drillthrough Action");  
  
    PerspectiveKpi pkpi = perspective.Kpis.Add("Internet Revenue");  
    Cube.Update();  
}  
```  
  
##  <a name="PC"></a>ProactiveCaching 物件  
 <xref:Microsoft.AnalysisServices.ProactiveCaching> 物件可由 AMO 定義。  
  
 建立 <xref:Microsoft.AnalysisServices.ProactiveCaching> 物件需要下列步驟：  
  
1.  建立 <xref:Microsoft.AnalysisServices.ProactiveCaching> 物件。  
  
     沒有要定義的基本屬性。  
  
2.  加入快取規格。  
  
|規格|Description|  
|-------------------|-----------------|  
|AggregationStorage|彙總的儲存類型。<br /><br /> 只適用於資料分割。 在維度上它必須是**規則。**|  
|SilenceInterval|在 MOLAP 影像處理開始之前，快取存在的最少時間量。|  
|延遲|最早通知與終結 MOLAP 影像之間的時間量。|  
|SilenceOverrideInterval|在 MOLAP 影像處理無條件介入之後，初始通知後的時間。|  
|ForceRebuildInterval|在 MOLAP 影像處理無條件開始之後 (沒有通知) 的時間 (在捨棄全新的 MOLAP 影像之後開始)。|  
|OnlineMode|當 MOLAP 影像是可用的。<br /><br /> 可以是**即時運算**或**OnCacheComplete**。|  
  
1.  將 <xref:Microsoft.AnalysisServices.ProactiveCaching> 物件加入父集合。 您將需要更新父系，因為 <xref:Microsoft.AnalysisServices.ProactiveCaching> 不是可更新的物件。  
  
 下列程式碼範例會在所有資料分割上建立 <xref:Microsoft.AnalysisServices.ProactiveCaching> 物件，這些資料分割是來自指定資料庫的 Adventure Works Cube 中之「網際網路銷售」量值群組。  
  
```  
static public void SetProactiveCachingSettings(Database db)  
{  
    ProactiveCaching pc;  
    if (db.Cubes.ContainsName("Adventure Works") && db.Cubes.FindByName("Adventure Works").MeasureGroups.ContainsName("Internet Sales"))  
    {  
        ProactiveCachingTablesBinding pctb;  
        TableNotification tn;  
  
        MeasureGroup mg = db.Cubes.FindByName("Adventure Works").MeasureGroups.FindByName("Internet Sales");  
        foreach(Partition part in mg.Partitions)  
        {  
            pc = new ProactiveCaching();  
            pc.AggregationStorage = ProactiveCachingAggregationStorage.MolapOnly;  
            pc.SilenceInterval = TimeSpan.FromSeconds(10);  
            pc.Latency = TimeSpan.FromSeconds(-1);  
            pc.SilenceOverrideInterval = TimeSpan.FromMinutes(10);  
            pc.ForceRebuildInterval = TimeSpan.FromSeconds(-1);  
            pc.Enabled = true;  
            pc.OnlineMode = ProactiveCachingOnlineMode.OnCacheComplete;  
            pctb = new ProactiveCachingTablesBinding();  
            pctb.NotificationTechnique = NotificationTechnique.Server;  
            tn = new TableNotification("[FactInternetSales]", "dbo");  
            pctb.TableNotifications.Add( tn);  
            pc.Source = pctb;  
  
            part.ProactiveCaching = pc;  
            part.Update();  
        }  
    }  
}  
```  
  
##  <a name="Transl"></a>翻譯物件  
 翻譯物件可以使用 AMO 來定義，但是是從瀏覽資料的用戶端應用程式來使用這些物件。 翻譯物件是非常容易撰寫程式的物件。 物件標題的翻譯是由「地區設定識別碼」與「已翻譯標題」配對所提供。 任何標題都可以啟用多個翻譯。 翻譯可以提供給大部分的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 物件使用，例如維度、屬性、階層、Cube、量值群組、量值等等。  
  
 下列程式碼範例為屬性 Product Name 的名稱提供西班牙文的翻譯。  
  
```  
static public void CreateTranslations(Database db)  
{  
    //Spanish Tranlations for Product Category in Product Dimension  
    Dimension dim = db.Dimensions["Product"];  
    DimensionAttribute atr = dim.Attributes["Product Name"];  
    Translation tran = atr.Translations.Add(3082);  
    tran.Caption = "Nombre Producto";  
  
    dim.Update(UpdateOptions.ExpandFull);  
  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices>   
 [AMO 類別簡介](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO OLAP 類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)   
 [邏輯架構 &#40;Analysis Services-多維度資料 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [資料庫物件 &#40;Analysis Services-多維度資料 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [處理多維度模型 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [安裝 Analysis services 多維度模型化教學課程的範例資料和專案](../../../analysis-services/install-sample-data-and-projects.md)  
  
  

