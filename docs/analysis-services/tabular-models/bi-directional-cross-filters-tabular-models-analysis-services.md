---
title: "雙向交叉篩選-表格式模型的 Analysis Services |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5e810707-f58d-4581-8f99-7371fa75b6ac
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: bb36d45580332bdff45daae25a7de3a9e7aa2beb
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="bi-directional-cross-filters---tabular-models---analysis-services"></a>雙向交叉篩選-表格式模型的 Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]新 SQL Server 2016 中已內建方法啟用*雙向交叉篩選*在表格式模型中，因而不須對手工 DAX 因應措施的資料表關聯性之間傳播篩選內容。  
  
 此概念可分解成以下元件組件：「交叉篩選」是指根據相關資料表中的值設定資料表篩選內容的功能，而「雙向」是指將篩選內容傳遞至資料表關聯性另一端的第二個相關資料表。 正如其名，您有兩種方向可以切入關聯性，而不是只有一種方向。  就內部而言，雙向篩選會展開篩選內容來查詢資料的超集。  
  
 ![SSAS BIDI 1-Filteroption](../../analysis-services/tabular-models/media/ssas-bidi-1-filteroption.PNG "SSAS BIDI 1-Filteroption")  
  
 交叉篩選有兩種類型：單向和雙向篩選。 「單向」是關聯性中事實和維度資料表之間傳統的多對一篩選方向。 「雙向」是是一種交叉篩選，可讓某項關聯性的篩選內容能做為另一項資料表關聯性的篩選內容，也就是兩項關聯性共用一個資料表。  
  
 假設 **DimDate** 和 **DimProduct** 與 **FactOnlineSales**有外部索引鍵關聯性，則雙向篩選等同於同時使用 **FactOnlineSales-to-DimDate** 加上 **FactOnlineSales-to-DimProduct** 。  
  
 雙向交叉篩選輕鬆就能解決過去表格式和 Power Pivot 開發人員面對的多對多查詢設計問題。 如果您已經在表格式或 Power Pivot 模型中使用多對多關聯性的 DAX 因應措施，您可以嘗試套用雙向篩選來看看是否產生預期的結果。  
  
 建立雙向交叉篩選時，請謹記下列事項：  
  
-   啟用雙向篩選前請慎重考慮。  
  
     如果您在所有位置啟用雙向篩選，您的資料可能會過度篩選而以您未預期的方式運作。  您可能會因為建立超過一種的可能查詢路徑而造成不定性。 若要避免這兩種問題，可以計劃結合使用單向和雙向篩選。  
  
-   執行累加式測試來驗證各篩選對您模型的改變造成的影響。 [在 Excel 中分析](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md) 很適合累加式測試。 最佳做法是，定期使用其他報表用戶端來追蹤測試，以確保不會有意外狀況。  
  
> [!NOTE]  
>  從 CTP 3.2 開始，SSDT 包含會判斷是否自動嘗試雙向交叉篩選的預設設定。 如果您根據預設啟用雙向篩選，SSDT 將只會在模型透過一連串資料表關聯清楚指出一項查詢路徑時，才會啟用雙向篩選。  
  
## <a name="set-the-default"></a>設定預設值  
 預設值為單向篩選。 您可以針對設計工具中建立的新專案變更所有預設值，或專案已存在則針對模型本身來變更。  
  
 在專案的層級，建立專案時會評估設定，因此若您將預設值變更為雙向，建立下一個專案時便會看到您選取的設定生效。  
  
1.  在 SSDT 中，選取 [工具] > [選項] > [Analysis Services Tabular Designers] > [新增專案設定]。  
  
2.  將 [預設篩選方向]  設為 [單向]  或 [雙向] 。  
  
 同樣地，您也可以變更模型上的預設值。  
  
1.  在方案總管中，選取 [Model.bim] > [屬性]。  
  
2.  將 [預設篩選方向]  設為 [單向]  或 [雙向] 。  
  
## <a name="walkthrough-an-example"></a>範例逐步說明  
 了解雙向交叉篩選的最佳方法是透過範例。 請考慮以下來自 [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279)的資料集，其反映預設建立的基數和交叉篩選。  
  
 ![SSAS BIDI-2 模式](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "SSAS BIDI 2-模型")  
  
> [!NOTE]  
>  根據預設，在匯入資料期間，會以衍生自事實資料表和相關維度資料表之間的外部索引鍵和主索引鍵關聯性的多對一設定，來建立資料表關聯性。  
  
 請注意篩選方向是從維度資料表到事實資料表 -- 促銷、產品、日期、客戶及客戶地理位置都是有效的篩選。  
  
 ![ssas bidi 3-defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "ssas bidi 3-defaultrelationships")  
  
 對於這個簡單的星型結構描述，在 Excel 中測試可確認從資料列和資料行上的維度資料表，篩選到由位在中心 **FactOnlineSales** 資料表的 **Sum of Sales** 量值所提供的彙總資料時，資料會正確地切割。  
  
 ![ssas bidi 4-excelSumSales](../../analysis-services/tabular-models/media/ssas-bidi-4-excelsumsales.PNG "ssas bidi 4-excelSumSales")  
  
 只要量值是從事實資料表提取，且篩選內容終止於事實資料表，對此模型的彙總就會正確篩選。 如果您想在其他位置建立量值 (例如在 products 或 customer 資料表中的特殊計數，或 promotion 資料表中的 average discount)，並讓現有的篩選內容擴充到該量值，則會發生什麼事。  
  
 讓我們試試看從 **DimProducts** 將一個獨特的計數加入樞紐分析表。 請注意 **Count Products**的重複值。 乍看之下，這好像缺少資料表關聯性，但在我們的模型中，我們可以看到所有的關聯性都已經定義且正在使用。 在此案例中，因為 products 資料表中的資料列上沒有日期篩選，所以會出現重複值。  
  
 ![ssas-bidi-5-prodcount-nofilter](../../analysis-services/tabular-models/media/ssas-bidi-5-prodcount-nofilter.png "ssas-bidi-5-prodcount-nofilter")  
  
 在 **FactOnlineSales** 和 **DimProduct**之間加上雙向交叉篩選之後，product 資料表中的資料列現在已根據製造商和日期正確篩選。  
  
 ![ssas-bidi-6-prodcount-withfilter](../../analysis-services/tabular-models/media/ssas-bidi-6-prodcount-withfilter.png "ssas-bidi-6-prodcount-withfilter")  
  
## <a name="learn-step-by-step"></a>逐步學習  
 您可以試作這個逐步說明來嘗試雙向交叉篩選。 若要進行，您會需要：  
  
-   SQL Server 2016 Analysis Services 執行個體、表格式模型、最新版的 CTP  
  
-   和最新版 CTP 一起推出的[SQL Server Data Tools for Visual Studio 2015 (SSDT)](http://go.microsoft.com/fwlink/p/?LinkID=627574)。  
  
-   [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279)  
  
-   此資料的讀取權限  
  
-   Excel (搭配 [在 Excel 中進行分析]使用)  
  
### <a name="create-a-project"></a>建立專案  
  
1.  啟動 Visual Studio 2015 的 SQL Server Data Tools。  
  
2.  按一下 [檔案] > [新增] > [專案] > [Analysis Services 表格式模型]。  
  
3.  在 [表格式模型設計工具] 中，將工作區資料庫設為表格式伺服器模式的 SQL Server 2016 Preview Analysis Services。  
  
4.  請確認模型相容性層級設為**SQL Server 2016 RTM (1200)**或更高版本。  
  
     按一下 **[確定]** 建立專案。  
  
### <a name="add-data"></a>加入資料  
  
1.  按一下 [模型] > [從資料來源匯入] > [Microsoft SQL Server]。  
  
2.  指定伺服器、資料庫和驗證方法。  
  
3.  選擇 [ContosoRetailDW] 資料庫。  
  
4.  按一下 **[下一步]**。  
  
5.  選取資料表時，按下 Ctrl 並選取下列資料表：  
  
    -   FactOnlineSales  
  
    -   DimCustomer  
  
    -   DimDate  
  
    -   DimGeography  
  
    -   DimPromotion  
  
     如果您想要它們在模型中更容易閱讀，可以在此步驟編輯名稱。  
  
     ![ssas bidi-7 ImportData](../../analysis-services/tabular-models/media/ssas-bidi-7-importdata.PNG "ssas bidi-7 ImportData")  
  
6.  匯入資料  
  
 如果發生錯誤，請確認用來連接資料庫的帳戶具備有 Contoso 資料倉儲讀取權限的 SQL Server 登入。 在遠端連線時，您可能也會想檢查 SQL Server 的防火牆上的連接埠設定。  
  
### <a name="review-default-table-relationships"></a>檢閱預設資料表關聯性  
 切換至圖表檢視︰[模型] > [模型檢視] > [圖表檢視]。 基數和作用中的關聯性是以視覺化方式表示。 所有關聯性都是任兩個相關資料表之間的一對多關聯。  
  
 ![SSAS BIDI-2 模式](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "SSAS BIDI 2-模型")  
  
 或者，按一下 [資料表] > [管理關聯性] 以在表格配置中檢視相同的資訊。  
  
 ![ssas bidi 3-defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "ssas bidi 3-defaultrelationships")  
  
### <a name="create-measures"></a>建立量值  
 您將需要彙總來以維度資料的不同 Facet 的加總銷售量。 在 **DimProduct** 中，您可以建立計算產品的量值，並將它用於產品推銷的分析，顯示針對指定的年份、指定的地區或客戶類型所銷售之產品的計數。  
  
1.  按一下 [模型] > [模型檢視] > [圖表檢視]。  
  
2.  按一下 [FactOnlineSales] 。  
  
3.  選取 [SalesAmount]  資料行。  
  
4.  按一下 [資料行] > [自動加總] > [總和] 來建立銷售的量值。  
  
5.  按一下 [DimProduct] 。  
  
6.  選取 [ProductKeycolumn] 。  
  
7.  按一下 [資料行] > [自動加總] > [DistinctCount] 來建立唯一產品的量值。  
  
### <a name="analyze-in-excel"></a>在 Excel 中分析  
  
1.  按一下 [模型] > [在 Excel 中進行分析] 來將所有資料加入一個樞紐分析表。  
  
2.  從欄位清單選取兩個您剛才建立的量值。  
  
3.  選取 [產品] > [製造商]。  
  
4.  選取 [日期] > [日曆年度]。  
  
 請注意，銷售會如預期般按照年度和製造商分類。 這是因為 **FactOnlineSales**、 **DimProduct**和 **DimDate** 之間預設的篩選內容，對於關聯性的「多個」端點皆正確運作。  
  
 同時，您也可以看到在同一個篩選內容中，產品計數沒有像銷售一樣被挑選。 不過產品計數正確地按照製造商篩選 (製造商和產品計數位在同一個資料表)，資料篩選沒有按照產品計數傳播。  
  
### <a name="change-the-cross-filter"></a>變更交叉篩選  
  
1.  回到模型中，選取 [資料表] > [管理關聯性]。  
  
2.  編輯 **FactOnlineSales** 和 **DimProduct**之間的關聯性。  
  
     將篩選方向變更為兩個資料表。  
  
3.  儲存設定。  
  
4.  在活頁簿中，按一下 [重新整理] 重新讀取模型。  
  
 您現在應該會看到產品計數和銷售都以相同的篩選內容篩選，其中不只包含來自 **DimProducts** 的製造商，也包含來自 **DimDate**的日曆年度。  
  
## <a name="conclusion-and-next-steps"></a>結論與後續步驟  
 了解雙向交叉篩選可以當作試誤學習的時機與方法，以明白它在您的案例中會如何運作。 有時候，您會發現內建行為並不足夠，且必須回到 DAX 計算上以完成工作。 在＜另請參閱＞  一節中，您會找到一些關於此主題的其他資源的連結。  
  
 實際上來說，交叉篩選能夠啟用通常只有透過多對多建構才能提供的資料瀏覽格式。 然而，請務必了解雙向交叉篩選不是多對多建構。  此版本的表格式模型設計仍不支援實際的多對多資料表設定。  
  
## <a name="see-also"></a>請參閱  
 [在 Power BI Desktop 建立並管理關聯性](https://support.powerbi.com/knowledgebase/articles/464155-create-and-manage-relationships-in-power-bi-desktop)   
 [如何處理簡單多對多關聯性，在 Power Pivot 和 SSAS 表格式模型中的實際範例](http://social.technet.microsoft.com/wiki/contents/articles/22202.a-practical-example-of-how-to-handle-simple-many-to-many-relationships-in-power-pivotssas-tabular-models.aspx)   
 [正在解析多對多關聯性利用 DAX 交叉資料表篩選](http://blog.gbrueckl.at/2012/05/resolving-many-to-many-relationships-leveraging-dax-cross-table-filtering/)   
 [多對多革命 （SQLBI 部落格）](http://www.sqlbi.com/articles/many2many/)  
  
  
