---
title: 在 R 中使用 olapR 建立 MDX 查詢
description: 了解如何在 SQL Server 中使用 olapR 套件程式庫撰寫 MDX 查詢，或以 R 語言指令碼執行現有的 MDX 查詢。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 05/22/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5789a0791654b89ac78f9333cb71e10f3ca9322e
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173667"
---
# <a name="how-to-create-mdx-queries-in-r-using-olapr"></a>如何在 R 中使用 olapR 建立 MDX 查詢
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) \(英文\) 套件針對 SQL Server Analysis Services 中裝載的 Cube 支援 MDX 查詢。 您可以針對現有的 Cube 建置查詢、瀏覽維度和其他 Cube 物件，並貼上現有的 MDX 查詢來取出資料。

本文將說明 **olapR** 套件的兩個主要用法：

+ [使用 olapR 套件中提供的建構函式，從 R 建置 MDX 查詢](#buildMDX)
+ [使用 olapR 和 OLAP 提供者來執行現有的有效 MDX 查詢](#executeMDX)

不支援下列作業：

+ 針對表格式模型進行 DAX 查詢
+ 建立新的 OLAP 物件
+ 回寫至分割區，包括量值或總和

## <a name="build-an-mdx-query-from-r"></a><a name="buildMDX"></a> 從 R 建置 MDX 查詢

1. 定義可指定 OLAP 資料來源 (SSAS 執行個體) 和 MSOLAP 提供者的連接字串。

2. 使用 `OlapConnection(connectionString)` 函式建立 MDX 查詢的控制代碼，並傳遞連接字串。

3. 使用 `Query()` 建構函式具現化查詢物件。

4. 使用下列 helper 函式，以提供要包含在 MDX 查詢中之維度和量值的更多詳細資訊︰

     + `cube()` 指定 SSAS 資料庫的名稱。 如果要連線到具名執行個體，請提供電腦名稱和執行個體名稱。 
     + `columns()` 提供要在 **ON COLUMNS** 引數中使用的量值名稱。
     + `rows()` 提供要在 **ON ROWS** 引數中使用的量值名稱。
     + `slicers()` 指定要用作交叉分析篩選器的欄位或成員。 交叉分析篩選器就像套用至所有 MDX 查詢資料的篩選。
     
     + `axis()` 指定要在查詢中使用之其他座標軸的名稱。 
     
         OLAP Cube 最多可以包含 128 個查詢座標軸。 前四個軸通常稱為**資料行**、**資料列**、**頁面**和**章節**。 
         
         如果您的查詢相當簡單，您可以使用 `columns`、 `rows`等函式來建置查詢。 不過，您也可以使用索引值非零的 `axis()` 函式來建置具有許多限定詞的 MDX 查詢，或將額外維度新增為限定詞。

5. 根據結果的圖形，將控制代碼和完成的 MDX 查詢傳遞至下列其中一個函式： 

  + `executeMD` 傳回多維度陣列
  + `execute2D` 傳回二維 (表格式) 資料框架

## <a name="execute-a-valid-mdx-query-from-r"></a><a name="executeMDX"></a> 從 R 執行有效的 MDX 查詢

1. 定義可指定 OLAP 資料來源 (SSAS 執行個體) 和 MSOLAP 提供者的連接字串。

2. 使用 `OlapConnection(connectionString)` 函式建立 MDX 查詢的控制代碼，並傳遞連接字串。

3. 定義 R 變數來儲存 MDX 查詢的文字。

4. 根據結果的形狀，將控制代碼以及包含 MDX 查詢的變數傳遞至 `executeMD` 或 `execute2D`函式。

    + `executeMD` 傳回多維度陣列
    + `execute2D` 傳回二維 (表格式) 資料框架

## <a name="examples"></a>範例

下列範例會以 AdventureWorks 資料超市和 Cube 專案為基礎，因為該專案可在多個版本中廣泛使用，包括能夠輕鬆還原到 Analysis Services 的備份檔案。 如果您目前沒有 Cube，可使用下列其中一個選項來取得範例 Cube：

+ 若要建立可用於這些範例的 Cube，請遵循 Analysis Services 教學課程，直到第 4 課：[建立 OLAP Cube](https://docs.microsoft.com/analysis-services/multidimensional-tutorial/multidimensional-modeling-adventure-works-tutorial) \(部分機器翻譯\)

+ 下載現有的 Cube 作為備份，並將它還原到 Analysis Services 的執行個體。 例如，此網站會以壓縮格式提供完整處理的 Cube：[Adventure Works 多維度模型 SQL 2014](https://msftdbprodsamples.codeplex.com/downloads/get/882334)。 將檔案解壓縮，然後將它還原到您的 SSAS 執行個體。 如需詳細資訊，請參閱[備份與還原](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases) \(部分機器翻譯\) 或 [Restore-ASDatabase Cmdlet](/powershell/module/sqlserver/restore-asdatabase)。

### <a name="1-basic-mdx-with-slicer"></a>1.交叉分析篩選器的基本 MDX

這個 MDX 查詢會選取「量值」  表示網際網路銷售計數和銷售量的計數和數量，並將它們放在 [資料行] 座標軸上。 它會將 SalesTerritory 維度成員新增為「交叉分析篩選器」  來篩選查詢，僅在計算中使用來自澳洲的銷售量。

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, 
{[Product].[Product Line].[Product Line].MEMBERS} ON ROWS 
FROM [Analysis Services Tutorial] 
WHERE [Sales Territory].[Sales Territory Country].[Australia]
```

+ 在資料行上，您可以指定多個量值作為以逗號區隔字串的元素。
+ [資料列] 座標軸會使用「產品線」維度的所有可能值 (所有 MEMBERS)。 
+ 此查詢會傳回包含三個資料行的資料表，內含所有國家/地區之網際網路銷售量的「彙總」  摘要。
+ WHERE 子句會指定「交叉分析篩選器軸」  。 在此範例中，交叉分析篩選器會使用 **SalesTerritory** 維度成員來篩選查詢，因此，計算中僅會使用來自澳洲的銷售量。

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

如果是具名執行個體，請務必逸出任何可能在 R 中被視為控制字元的字元。例如，下列連接字串會參考名為 ContosoHQ 之伺服器上的執行個體 OLAP01：

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

如果您使用 SQL Server Management Studio 中的 MDX 建立器來定義查詢，然後儲存 MDX 字串，則會從 0 開始對軸進行編號，如下所示： 

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Countr,y].[Australia]
```

您還是可以執行這個查詢作為預先定義的 MDX 字串。 不過，若要利用 R 使用 `axis()` 函式來建置相同查詢，就必須從 1 開始對軸進行編號。

### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2.探索 SSAS 執行個體上的 Cube 和其欄位

您可以使用 `explore` 函式傳回要在建構查詢時使用的 Cube、維度或量值清單。 如果您無法存取其他 OLAP 瀏覽工具，或您想要以程式設計方式操作或建構 MDX 查詢，則這十分方便使用。

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>列出所指定連線上的可用 Cube

若要檢視您具有檢視權限的執行個體上的所有 Cube 或檢視方塊，請提供控制代碼作為 `explore`的引數。

> [!IMPORTANT]
> 最終結果**不是** Cube；TRUE 僅表示中繼資料作業成功。 如果引數無效，則會擲回錯誤。

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

定義來源並建立控制代碼之後，請指定要傳回的 Cube、維度和階層。 在傳回結果中，前面加上 **->** 的項目代表前一個成員的子系。

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)
explore(ocs, "Analysis Services Tutorial", "Product", "Product Categories", "Category")
```

| 結果  |
| ----|
| _Accessories_|
|_Bikes_|
|_Clothing_|
|_Components_|
|-> 組件元件|
|-> 組件元件|


## <a name="see-also"></a>另請參閱

[在 R 中使用 OLAP Cube 的資料](../../machine-learning/r/using-data-from-olap-cubes-in-r.md)
