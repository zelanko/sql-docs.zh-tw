---
title: Analysis Services 表格式模型中的計算群組 |Microsoft Docs
ms.date: 06/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: abc1f51d21613676fd94271f931e1a7692cc1efc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822697"
---
# <a name="calculation-groups-preview"></a>計算群組 （預覽版）
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

計算群組可以大幅降低備援的量值的數目，藉由群組為常用的量值運算式*計算項目*。 Azure Analysis Services 中支援計算群組和 SQL Server Analysis Services 2019 表格式模型在 1470年和更新版本[相容性層級](compatibility-level-for-tabular-models-in-analysis-services.md)。 1470 相容性層級的模型是目前**預覽**。  

本文說明： 

> [!div class="checklist"]
> * 優點 
> * 計算群組的運作方式
> * 動態的格式字串
> * 優先順序
> * 工具
> * 限制



## <a name="benefits"></a>優點

計算群組解決問題，其中可以有複雜的模型中的過多的重複使用相同的計算-最常見的使用時間智慧計算的量值。 例如，銷售分析師想要檢視銷售總額，並依照月份至今 (MTD)，當季到目前 (QTD)，來排序今年到目前 (YTD)，排序今年到目前的前一年 (PY)，依此類推。 資料模型師 」，就必須建立個別的量值，可能會導致數十個量值的每一個計算。 針對使用者，這樣表示必須透過了同樣多的量值，排序和個別套用至其報表。 

讓我們先看看計算群組至報表的工具，例如 Power BI 中的使用者的顯示方式。 接著我們將看 2005),steve 計算群組，以及如何在模型中建立。

計算群組會作為具有單一資料行的資料表，顯示在報告用戶端中。 不像一般的資料行或維度的資料行，而它代表一或多個可重複使用的計算，或*計算項目*，可以套用至任何已新增至視覺效果的值篩選的量值。

在下列動畫中，使用者正在分析 2012年和 2013 年的銷售資料。 套用計算群組，常見的基底量值之前**銷售**計算每個月的總銷售量的總和。 使用者接著想要套用時間智慧計算銷售總額取得月初至今、 季初至今，年初至今的情況下，等等。 沒有計算群組中，使用者就必須選取個別的時間智慧量值。

計算群組，在此範例中名為**時間智慧**，當使用者拖曳**時間計算**項目**資料行**篩選區域中，每個計算項目會顯示為個別的資料行。 每個資料列的值會計算基底量值中，從**銷售**。  

![在 Power BI 中套用的計算群組](media/calculation-groups/calc-groups-pbi.gif)


計算群組搭配**明確**DAX 量值。 在此範例中，**銷售**是已經在模型中建立明確量值。 計算群組功能不適用於隱含的 DAX 量值。 比方說，在 Power BI 中時的使用者資料行拖放視覺效果來檢視彙總的值，而不需要建立明確量值會建立隱含量值。 在此階段中，Power BI 會產生為內嵌撰寫 DAX 計算-這表示隱含量值不能用於計算群組的隱含量值的 DAX。 導入了新的模型屬性顯示表格式物件模型 (TOM)， **DiscourageImplicitMeasures**。 目前，若要建立計算群組的這個屬性必須設為 **，則為 true**。 當設定為 true 時，Power BI Desktop 中 Live Connect 模式會停用建立隱含量值。

## <a name="how-they-work"></a>其運作方式

既然您已了解如何計算群組中受益的使用者，讓我們看看如何建立時間智慧計算群組範例所示。

我們進入細節之前，請讓我們先介紹一些新的 DAX 函數特別針對計算群組： 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) -由計算項目來參考目前內容中的量值的運算式。 在此範例中，Sales 量值。

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) -由計算項目，來判斷在依名稱的內容中的量值的運算式。

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) -由計算項目，來判斷在內容中的量值的量值清單中指定的運算式。

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax) -由計算項目，以擷取在內容中的量值的格式字串的運算式。

### <a name="time-intelligence-example"></a>時間智慧範例

資料表名稱-**時間智慧**   
資料行名稱-**時間計算**   
優先順序- **20**   

#### <a name="time-intelligence-calculation-items"></a>時間智慧計算項目

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

**PY**

```dax
CALCULATE(SELECTEDMEASURE(), SAMEPERIODLASTYEAR(DimDate[Date]))
```

**PY MTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "MTD"
)
```

**PY QTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "QTD"
)
```

**PY YTD**

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

若要測試此計算群組，您可以在 SSMS 或開放原始碼執行 DAX 查詢[DAX Studio](http://daxstudio.org/)。 此查詢範例中將省略 YOY 和 YOY %。

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

傳回的資料表會顯示每個項目套用的計算的計算。 比方說，您可以看到適用於 2012 年 3 月 QTD 是一月、 二月和三月 2012年的總和。

![傳回的查詢](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>動態的格式字串

*動態的格式字串*與計算群組可讓量值在格式字串的條件式應用程式而不強迫以傳回字串。

表格式模型支援使用 DAX 的量值的動態格式化[格式](https://docs.microsoft.com/dax/format-function-dax)函式。 不過，FORMAT 函數缺點是傳回字串，強制執行可能會是數值，也會傳回字串形式的量值。 這會有一些限制，例如不使用大部分的 Power BI 視覺效果，取決於數字的值，例如圖表。

### <a name="dynamic-format-strings-for-time-intelligence"></a>時間智慧的動態的格式字串

如果看一下上述的時間智慧範例時，所有計算項都目除外**YOY %** 應在內容中使用目前的量值的格式。 例如， **YTD**計算銷售的基底量值應該是貨幣。 如果這是類似下訂單的基底量值的計算群組，格式會是數字。 **YOY %** ，不過，應該是基底量值的百分比表示不論格式為何。

針對**YOY %** ，我們可以將格式字串運算式屬性設定為連線，覆寫的格式字串**0.00%;-0.00%; 0.00%** 。 若要深入了解的格式字串運算式屬性，請參閱[MDX 資料格屬性-格式字串內容](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values)。

在此的矩陣視覺效果在 Power BI 中，您會看到**目前的銷售/YOY**並**訂單目前/YOY**保留其各自的基底量值的格式字串。 **銷售 YOY %** 並**排序 YOY %** ，不過，覆寫要使用的格式字串*百分比*格式。

![在矩陣視覺效果中的時間智慧](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>貨幣轉換的動態的格式字串

動態的格式字串會提供簡單的貨幣轉換。 請考慮下列 Adventure Works 資料模型。 它會針對模型化 *-一對多*所定義的貨幣轉換[轉換類型](../currency-conversions-analysis-services.md#conversion-types)。

![在表格式模型中的貨幣匯率](media/calculation-groups/calc-groups-currency-conversion.png)

A **FormatString**資料行加入至**DimCurrency**資料表，並填入個別貨幣的格式字串。

![格式字串資料行](media/calculation-groups/calc-groups-formatstringcolumn.png)

例如，下列計算群組然後定義為：

### <a name="currency-conversion-example"></a>貨幣轉換範例

資料表名稱-**貨幣轉換**   
資料行名稱-**轉換計算**   
優先順序- **5**   

#### <a name="calculation-items-for-currency-conversion"></a>貨幣轉換計算項目

**沒有任何轉換**

```dax
SELECTEDMEASURE()
```

**已轉換的貨幣**

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
格式字串運算式必須傳回純量的字串。 它會使用新[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax)函式來還原為基底量值的格式字串，如果篩選內容中有多個貨幣。

下列動畫顯示的動態格式貨幣轉換**銷售**在報表中的量值。

![套用貨幣轉換動態的格式字串](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>優先順序

優先順序是計算群組定義的屬性。 一個以上的計算群組時，它會指定評估順序。 較高的數字表示較高的優先順序，這表示會先計算群組中評估優先順序較低。

針對此範例中，我們將使用相同的模型做為時間智慧上面的範例，但也加入**平均值**計算群組。 平均計算群組包含無關的傳統時間智慧，因為它們不變更日期篩選內容-它們只適用於在其中平均計算的平均計算。

在此範例中，會定義每日平均計算。 計算，例如石油每天的平均桶通石油和天然氣應用程式中。 其他常見的商業範例包括零售存放區的平均銷售額。

雖然此類計算的計算方式與時間智慧計算無關，也可能需要將它們結合。 比方說，使用者可能會想要看到的每日檢視目前的日期年份從每日石油率的年初迄今的石油桶 」。 在此案例中，應該用於計算項目設定優先順序。

### <a name="averages-example"></a>平均的範例

資料表名稱是**平均值**。   
資料行名稱是**平均計算**。   
優先順序**10**。   

#### <a name="calculation-items-for-averages"></a>計算平均值的項目

**沒有平均值**

```dax
SELECTEDMEASURE()
```

**每日平均**

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

DAX 查詢和傳回資料表的範例如下：

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

#### <a name="averages-query-return"></a>傳回的平均查詢

![傳回的查詢](media/calculation-groups/calc-groups-ytd-daily-avg.png)

下表顯示如何計算年 3 月 2012年值。


|資料行名稱  |計算 |
|---------|---------|
|YTD     |    Jan、 Feb、 Mar 2012 的銷售總和<br />= 495,364 + 506,994 + 373,483     |
|每日平均    |     2012 年 5 月的銷售額除以 3 月的天數 #<br />= 373,483 / 31       |
|年初迄今每日平均     | 2012 年 5 月年初迄今除以 # Jan、 Feb 和 3 月中的天數<br />=  1,375,841 / (31 + 29 + 31)       |

以下是 YTD 計算項目，套用的優先順序定義**20**。

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

以下是 每日平均，套用的優先順序**10**。

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

時間智慧計算群組的優先順序會高於平均值計算群組，因為它會套用為廣泛越好。 年初迄今每日平均計算適用於 YTD 分子和分母 （計數的天數） 的每日平均計算。

這是相當於下列運算式：

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

沒有此運算式：

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>兩側的遞迴

在時間智慧上述範例中，部分計算的項目參考其他項目相同的計算群組中。 這就叫做*兩側的遞迴*。 例如， **YOY %** 同時參考**YOY**並**PY**。

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

在此情況下，這兩個運算式會個別評估因使用不同的計算陳述式。 不支援其他類型的遞迴。

## <a name="single-calculation-item-in-filter-context"></a>篩選內容中的單一計算項目

在時間智慧範例中， **PY YTD**計算項目都有一個計算運算式：

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

CALCULATE() 函式的年初迄今引數會覆寫要重複使用已經在 YTD 計算項目中定義的邏輯的篩選內容。 您不能在單一評估中套用 PY 和年初迄今。 計算群組都*只會套用*計算群組的單一計算項目是否在篩選內容。

## <a name="mdx-support"></a>MDX 支援

計算群組支援多維度資料的運算式 (MDX) 查詢。 這表示，Microsoft Excel 使用者，哪一個查詢表格式資料模型使用 MDX，可以充分利用的樞紐分析表的工作表中的計算群組和圖表。

## <a name="tools"></a>工具

計算群組尚不支援在 SQL Server Data Tools，Visual Studio 中使用 Analysis Services 延伸模組。 不過，建立計算群組使用表格式模型指令碼語言 (TMSL) 或開放原始碼[表格式編輯器](https://github.com/otykier/TabularEditor)。

## <a name="limitations"></a>限制

[物件層級安全性](object-level-security.md)(OLS) 定義計算方式不支援群組的資料表。 不過，OLS 可以定義在相同的模型中的其他資料表。 如果計算項目是指 OLS 安全的物件，則會傳回一般錯誤。

[資料列層級安全性](roles-ssas-tabular.md#bkmk_rowfliters)(RLS) 不支援。 您可以定義 RLS 的相同模型中的資料表，但不是能在計算群組本身 （直接或間接）。

[詳細資料列運算式](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)計算群組不支援。

## <a name="see-also"></a>另請參閱  

[表格式模型中的 DAX](understanding-dax-in-tabular-models-ssas-tabular.md)   
[DAX 參考](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  
