---
title: "SQL Server Analysis Services vNext 的新功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 13
---
# SQL Server Analysis Services vNext 的新功能
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

## <a name="sql-server-analysis-services-on-windows-ctp-12"></a>Windows CTP 1.2 上的 SQL Server Analysis Services

此版本中沒有新功能。 改進的項目包含錯誤修正和效能。

最新的 SQL Server Data Tools (SSDT) 預覽版 (與 SQL Server vNext CTP 1.2 一致)，以新的查詢編輯器功能表和快速存取功能，改進 CTP 1.1 引進的新式「取得資料」體驗。 

## <a name="sql-server-analysis-services-on-windows-ctp-11"></a>Windows CTP 1.1 上的 SQL Server Analysis Services 

此版本推出表格式模型的增強功能。 

### <a name="1400-compatibility-level-for-tabular-models"></a>表格式模型的&1400; 相容性層級
  若要充分利用本文中所述的功能，新的或現有的表格式模型都必須設定為 1400 相容性層級。 使用 1400 相容性層級的模型無法部署到 SQL Server 2016 SP1 或更早版本，或降級為較低的相容性層級。
  
  若要建立新的或升級現有的表格式模型專案至 1400 相容性層級，請下載並安裝 [SQL Server Data Tools (SSDT) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939) 的**預覽版本**。 
  
在 SSDT 中，您可以在建立新的表格式模型專案時，選取新的 1400 相容性層級。 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)

>[!NOTE] SQL Server Data Tools (SSDT) 12 月發行版本的整合式工作區支援 1400 相容性層級。 如果在工作區伺服器執行個體上建立新的表格式模型專案，您所部署的該執行個體或任何執行個體都必須是 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]CTP 1.1。 

若要在 SSDT 中升級現有的表格式模型，請在方案總管中，以滑鼠右鍵按一下 [Model.bim]，然後在 [內容] 中將**相容性層級**屬性設定為 [SQL Server vNext (1400)]。 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

### <a name="modern-get-data-experience"></a>新式取得資料經驗
伴隨 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1 版本的 SQL Server Data Tools (SSDT) 最新預覽版本，針對 1400 相容性層級的表格式模型推出新式的**取得資料**體驗。 這項新功能是以 Power BI Desktop 和 Microsoft Excel 2016 中類似的功能為基礎。

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

>[!NOTE] 這個版本支援的資料來源數目有限。 未來的更新會支援其他的資料來源和功能。

若要深入了解新式的取得資料體驗，請參閱 [Analysis Services Team Blog](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-vnext-on-windows-ctp-1-1-for-analysis-services/) (Analysis Services 小組部落格)。

## <a name="ragged-hierarchies"></a>不完全階層
在表格式模型中，您可以建立父子式階層的模型。 有多種不同層級的階層通常稱為「不完全階層」。 依預設，不完全階層會在最低的子系下顯示空白層級。 組織圖中的不完全階層範例如下︰

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

此版本推出**隱藏成員**屬性。 您可以將階層的**隱藏成員**屬性設定為[Hide blank members (隱藏空白成員)]。

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE] 模型中的空白成員以 DAX 空白值表示，不是空的字串。

設為 **Hide blank members** (隱藏空白成員) 並部署了模型後，較方便讀取的階層版本會顯示在報表用戶端，例如 Excel。

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)

### <a name="detail-rows"></a>詳細資料列
您現在可以定義參與量值的自訂資料列集。 詳細資料列類似多維度模型中的預設鑽研動作。 這可讓使用者檢視比彙總層級更詳細的資訊。 

下列的樞紐分析表會依年份顯示 Adventure Works 範例表格式模型的 Internet Total Sales (網際網路總銷售額)。 您可以滑鼠右鍵按一下量值中有彙總值的儲存格，然後按一下 [顯示詳細資料] 檢視詳細資料列。

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
此版本包含 DAX 運算式的 `IN` 運算子。 這類似於 `WHERE` 子句中常用來指定多個值的 [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) 運算子。

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

在此情況下，`IN` 運算子參照有 3 個資料列的單一資料行資料表，每列都有指定的色彩。 請注意，資料表的建構函式語法使用大括號。

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

例如，下列程式碼將 **TablePermission** 類別的 **MetadataPermission** 屬性設為 [無]，協助保護範例 Adventure Works 表格式模型中的 Product 資料表。

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
## <a name="future-updates"></a>未來的更新
未來的版本中會包含其他的增強功能。 發佈有關 SQL Server vNext 新功能的相關重要聲明時，本文即會更新。
