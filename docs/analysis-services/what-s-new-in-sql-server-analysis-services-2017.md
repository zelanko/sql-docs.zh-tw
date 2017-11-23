---
title: "什麼是 SQL Server 2017 Analysis Services 的新功能 |Microsoft 文件"
ms.date: 10/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: analysis-services
ms.topic: article
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 5ae75be33450531d510463281ef182121797e79a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="whats-new-in-sql-server-2017-analysis-services"></a>SQL Server 2017 Analysis Services 中最新消息
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

SQL Server 2017 Analysis Services 會看到一些最重要的增強功能自 SQL Server 2012。 這一版為基礎的表格式模式 （SQL Server 2012 Analysis Services 中首次引進） 成功，可讓表格式模型比以往更強大。

多維度模式和 Power Pivot for SharePoint 模式是許多 Analysis Services 部署裝訂。 Analysis Services 產品開發週期中，這些模式才成熟。 沒有這些模式，在此版本中的任何新功能。 然而，在錯誤修正和效能增強功能會加入。

這裡說明的功能會包含在 SQL Server 2017 Analysis Services。 若要利用它們，您也必須使用的最新版本，但是[SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) (SSDT) 和[SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) (SSMS)。 SSDT 和 SSMS 會隨每月新功能和改進功能通常符合 SQL Server 中的新功能。  

時請務必了解所有新功能，也很重要知道什麼被取代，而且在此版本和未來的版本中已停止。 請務必查看[回溯相容性 (SQL Server 2017 Analysis Services)](analysis-services-backward-compatibility-sql2017.md)。

在此版本中，讓我們看看一些重要的新功能。

## <a name="1400-compatibility-level-for-tabular-models"></a>表格式模型的 1400 相容性層級
  若要使用的許多新功能與功能所述的以下，必須設定或升級 1400年相容性層級為新的或現有的表格式模型。 使用 1400 相容性層級的模型無法部署到 SQL Server 2016 SP1 或更早版本，或降級為較低的相容性層級。 若要進一步了解，請參閱[Analysis Services 表格式模型的相容性層級](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。
  
在 SSDT 中，您可以在建立新的表格式模型專案時，選取新的 1400 相容性層級。 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)


若要升級現有的表格式模型在 SSDT 中，在 [方案總管] 中，以滑鼠右鍵按一下**Model.bim**，然後在**屬性**，將**相容性層級**屬性**SQL Server 2017 (1400)**。 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

請務必記住，一旦您 1400年来升級現有的模型，您無法降級。 請務必保留 1200年模型資料庫的備份。

## <a name="modern-get-data-experience"></a>新式取得資料經驗
從資料來源匯入資料到您的表格式模型時，SQL Server Data Tools (SSDT) 導入了現代**取得資料**遇到 1400年相容性層級的模型。 這項新功能是以 Power BI Desktop 和 Microsoft Excel 2016 中類似的功能為基礎。 現代的 取得資料 功能提供廣大資料轉換和資料 mashup 功能，透過 取得資料的查詢產生器 」 和 「 M 運算式。

現代的 [取得資料] 功能提供支援各種不同的資料來源。 接下來，更新會包含更多的支援。

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

 功能強大且直覺式使用者介面可讓您選取您的資料和資料轉換/mashup 功能比以往更為容易。

![進階的 mashup](../analysis-services/media/as-get-data-advanced.png)


現代的 取得資料體驗，M mashup 功能不會套用到現有的表格式模型 upraded 從 1400年 1200年相容性層級。 1400 相容性層級建立新的模型僅適用於新的體驗。

## <a name="encoding-hints"></a>編碼的提示
此版本導入編碼提示，並用來最佳化的大型記憶體中的表格式模型的處理 （資料重新整理） 的進階功能。 若要進一步了解編碼方式，請參閱[效能微調的表格式模型 SQL Server 2012 Analysis Services 中](https://msdn.microsoft.com/library/dn393915.aspx)以深入了解編碼方式的技術白皮書。

* 編碼值提供較佳的查詢效能，通常僅適用於彙總的資料行。

* 雜湊編碼，最好群組依據資料行 （通常是維度資料表值） 和外部索引鍵。 字串資料行一律會編碼的雜湊。

數值資料行可以使用其中一種編碼的方法。 當 Analysis Services 開始處理資料表時，如果任一個資料表是空的 （或如果沒有資料分割） 或正在執行完整資料表處理操作時，每個數值資料行來判斷是否要套用的值或雜湊編碼採取範例值. 根據預設，值編碼選擇是當資料行中相異值的範例是夠大，否則雜湊編碼通常會提供更好的壓縮。 您可根據 進一步了解資料的分佈，部分處理的資料行之後，變更編碼方式，並重新啟動在編碼程序; Analysis services不過，這會增加處理時間，並沒有效率。 效能微調技術白皮書討論更多詳細資料中重新編碼，並說明如何使用 SQL Server Profiler 會偵測到。

編碼提示允許指定之提供背景知識從資料分析和 （或） 重新編碼追蹤事件的回應編碼方式的喜好設定模型師 」。 因為雜湊編碼的資料行的彙總為速度較慢，超過值編碼的資料行值編碼可指定做為這類資料行的提示。 不保證會套用喜好設定。 這是相對於設定的提示。 若要指定編碼的提示，請在資料行上設定 EncodingHint 屬性。 可能的值為 「 預設 」、 「 值 」 和 「 雜湊 」。 下列程式碼片段的 JSON 型 Model.bim 檔案中的中繼資料指定編碼 Sales Amount 資料行的值。

```
{
    "name": "Sales Amount",
    "dataType": "decimal",
    "sourceColumn": "SalesAmount",
    "formatString": "\\$#,0.00;(\\$#,0.00);\\$#,0.00",
    "sourceProviderType": "Currency",
    "encodingHint": "Value"
}
```

## <a name="ragged-hierarchies"></a>不完全階層
在表格式模型中，您可以建立父子式階層的模型。 有多種不同層級的階層通常稱為「不完全階層」。 依預設，不完全階層會在最低的子系下顯示空白層級。 組織圖中的不完全階層範例如下︰

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

此版本推出 **隱藏成員** 屬性。 您可以將階層的 **隱藏成員** 屬性設定為[Hide blank members (隱藏空白成員)] 。

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > 模型中的空白成員以 DAX 空白值表示，不是空的字串。

設為 **Hide blank members**(隱藏空白成員) 並部署了模型後，較方便讀取的階層版本會顯示在報表用戶端，例如 Excel。

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)


## <a name="detail-rows"></a>詳細資料列
您現在可以定義參與量值的自訂資料列集。 詳細資料列類似多維度模型中的預設鑽研動作。 這可讓使用者檢視比彙總層級更詳細的資訊。 

下列的樞紐分析表會依年份顯示 Adventure Works 範例表格式模型的 Internet Total Sales (網際網路總銷售額)。 您可以滑鼠右鍵按一下量值中有彙總值的儲存格，然後按一下 [顯示詳細資料]  檢視詳細資料列。

![AS_Show_Details](../analysis-services/media/as-show-details.png)

預設會顯示 Internet Sales 資料表中的相關聯資料。 對使用者而言，此限制的行為通常沒有意義，因為資料表可能沒有能顯示有用資訊的必要資料行，例如客戶名稱和訂單資訊。 您可以使用 [詳細資料列] 指定量值的 **Detail Rows Expression** (詳細資料列運算式) 屬性。

#### <a name="detail-rows-expression-property-for-measures"></a>量值的 Detail Rows Expression (詳細資料列運算式) 屬性
量值的 **Detail Rows Expression** (詳細資料列運算式)屬性可讓模型作者自訂傳回給使用者的資料行和資料列。

![AS_Detail_Rows_Expression_Property](../analysis-services/media/as-detail-rows-expression-property.png)

[SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) DAX 函數通常用在詳細資料列運算式中。 下例會定義範例 Adventure Works 表格式模型的 Internet Sales 資料表中，資料列要傳回的資料行︰

```
SELECTCOLUMNS(
    'Internet Sales',
    "Customer First Name", RELATED( Customer[Last Name]),
    "Customer Last Name", RELATED( Customer[First Name]),
    "Order Date", 'Internet Sales'[Order Date],
    "Internet Total Sales", [Internet Total Sales]
)
```

定義屬性及部署模型之後，當使用者選取 [顯示詳細資料] 時，就會傳回自訂的資料列集。 它會自動接受所選儲存格的篩選器內容優先權。 本例中只會顯示 2010 年的值資料列︰

![AS_Detail_Rows](../analysis-services/media/as-detail-rows.png)

#### <a name="default-detail-rows-expression-property-for-tables"></a>資料表的預設 Detail Rows Expression (詳細資料列運算式) 屬性
除量值之外，資料表也有定義詳細資料列運算式的屬性。 **Default Detail Rows Expression** (預設詳細資料列運算式) 屬性的作用如同資料表中所有量值的預設值。 沒有自己的運算式定義的量值運算式會繼承資料表，並顯示在資料列集定義的資料表。 這可讓重複使用運算式，以及新的量值加入至資料表稍後會自動繼承運算式。

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>DETAILROWS DAX 函數
本版中附有新的 `DETAILROWS` DAX 函數，會傳回詳細資料列運算式所定義的資料列集。 其運作方式類似 MDX 的 `DRILLTHROUGH` 陳述式，與表格式模型中所定義的詳細資料列運算式也相容。

下列 DAX 查詢會傳回量值或其資料表的詳細資料列運算式所定義的資料列集。 如未定義任何運算式，則會傳回 Internet Sales 資料表的資料，因為它是包含量值的資料表。

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="object-level-security"></a>物件層級安全性
此版本導入[物件層級安全性](../analysis-services/tabular-models/object-level-security.md)資料表和資料行。 除了限制存取資料表和資料行的資料，您可以保護敏感的資料表和資料行名稱。 這有助於防止惡意使用者探查是否有這類資料表。

物件層級安全性必須使用 JSON 基礎之中繼資料、 Tabular Model Scripting Language (TMSL) 或表格式物件模型 (TOM) 設定。 

例如，下列程式碼將 **TablePermission** 類別的 **MetadataPermission** 屬性設為 [無] ，協助保護範例 Adventure Works 表格式模型中的 Product 資料表。

```
//Find the Users role in Adventure Works and secure the Product table
ModelRole role = db.Model.Roles.Find("Users");
Table productTable = db.Model.Tables.Find("Product");
if (role != null && productTable != null)
{
    TablePermission tablePermission;
    if (role.TablePermissions.Contains(productTable.Name))
    {
        tablePermission = role.TablePermissions[productTable.Name];
    }
    else
    {
        tablePermission = new TablePermission();
        role.TablePermissions.Add(tablePermission);
        tablePermission.Table = productTable;
    }
    tablePermission.MetadataPermission = MetadataPermission.None;
}
db.Update(UpdateOptions.ExpandFull);
```

## <a name="dynamic-management-views-dmvs"></a>動態管理檢視 (DMV)
[Dmv](../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)傳回本機伺服器作業和伺服器健全狀況的相關資訊的查詢在 SQL Server Profiler。
此版本包含改良[動態管理檢視](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services)(DMV) 1200年和 1400年相容性層級的表格式模型。

[DISCOVER_CALC_DEPENDENCY](../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)現在可搭配表格式 1200年模型和 1400年模型。 1400 的表格式模型顯示 M 磁碟分割、 M 運算式和結構化的資料來源之間的相依性。 若要進一步了解，請參閱[Analysis Services 部落格](https://blogs.msdn.microsoft.com/analysisservices/2017/07/17/whats-new-in-sql-server-2017-rc1-for-analysis-services/)。

[MDSCHEMA_MEASUREGROUP_DIMENSIONS](../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)增強功能是針對這個 DMV，可由各種用戶端工具來顯示量值維度性。 比方說，在 Excel 樞紐分析表中的瀏覽功能可讓使用者跨-向下切入至與選取的量值相關的維度。 此版本中修正基數資料行，先前所顯示不正確的值。

## <a name="dax-enhancements"></a>DAX 增強功能
本版包含新的 DAX 函數和功能的支援。 若要利用，您必須使用最新版的 SSDT。 若要進一步了解，請參閱[新的 DAX 函數](https://msdn.microsoft.com/library/mt704075.aspx)。

其中一個新的 DAX 功能的最重要項目是新[IN 運算子 / 函式 CONTAINSROW](https://msdn.microsoft.com/library/mt842621.aspx) DAX 運算式。 這類似於 [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) 子句中常用來指定多個值的 `WHERE` 運算子。

過去通常使用邏輯 `OR` 運算子指定多重值的篩選條件，如下列量值運算式中所示︰

```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
                 'Product'[Color] = "Red"
            || 'Product'[Color] = "Blue"
            || 'Product'[Color] = "Black"
    )
```

這可使用 `IN` 運算子簡化︰
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], 'Product'[Color] IN { "Red", "Blue", "Black" }
    )
```

在此情況下， `IN` 運算子參照有 3 個資料列的單一資料行資料表，每列都有指定的色彩。 請注意，資料表的建構函式語法使用大括號。

`IN` 運算子的功能等同於 `CONTAINSROW` 函數：
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], CONTAINSROW({ "Red", "Blue", "Black" }, 'Product'[Color])
    )
```

`IN` 運算子也可以有效地搭配資料表建構函式。 例如，下列依產品色彩和類別組合的量值篩選︰
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
              ( 'Product'[Color] = "Red"   && Product[Product Category Name] = "Accessories" )
         || ( 'Product'[Color] = "Blue"  && Product[Product Category Name] = "Bikes" )
         || ( 'Product'[Color] = "Black" && Product[Product Category Name] = "Clothing" )
        )
    )
```

使用新的 `IN` 運算子，上述的量值運算式現在即等同於下列運算式︰
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
            ('Product'[Color], Product[Product Category Name]) IN
            { ( "Red", "Accessories" ), ( "Blue", "Bikes" ), ( "Black", "Clothing" ) }
        )
    )
```

## <a name="additional-improvements"></a>其他增強功能
除了所有新的功能，Analysis Services、 SSDT 和 SSMS 也會包含下列增強功能：

* 階層和資料行重複使用形式出現在 Power BI 的欄位清單中更有用的位置。
* 若要輕鬆地建立與日期欄位為基礎的日期維度關聯性的日期關聯性。
* Analysis Services 的預設安裝選項現在是為表格式模式。
* 新資料來源取得資料 (Power Query)。
* SSDT 的 DAX 編輯器。
* 現有 DirectQuery 資料來源支援的 M 查詢。
* SSMS 增強功能，例如檢視、 編輯和指令碼支援的結構化的資料來源。



## <a name="see-also"></a>另請參閱
[SQL Server 2017 版本資訊](../sql-server/sql-server-2017-release-notes.md)   
[SQL Server 2017 的新功能](../sql-server/what-s-new-in-sql-server-2017.md)
