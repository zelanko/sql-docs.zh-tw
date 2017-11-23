---
title: "如何使用 olapR 來建立 MDX 查詢 | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: c12b988e-be7e-41ba-a84c-299a5c45d4ab
caps.latest.revision: "3"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 04dc669f1ca6e472bf66b3795cf3096e9fa77f0d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="how-to-create-mdx-queries-using-olapr"></a>如何使用 olapR 建立 MDX 查詢
## <a name="how-to-build-an-mdx-query-from-r"></a>如何從 R 建置 MDX 查詢

1. 定義可指定 OLAP 資料來源 (SSAS 執行個體) 和 MSOLAP 提供者的連接字串。

2. 使用 `OlapConnection(connectionString)` 函式建立 MDX 查詢的控制代碼，並傳遞連接字串。

3. 使用 `Query()` 建構函式具現化查詢物件。

4. 使用下列 helper 函式，以提供要包含在 MDX 查詢中之維度和量值的更多詳細資訊︰
     + `cube()` 指定 SSAS 資料庫的名稱。
     + `columns()` 提供要在 ON COLUMNS 引數中使用的量值名稱。  
     + `rows()` 提供要在 ON ROWS 引數中使用的量值名稱。
     + `slicers()` 指定要用作交叉分析篩選器的欄位或成員。 交叉分析篩選器就像套用至所有 MDX 查詢資料的篩選。
     
     + `axis()` 指定要在查詢中使用之其他座標軸的名稱。 OLAP Cube 最多可以包含 128 個查詢座標軸。 前四個座標軸一般稱為「資料行」、「資料列」、「頁面」和「章節」。 如果您的查詢相當簡單，您可以使用 `columns`、 `rows`等函式來建置查詢。     
     不過，您也可以使用索引值非零的 `axis()` 函式來建置具有許多限定詞的 MDX 查詢，或將額外維度新增為限定詞。

5. 根據結果的形狀，將控制代碼和已完成 MDX 查詢傳遞至 `executeMD` 或 `execute2D`函式。

  + `executeMD` 傳回多維度陣列
  + `execute2D` 傳回二維 (表格式) 資料框架


## <a name="how-to-run-an-existing-mdx-query-from-r"></a>如何從 R 執行現有 MDX 查詢

1. 定義可指定 OLAP 資料來源 (SSAS 執行個體) 和 MSOLAP 提供者的連接字串。

2. 使用 `OlapConnection(connectionString)` 函式建立 MDX 查詢的控制代碼，並傳遞連接字串。

3. 定義 R 變數來儲存 MDX 查詢的文字。

4. 根據結果的形狀，將控制代碼以及包含 MDX 查詢的變數傳遞至 `executeMD` 或 `execute2D`函式。

    + `executeMD` 傳回多維度陣列
    + `execute2D` 傳回二維 (表格式) 資料框架



## <a name="examples"></a>範例

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
+ 這個查詢會傳回包含三個資料行的資料表，內含所有國家/地區的網際網路銷售量的「積存」  摘要。 
+ WHERE 子句是「交叉分析篩選器座標軸」 。 交叉分析篩選器會使用 SalesTerritory 維度成員來篩選查詢，僅在計算中使用來自澳洲的銷售量。

#### <a name="to-build-this-query-using-the-functions-provided-in-olapr"></a>使用 olapR 中所提供的函式來建置此查詢

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

qry <- Query()
cube(qry) <- "[Analysis Services Tutorial]"
columns(qry) <- c("[Measures].[Internet Sales Count]", "[Measures].[Internet Sales-Sales Amount]")
rows(qry) <- c("[Product].[Product Line].[Product Line].MEMBERS") 
slicers(qry) <- c("[Sales Territory].[Sales Territory Country].[Australia]")

result1 <- executeMD(ocs, qry)

```

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>執行這個查詢作為預先定義的 MDX 字串

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

請注意，如果您使用 SQL Server Management Studio 中的 MDX 產生器來定義查詢，然後儲存 MDX 字串，則會從 0 開始對座標軸進行編號，如下所示︰ 

~~~~
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Country].[Australia]
~~~~

您還是可以執行這個查詢作為預先定義的 MDX 字串。 不過，若要使用 R 並使用 `axis()` 函式來建置相同查詢，請一定要從1 開始對座標軸進行編號。


### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2.探索 SSAS 執行個體上的 Cube 和其欄位

您可以使用 `explore` 函式傳回要在建構查詢時使用的 Cube、維度或量值清單。 如果您無法存取其他 OLAP 瀏覽工具，或您想要以程式設計方式操作或建構 MDX 查詢，則這十分方便使用。

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>列出所指定連線上的可用 Cube

若要檢視您具有檢視權限的執行個體上的所有 Cube 或檢視方塊，請提供控制代碼作為 `explore`的引數。
請注意，最終結果不是 Cube；TRUE 僅表示中繼資料作業成功。 如果引數無效，則會擲回錯誤。

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
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
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs \<- OlapConnection(cnnstr)
explore(ocs, "Sales")
```

| 結果  |  
| ----|
| _客戶_|
|_日期_|
|_區域_|


#### <a name="to-return-all-members-of-the-specified-dimension-and-hierarchy"></a>傳回所指定維度和階層的所有成員

定義來源並建立控制代碼之後，請指定要傳回的 Cube、維度和階層。
請注意，傳回結果中前面加上 **->** 的項目代表前一個成員的子系。

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs \<- OlapConnection(cnnstr)
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

[在 R 中使用 OLAP Cube 的資料](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md)
