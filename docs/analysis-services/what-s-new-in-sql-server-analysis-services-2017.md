---
title: "什麼 &#39; 的新功能 SQL Server 2017 Analysis Services |Microsoft 文件"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 572af6f86f015c88141bb6e78b781b5825be155c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="what39s-new-in-sql-server-2017-analysis-services"></a>什麼 &#39; 的新功能 SQL Server 2017 Analysis Services
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]


## <a name="sql-server-2017-analysis-services-rc2"></a>SQL Server 2017 Analysis Services RC2
此版本中沒有新功能。 在此版本中的增強功能包括 bug 修正和效能。

## <a name="sql-server-2017-analysis-services-rc1"></a>SQL Server 2017 Analysis Services RC1
在此版本中有任何新功能，不過，本版還包含其他的增強功能[動態管理檢視](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services)(DMV) 1200年和 1400年相容性層級的表格式模型。

現在 DISCOVER_CALC_DEPENDENCY 適用於表格式 1200年模型和 1400年模型。 1400 的表格式模型顯示 M 磁碟分割、 M 運算式和結構化的資料來源之間的相依性。 若要進一步了解，請參閱[Analysis Services 部落格](https://blogs.msdn.microsoft.com/analysisservices/)。

MDSCHEMA_MEASUREGROUP_DIMENSIONS 增強功能是針對這個 DMV，可由各種用戶端工具來顯示量值維度性。 比方說，在 Excel 樞紐分析表中的瀏覽功能可讓使用者跨-向下切入至與選取的量值相關的維度。 此版本中修正基數資料行，先前所顯示不正確的值。

## <a name="sql-server-analysis-services-ctp-21"></a>SQL Server Analysis Services CTP 2.1
此版本中沒有新功能。 在此版本中的增強功能包括 bug 修正和效能，以及增強功能[動態管理檢視](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services)(DMV)。 Dmv 會傳回本機伺服器作業和伺服器健全狀況的相關資訊的查詢在 SQL Server Profiler。 如需詳細資訊，請參閱[Analysis Services 部落格](https://blogs.msdn.microsoft.com/analysisservices/)。

## <a name="sql-server-analysis-services-ctp-20"></a>SQL Server Analysis Services CTP 2.0
這個版本包含許多新的增強功能的表格式模型中，包括：

* 物件層級安全性，以保護表格式模型的中繼資料。
* 回應速度更快的開發人員經驗的交易效能改進。
* 增強的動態管理檢視功能啟用相依性分析和報告的 1200年和 1400年模型。
* 詳細資料資料列運算式的撰寫體驗的增強功能。
* 階層和資料行重複使用來顯示更有幫助的位置，在 Power BI 的 [欄位] 清單中。
* 若要輕鬆地建立與日期欄位為基礎的日期維度關聯性的日期關聯性。
* Analysis Services 的預設安裝選項現在是為表格式模式。
* 新資料來源取得資料 (電源 Qery)。
* SSDT 的 DAX 編輯器。
* 現有 DirectQuery 資料來源支援的 M 查詢。
* SSMS 增強功能，例如檢視、 編輯和指令碼支援的結構化的資料來源。

若要取得有關這個 CTP 2.0 版本的詳細資訊，請參閱[Analysis Services 部落格](https://blogs.msdn.microsoft.com/analysisservices/)。

## <a name="sql-server-analysis-services-on-windows-ctp-14"></a>在 CTP 1.4 Windows 上的 SQL Server Analysis Services
[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate)和[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms-release-candidate)與 SQL Server 2017 預覽版本的預覽版本一致。 請務必使用最新取得的新功能。 若要進一步了解，請參閱[Analysis Services 部落格](https://blogs.msdn.microsoft.com/analysisservices/)。



## <a name="sql-server-analysis-services-on-windows-ctp-13"></a>CTP 1.3 在 Windows 上的 SQL Server Analysis Services

### <a name="encoding-hints"></a>編碼的提示

此版本導入編碼提示，並用來最佳化的大型記憶體中的表格式模型的處理 （資料重新整理） 的進階功能。 若要進一步了解編碼方式，請參閱[效能微調的表格式模型 SQL Server 2012 Analysis Services 中](https://msdn.microsoft.com/library/dn393915.aspx)以深入了解編碼方式的技術白皮書。 此處所述在編碼程序適用於 CTP 1.3。

* 編碼值提供較佳的查詢效能，通常僅適用於彙總的資料行。

* 雜湊編碼，最好群組依據資料行 （通常是維度資料表值） 和外部索引鍵。 字串資料行一律會編碼的雜湊。

數值資料行可以使用其中一種編碼的方法。 當 Analysis Services 開始處理資料表時，如果任一個資料表是空的 （或如果沒有資料分割） 或正在執行完整資料表處理操作時，每個數值資料行來判斷是否要套用的值或雜湊編碼採取範例值. 根據預設，值編碼選擇是當資料行中相異值的範例是夠大，否則雜湊編碼通常會提供更好的壓縮。 您可根據 進一步了解資料的分佈，部分處理的資料行之後，變更編碼方式，並重新啟動在編碼程序的 Analysis services。 這當然會增加處理時間，而沒有效率。 效能微調技術白皮書討論更多詳細資料中重新編碼，並說明如何使用 SQL Server Profiler 會偵測到。

CTP 1.3 中的編碼提示允許指定之提供背景知識從資料分析和 （或） 重新編碼追蹤事件的回應編碼方式的喜好設定模型師 」。 因為雜湊編碼的資料行的彙總為速度較慢，超過值編碼的資料行值編碼可指定做為這類資料行的提示。 不保證，則會套用喜好設定;因此，它是提示，而不是一種設定。 若要指定編碼的提示，請在資料行上設定 EncodingHint 屬性。 可能的值為 「 預設 」、 「 值 」 和 「 雜湊 」。 在撰寫本文時，屬性不還會公開在 SSDT 中，因此必須使用 JSON 基礎之中繼資料、 Tabular Model Scripting Language (TMSL) 或表格式物件模型 (TOM) 設定。 下列程式碼片段的 JSON 型 Model.bim 檔案中的中繼資料指定編碼 Sales Amount 資料行的值。

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

### <a name="extended-events-not-working-in-ctp-13"></a>擴充事件無法運作中 CTP 1.3
擴充事件的 SSAS 在 CTP 1.3 中無法運作。 修正已規劃的下一步的 CTP 中。

## <a name="sql-server-analysis-services-on-windows-ctp-12"></a>Windows CTP 1.2 上的 SQL Server Analysis Services

此版本中沒有新功能。 改進的項目包含錯誤修正和效能。

最新預覽版本的 SQL Server 資料工具 (SSDT)，這與 SQL Server 2017 CTP 1.2 一致，改良，其與新的查詢編輯器 功能表、 快速存取功能 CTP 1.1 版中導入新現代取得資料體驗。 

## <a name="sql-server-analysis-services-on-windows-ctp-11"></a>Windows CTP 1.1 上的 SQL Server Analysis Services 

此版本推出表格式模型的增強功能。 

### <a name="1400-compatibility-level-for-tabular-models"></a>表格式模型的&1400; 相容性層級
  若要充分利用本文中所述的功能，新的或現有的表格式模型都必須設定為 1400 相容性層級。 使用 1400 相容性層級的模型無法部署到 SQL Server 2016 SP1 或更早版本，或降級為較低的相容性層級。
  
  若要建立新的或升級現有的表格式模型專案至 1400 相容性層級，請下載並安裝 **SQL Server Data Tools (SSDT) 17.0 RC2** 的 [預覽版本](https://go.microsoft.com/fwlink?LinkId=837939)。 
  
在 SSDT 中，您可以在建立新的表格式模型專案時，選取新的 1400 相容性層級。 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)

>[!NOTE]
> SQL Server Data Tools (SSDT) 12 月發行版本的整合式工作區支援 1400 相容性層級。 如果在工作區伺服器執行個體上建立新的表格式模型專案，您所部署的該執行個體或任何執行個體都必須是 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1。 

若要升級現有的表格式模型在 SSDT 中，在 [方案總管] 中，以滑鼠右鍵按一下**Model.bim**，然後在**屬性**，將**相容性層級**屬性**SQL Server 2017 (1400)**。 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

### <a name="modern-get-data-experience"></a>新式取得資料經驗
伴隨 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1 版本的 SQL Server Data Tools (SSDT) 最新預覽版本，針對 1400 相容性層級的表格式模型推出新式的 **取得資料** 體驗。 這項新功能是以 Power BI Desktop 和 Microsoft Excel 2016 中類似的功能為基礎。

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

>[!NOTE]
> 這個版本支援的資料來源數目有限。 未來的更新會支援其他的資料來源和功能。

若要深入了解新式的取得資料體驗，請參閱 [Analysis Services Team Blog](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-2017-on-windows-ctp-1-1-for-analysis-services/)(Analysis Services 小組部落格)。

## <a name="ragged-hierarchies"></a>不完全階層
在表格式模型中，您可以建立父子式階層的模型。 有多種不同層級的階層通常稱為「不完全階層」。 依預設，不完全階層會在最低的子系下顯示空白層級。 組織圖中的不完全階層範例如下︰

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

此版本推出 **隱藏成員** 屬性。 您可以將階層的 **隱藏成員** 屬性設定為[Hide blank members (隱藏空白成員)] 。

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > 模型中的空白成員以 DAX 空白值表示，不是空的字串。

設為 **Hide blank members**(隱藏空白成員) 並部署了模型後，較方便讀取的階層版本會顯示在報表用戶端，例如 Excel。

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)

### <a name="detail-rows"></a>詳細資料列
您現在可以定義參與量值的自訂資料列集。 詳細資料列類似多維度模型中的預設鑽研動作。 這可讓使用者檢視比彙總層級更詳細的資訊。 

下列的樞紐分析表會依年份顯示 Adventure Works 範例表格式模型的 Internet Total Sales (網際網路總銷售額)。 您可以滑鼠右鍵按一下量值中有彙總值的儲存格，然後按一下 [顯示詳細資料]  檢視詳細資料列。

![AS_Show_Details](../analysis-services/media/as-show-details.png)

預設會顯示 Internet Sales 資料表中的相關聯資料。 對使用者而言，此限制的行為通常沒有意義，因為資料表可能沒有能顯示有用資訊的必要資料行，例如客戶名稱和訂單資訊。 您可以使用 [詳細資料列] 指定量值的 **Detail Rows Expression** (詳細資料列運算式) 屬性。

#### <a name="detail-rows-expression-property-for-measures"></a>量值的 Detail Rows Expression (詳細資料列運算式) 屬性
量值的 **Detail Rows Expression** (詳細資料列運算式)屬性可讓模型作者自訂傳回給使用者的資料行和資料列。

![AS_Detail_Rows_Expression_Property](../analysis-services/media/as-detail-rows-expression-property.png)

Detail Rows Expression (詳細資料列運算式) 中會經常使用 [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) DAX 函數。 下例會定義範例 Adventure Works 表格式模型的 Internet Sales 資料表中，資料列要傳回的資料行︰

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
除量值之外，資料表也有定義詳細資料列運算式的屬性。 **Default Detail Rows Expression** (預設詳細資料列運算式) 屬性的作用如同資料表中所有量值的預設值。 未定義本身運算式的量值會繼承資料表的運算式，並顯示為資料表定義的資料列集。 這允許重複使用運算式，而之後加入資料表的新量值會自動繼承運算式。

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>DETAILROWS DAX 函數
本版中附有新的 `DETAILROWS` DAX 函數，會傳回詳細資料列運算式所定義的資料列集。 其運作方式類似 MDX 的 `DRILLTHROUGH` 陳述式，與表格式模型中所定義的詳細資料列運算式也相容。

下列 DAX 查詢會傳回量值或其資料表的詳細資料列運算式所定義的資料列集。 如未定義任何運算式，則會傳回 Internet Sales 資料表的資料，因為它是包含量值的資料表。

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="dax-enhancements"></a>DAX 增強功能
此版本包含 DAX 運算式的 `IN` 運算子。 這類似於 [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) 子句中常用來指定多個值的 `WHERE` 運算子。

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


## <a name="table-level-security"></a>資料表層級的安全性
此版本推出資料表層級的安全性。 除了限制存取資料表資料，也可以保護敏感的資料表名稱。 這有助於防止惡意使用者探查是否有這類資料表。

資料表層級的安全性必須使用以 JSON 為基礎的中繼資料、表格式模型撰寫指令碼語言 (TMSL) 或表格式物件模型 (TOM) 來設定。 

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


