---
title: Analysis Services 表格式模型中的計算群組 |Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: af63f41555a021fc720c7d1e15778265fe7de500
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419533"
---
# <a name="calculation-groups-preview"></a>計算群組 (預覽)
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

計算群組可以藉由將一般量值運算式分組為*計算專案*, 大幅減少多餘量值的數目。 Azure Analysis Services 和1470和更高[相容性層級](compatibility-level-for-tabular-models-in-analysis-services.md)的 SQL Server Analysis Services 2019 表格式模型支援計算群組。 1470相容性層級的模型目前為**預覽**狀態。  

本文說明： 

> [!div class="checklist"]
> * 權益 
> * 計算群組的工作方式
> * 動態格式字串
> * 排序
> * 優先順序
> * 工具
> * 限制



## <a name="benefits"></a>權益

計算群組會解決複雜模型中的問題, 其中使用相同的計算 (最常見的是時間智慧計算) 來激增多餘的量值。 例如, 銷售分析師想要依月份至今 (MTD)、季迄今 (QTD)、年初至今 (YTD)、前一年的訂單年初至今 (.PY) 等來查看銷售總額和訂單。 資料建模者必須為每個計算建立個別的量值, 而這可能會導致數十個量值。 對於使用者而言, 這可能表示必須直接排序量值, 並將其個別套用到其報表。 

讓我們先看看如何在 Power BI 之類的報告工具中, 對使用者顯示計算群組。 接著, 我們將探討計算群組的組成, 以及如何在模型中建立它們。

計算群組會作為具有單一資料行的資料表，顯示在報告用戶端中。 此資料行不像一般資料行或維度, 而是表示一或多個可重複使用的計算, 或可套用至已加入至視覺效果值篩選之任何量值的*計算專案*。

在下列動畫中, 使用者會分析年2012和2013的銷售資料。 在套用計算群組之前, 一般基底量值**銷售**會計算每個月總銷售額的總和。 然後, 使用者想要套用時間智慧計算, 以取得 [月至今]、[季至今]、[年初至今] 等等的銷售總額。 如果沒有計算群組, 使用者就必須選取個別的時間智慧量值。

使用計算群組 (在此範例中稱為「**時間智慧**」), 當使用者將**時間計算**專案拖曳到 [資料**行**篩選] 區域時, 每個計算專案都會顯示為個別的資料行。 每個資料列的值都是從基底量值**Sales**計算而來。  

![Power BI 中套用的計算群組](media/calculation-groups/calc-groups-pbi.gif)


計算群組會使用**明確**的 DAX 量值。 在此範例中, **Sales**是已在模型中建立的明確量值。 計算群組無法使用隱含 DAX 量值。 例如, 在 Power BI 隱含量值會在使用者將資料行拖曳至視覺效果以查看匯總值時建立, 而不需要建立明確量值。 此時, Power BI 會針對撰寫為內嵌 DAX 計算的隱含量值產生 DAX, 這表示隱含量值無法與計算群組搭配使用。 已引進在表格式物件模型 (TOM) 中可見的新模型屬性 ( **DiscourageImplicitMeasures**)。 目前為了建立計算群組, 此屬性必須設定為**true**。 設定為 true 時, 即時連接模式中的 Power BI Desktop 會停用隱含量值的建立。

## <a name="how-they-work"></a>其工作方式

既然您已瞭解計算群組如何讓使用者受益, 讓我們看看如何建立所顯示的時間智慧計算群組範例。

在我們深入探討詳細資料之前, 讓我們先介紹一些特別針對計算群組的新 DAX 函數: 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) -供計算專案的運算式用來參考目前在內容中的量值。 在此範例中, Sales 量值。

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) -由運算式用來計算專案, 以依名稱決定內容中的量值。

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) -用於計算專案的運算式, 以判斷內容中的量值是在量值清單中指定。

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax) -供計算專案的運算式用來抓取內容中量值的格式字串。

### <a name="time-intelligence-example"></a>時間智慧範例

資料表名稱-**時間智慧**   
資料行名稱-**時間計算**   
優先順序- **20**   

#### <a name="time-intelligence-calculation-items"></a>時間智慧計算專案

**Current**

```dax
SELECTEDMEASURE()
```

**MTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESMTD(DimDate[Date]))
```

**QTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESQTD(DimDate[Date]))
```

**YTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

**.PY**

```dax
CALCULATE(SELECTEDMEASURE(), SAMEPERIODLASTYEAR(DimDate[Date]))
```

**.PY MTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "MTD"
)
```

**.PY QTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "QTD"
)
```

**.PY 年初迄今**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

**YOY**

```dax
SELECTEDMEASURE() –
CALCULATE(
    SELECTEDMEASURE(),
    'Time Intelligence'[Time Calculation] = "PY"
)
```

**YOY%**

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

若要測試此計算群組, 您可以在 SSMS 或開放原始碼[DAX Studio](http://daxstudio.org/)中執行 DAX 查詢。 此查詢範例會省略 YOY 和 YOY%。

#### <a name="time-intelligence-query"></a>時間智慧查詢

```dax
EVALUATE
CALCULATETABLE (
    SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Current", CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "Current" ),
        "QTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "QTD" ),
        "YTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "YTD" ),
        "PY",      CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY" ),
        "PY QTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY QTD" ),
        "PY YTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY YTD" )
    ),
    DimDate[CalendarYear] IN { 2012, 2013 }
)
```

#### <a name="time-intelligence-query-return"></a>時間智慧查詢傳回

傳回資料表會顯示所套用的每個計算專案的計算。 例如, 您可以看到2012年3月的 QTD 是1月、2月和3月2012的總和。

![查詢傳回](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>動態格式字串

具有計算群組的*動態格式字串*允許在不強制傳回字串的情況下, 將格式字串套用至量值的條件式應用。

表格式模型使用 DAX 的[格式](https://docs.microsoft.com/dax/format-function-dax)函數, 支援量值的動態格式化。 不過, FORMAT 函式具有傳回字串的缺點, 會強制執行其他數值的值, 也會以字串的形式傳回。 這可能會有一些限制, 例如, 根據數值 (如圖表), 不能使用大部分的 Power BI 視覺效果。

### <a name="dynamic-format-strings-for-time-intelligence"></a>時間智慧的動態格式字串

如果我們查看上面顯示的時間智慧範例, 除了**YOY%** 以外的所有計算專案, 都應該使用內容中目前量值的格式。 例如, 在「銷售基底」量值上計算的「年初**迄今**」應該是貨幣。 如果這是「訂單」基底量值之類的計算群組, 則格式會是數值。 不過, 不論基底量值的格式為何, **YOY%** 都應該是百分比。

對於**YOY%** , 我們可以將格式字串運算式屬性設定為**0.00%;-0.00%; 0.00%** , 以覆寫格式字串。 若要深入瞭解格式字串運算式屬性, 請參閱[MDX 資料格屬性-格式字串內容](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values)。

在 Power BI 的這個 [矩陣] 視覺效果中, 您會看到目前/ **YOY**的**sales** , 並保留其各自的基底量值格式字串。 不過, **SALES YOY%** 和**Orders YOY%** 會覆寫格式字串, 以使用*百分比*格式。

![矩陣視覺效果中的時間智慧](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>貨幣轉換的動態格式字串

動態格式字串提供簡單的貨幣轉換。 請考慮下列的「艾德作品」資料模型。 它會針對[轉換類型](../currency-conversions-analysis-services.md#conversion-types)所定義的一對多貨幣轉換進行模型化。

![表格式模型中的貨幣速率](media/calculation-groups/calc-groups-currency-conversion.png)

[**字串**格式] 資料行會新增至**DimCurrency**資料表, 並以個別貨幣的格式字串填入。

![格式字串資料行](media/calculation-groups/calc-groups-formatstringcolumn.png)

在此範例中, 下列計算群組會定義為:

### <a name="currency-conversion-example"></a>貨幣轉換範例

資料表名稱-**貨幣轉換**   
資料行名稱-**轉換計算**   
優先順序- **5**   

#### <a name="calculation-items-for-currency-conversion"></a>貨幣轉換的計算專案

**沒有轉換**

```dax
SELECTEDMEASURE()
```

**轉換的貨幣**

```dax
IF(
    //Check one currency in context & not US Dollar, which is the pivot currency:
    SELECTEDVALUE( DimCurrency[CurrencyName], "US Dollar" ) = "US Dollar",
    SELECTEDMEASURE(),
    SUMX(
        VALUES(DimDate[Date]),
        CALCULATE( DIVIDE( SELECTEDMEASURE(), MAX(FactCurrencyRate[EndOfDayRate]) ) )
    )
)
```

格式字串運算式

```dax
SELECTEDVALUE(
    DimCurrency[FormatString],
    SELECTEDMEASUREFORMATSTRING()
)
```
格式字串運算式必須傳回純量字串。 如果篩選內容中有多個貨幣, 它會使用新的[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax)函數來還原為基底量值格式字串。

下列動畫顯示報表中**Sales**量值的動態格式貨幣轉換。

![已套用貨幣轉換動態格式字串](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>優先順序

優先順序是針對計算群組定義的屬性。 當有一個以上的計算群組時, 它會指定評估的順序。 較大的數位表示較高的優先順序, 這表示它會在優先順序較低的計算群組之前進行評估。

在此範例中, 我們將使用與上述的時間智慧範例相同的模型, 但也會加入**平均值**計算群組。 平均計算群組包含與傳統時間智慧無關的平均計算, 因為它們不會變更日期篩選內容, 而只會在其中套用平均計算。

在此範例中, 會定義每日平均計算。 石油和天然氣應用程式中常見的計算, 例如每日的平均桶。 其他常見的商業範例包括將銷售平均存放在零售。

雖然這類計算是與時間智慧計算無關的計算, 但還是有可能需要結合它們。 例如, 使用者可能會想要查看每日 YTD 的桶, 以查看從一年開始到目前日期的每日石油利率。 在此案例中, 應該針對計算專案設定優先順序。

### <a name="averages-example"></a>平均範例

資料表名稱是**平均值**。   
資料行名稱是**平均計算**。   
優先順序為**10**。   

#### <a name="calculation-items-for-averages"></a>平均值的計算專案

**無平均值**

```dax
SELECTEDMEASURE()
```

**每日平均**

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

以下是 DAX 查詢和傳回資料表的範例:

#### <a name="averages-query"></a>平均查詢

```dax
EVALUATE
    CALCULATETABLE (
        SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Sales", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "No Average"
        ),
        "YTD", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "No Average"
        ),
        "Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "Daily Average"
        ),
        "YTD Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "Daily Average"
        )
    ),
    DimDate[CalendarYear] = 2012
)
```

#### <a name="averages-query-return"></a>查詢傳回的平均值

![查詢傳回](media/calculation-groups/calc-groups-ytd-daily-avg.png)

下表顯示如何計算2012年3月的值。


|資料行名稱  |計算 |
|---------|---------|
|YTD     |    Jan、二月、三月2012的銷售總和<br />= 495364 + 506994 + 373483     |
|每日平均    |     三月2012的銷售額除以三月份的 # 天<br />= 373483/31       |
|YTD 每日平均     | 三月2012的年初迄今除以 Jan、二月和三月的天數<br />= 1375841/(31 + 29 + 31)       |

以下是 YTD 計算專案的定義, 其優先順序為**20**。

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

以下是每日平均, 其優先順序為**10**。

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

由於時間智慧計算群組的優先順序高於平均計算群組, 因此會盡可能廣泛地套用。 YTD 每日平均計算會套用至每日平均計算的分子和分母 (日計數)。

這相當於下列運算式:

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

不是此運算式:

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>側邊遞迴

在上述的時間智慧範例中, 有些計算專案會參考相同計算群組中的其他部分。 這稱為「*側向遞迴*」。 例如, **YOY%** 會同時參考**YOY**和 **.py**。

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

在此情況下, 這兩個運算式會分別進行評估, 因為它們使用不同的計算語句。 不支援其他類型的遞迴。

## <a name="single-calculation-item-in-filter-context"></a>篩選內容中的單一計算專案

在我們的時間智慧範例中, **.py 年初迄今**計算專案具有單一計算運算式:

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

計算 () 函數的 YTD 引數會覆寫篩選內容, 以重複使用已在 YTD 計算專案中定義的邏輯。 不可能在單一評估中套用 .PY 和 YTD。 只有當計算群組中的單一計算專案是在篩選內容中時,*才*會套用計算群組。

## <a name="mdx-support"></a>MDX 支援

計算群組支援多維度日期運算式 (MDX) 查詢。 這表示, 使用 MDX 來查詢表格式資料模型的 Microsoft Excel 使用者, 可以充分利用工作表樞紐分析表和圖表中的計算群組。

## <a name="tools"></a>工具

SQL Server Data Tools 中尚不支援計算群組, Visual Studio 具有 Analysis Services 延伸模組。 不過, 您可以使用表格式模型指令碼語言 (TMSL) 或開放原始碼[表格式編輯器](https://github.com/otykier/TabularEditor)來建立計算群組。

## <a name="limitations"></a>限制

[物件層級安全性](object-level-security.md)不支援計算群組資料表上定義的 (OLS)。 不過, 您可以在相同模型中的其他資料表上定義 OLS。 如果計算專案參考 OLS 保護的物件, 則會傳回一般錯誤。

資料[列層級安全性](roles-ssas-tabular.md#bkmk_rowfliters)(RLS) 不受支援。 您可以在相同模型中的資料表上定義 RLS, 而不是在計算群組本身 (直接或間接)。

## <a name="see-also"></a>另請參閱  

[表格式模型中的 DAX](understanding-dax-in-tabular-models-ssas-tabular.md)   
[DAX 參考](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  
