---
title: 如何使用 olapR 在 R 中建立 MDX 查詢
description: 在 SQL Server 中使用 olapR 套件程式庫, 以撰寫 R 語言腳本中的 MDX 查詢。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 09f2f1dcca3fd8d0828a87e8c781d05c4ad8e5f5
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470129"
---
# <a name="how-to-create-mdx-queries-in-r-using-olapr"></a>如何使用 olapR 在 R 中建立 MDX 查詢
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[OlapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)封裝支援針對 SQL Server Analysis Services 所裝載的 CUBE 進行 MDX 查詢。 您可以針對現有的 cube 建立查詢、流覽維度和其他 cube 物件, 並貼上現有的 MDX 查詢來抓取資料。

本文說明**olapR**套件的兩個主要用途:

+ [使用 olapR 封裝中提供的函數, 從 R 建立 MDX 查詢](#buildMDX)
+ [使用 olapR 和 OLAP 提供者執行現有的有效 MDX 查詢](#executeMDX)

不支援下列作業:

+ 針對表格式模型的 DAX 查詢
+ 建立新的 OLAP 物件
+ 回寫至資料分割, 包括量值或總和

## <a name="buildMDX"></a>從 R 建立 MDX 查詢

1. 定義可指定 OLAP 資料來源 (SSAS 執行個體) 和 MSOLAP 提供者的連接字串。

2. 使用 `OlapConnection(connectionString)` 函式建立 MDX 查詢的控制代碼，並傳遞連接字串。

3. 使用 `Query()` 建構函式具現化查詢物件。

4. 使用下列 helper 函式，以提供要包含在 MDX 查詢中之維度和量值的更多詳細資訊︰

     + `cube()` 指定 SSAS 資料庫的名稱。 如果要連接到已命名的實例, 請提供電腦名稱稱和實例名稱。 
     + `columns()`提供要在**ON COLUMNS**引數中使用的量值名稱。
     + `rows()`提供要在**ON ROWS**引數中使用的量值名稱。
     + `slicers()` 指定要用作交叉分析篩選器的欄位或成員。 交叉分析篩選器就像套用至所有 MDX 查詢資料的篩選。
     
     + `axis()` 指定要在查詢中使用之其他座標軸的名稱。 
     
         OLAP Cube 最多可以包含 128 個查詢座標軸。 一般來說, 前四個座標軸稱為資料**行**、資料**列**、**頁面**和**章節**。 
         
         如果您的查詢相當簡單，您可以使用 `columns`、 `rows`等函式來建置查詢。 不過，您也可以使用索引值非零的 `axis()` 函式來建置具有許多限定詞的 MDX 查詢，或將額外維度新增為限定詞。

5. 根據結果的形狀, 將控制碼和已完成的 MDX 查詢傳遞至下列其中一個函式: 

  + `executeMD` 傳回多維度陣列
  + `execute2D` 傳回二維 (表格式) 資料框架

## <a name="executeMDX"></a>從 R 執行有效的 MDX 查詢

1. 定義可指定 OLAP 資料來源 (SSAS 執行個體) 和 MSOLAP 提供者的連接字串。

2. 使用 `OlapConnection(connectionString)` 函式建立 MDX 查詢的控制代碼，並傳遞連接字串。

3. 定義 R 變數來儲存 MDX 查詢的文字。

4. 根據結果的形狀，將控制代碼以及包含 MDX 查詢的變數傳遞至 `executeMD` 或 `execute2D`函式。

    + `executeMD` 傳回多維度陣列
    + `execute2D` 傳回二維 (表格式) 資料框架

## <a name="examples"></a>範例

下列範例是以 AdventureWorks 資料超市和 cube 專案為基礎, 因為該專案在多個版本中是廣泛可用的, 包括可輕鬆還原為 Analysis Services 的備份檔案。 如果您沒有現有的 cube, 請使用下列其中一個選項來取得範例 cube:

+ 遵循 Analysis Services 的教學課程, 以建立用於這些範例的 cube, 直到第4課:[建立 OLAP Cube](../../analysis-services/multidimensional-tutorial/multidimensional-modeling-adventure-works-tutorial.md)

+ 下載現有的 cube 做為備份, 並將它還原到 Analysis Services 的實例。 例如, 此網站以壓縮格式提供完整處理的 cube:[艾德工作多維度模型 SQL 2014](https://msftdbprodsamples.codeplex.com/downloads/get/882334)。 解壓縮檔案, 然後將它還原至您的 SSAS 實例。 如需詳細資訊, 請參閱[Backup and restore](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)或[Restore-.asdatabase Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)。

### <a name="1-basic-mdx-with-slicer"></a>1.交叉分析篩選器的基本 MDX

這個 MDX 查詢會選取「量值」表示網際網路銷售計數和銷售量的計數和數量，並將它們放在 [資料行] 座標軸上。 它會將 SalesTerritory 維度成員新增為「交叉分析篩選器」 來篩選查詢，僅在計算中使用來自澳洲的銷售量。

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, 
{[Product].[Product Line].[Product Line].MEMBERS} ON ROWS 
FROM [Analysis Services Tutorial] 
WHERE [Sales Territory].[Sales Territory Country].[Australia]
```

+ 在資料行上，您可以指定多個量值作為以逗號區隔字串的元素。
+ [資料列] 座標軸會使用「產品線」維度的所有可能值 (所有 MEMBERS)。 
+ 此查詢會傳回含有三個數據行的資料表, 其中包含所有國家/地區的網際網路銷售_匯總_摘要。
+ WHERE 子句會指定交叉分析篩選_器軸_。 在此範例中, 交叉分析篩選器會使用**SalesTerritory**維度的成員來篩選查詢, 僅在計算中使用來自澳大利亞的銷售額。

#### <a name="to-build-this-query-using-the-functions-provided-in-olapr"></a>使用 olapR 中所提供的函式來建置此查詢

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)

qry <- Query()
cube(qry) <- "[Analysis Services Tutorial]"
columns(qry) <- c("[Measures].[Internet Sales Count]", "[Measures].[Internet Sales-Sales Amount]")
rows(qry) <- c("[Product].[Product Line].[Product Line].MEMBERS") 
slicers(qry) <- c("[Sales Territory].[Sales Territory Country].[Australia]")

result1 <- executeMD(ocs, qry)

```

若為已命名的實例, 請務必將任何可能視為控制字元的字元, 都換成 R。 例如, 下列連接字串會參考名為 ContosoHQ 的伺服器上的實例 OLAP01:

```R
cnnstr <- "Data Source=ContosoHQ\\OLAP01; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
```

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>執行這個查詢作為預先定義的 MDX 字串

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

如果您使用 SQL Server Management Studio 中的 MDX 產生器來定義查詢, 然後儲存 MDX 字串, 則會從0開始算起的座標軸編號, 如下所示: 

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Countr,y].[Australia]
```

您還是可以執行這個查詢作為預先定義的 MDX 字串。 不過, 若要使用 R 來建立相同的查詢`axis()` , 請使用函式, 您必須從1開始將座標軸重新編號。

### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2.探索 SSAS 執行個體上的 Cube 和其欄位

您可以使用 `explore` 函式傳回要在建構查詢時使用的 Cube、維度或量值清單。 如果您無法存取其他 OLAP 瀏覽工具，或您想要以程式設計方式操作或建構 MDX 查詢，則這十分方便使用。

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>列出所指定連線上的可用 Cube

若要檢視您具有檢視權限的執行個體上的所有 Cube 或檢視方塊，請提供控制代碼作為 `explore`的引數。

> [!IMPORTANT]
> 最後的結果**不**是 cube;TRUE 只表示中繼資料作業成功。 如果引數無效，則會擲回錯誤。

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)
explore(ocs)
```

| 結果  |
| ----|
| _Analysis Services 教學課程_|
|_網際網路銷售_|
|_轉售商銷售_|
|_銷售摘要_|
|_[1] TRUE_|

#### <a name="to-get-a-list-of-cube-dimensions"></a>取得 Cube 維度清單

若要檢視 Cube 或檢視方塊中的所有維度，請指定 Cube 或檢視方塊名稱。

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs \<- OlapConnection(cnnstr)
explore(ocs, "Sales")
```

| 結果  |
| ----|
| _客戶_|
|_日期_|
|_區域_|


#### <a name="to-return-all-members-of-the-specified-dimension-and-hierarchy"></a>傳回所指定維度和階層的所有成員

定義來源並建立控制代碼之後，請指定要傳回的 Cube、維度和階層。 在傳回的結果中, 前面 **->** 加上的專案代表前一個成員的子系。

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)
explore(ocs, "Analysis Services Tutorial", "Product", "Product Categories", "Category")
```

| 結果  |
| ----|
| _配件_|
|_腳踏車_|
|_服裝_|
|_元件_|
|-> 組件元件|
|-> 組件元件|


## <a name="see-also"></a>另請參閱

[在 R 中使用 OLAP cube 的資料](../../advanced-analytics/r/using-data-from-olap-cubes-in-r.md)
