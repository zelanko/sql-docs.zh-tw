---
title: "在 R 中使用 OLAP cube 的資料 |Microsoft 文件"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 1c55a5b834cd91478a87ded7ebb86884117c7bfb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="using-data-from-olap-cubes-in-r"></a>在 R 中使用 OLAP cube 的資料

**OlapR**封裝是 R 封裝，提供由 Microsoft 用於機器學習伺服器和 SQL Server R 服務，可讓您執行 MDX 查詢以從 OLAP cube 取得資料。 此套件中，您不需要建立連結的伺服器，或清除扁平化的資料列集。您可以直接在 r 中使用 OLAP 資料

本文說明的 API，以及概觀 fo OLAP 和 MDX 的 R 使用者可能是多維度 cube 資料庫的新手。

## <a name="what-is-an-olap-cube"></a>什麼是 OLAP cube？

OLAP 是短的線上分析處理。 OLAP 方案廣泛用於擷取和儲存一段時間的重要商務資料。 OLAP 資料可供各種工具、儀表板和視覺效果取用，以進行商務分析。 如需詳細資訊，請參閱[線上分析處理](https://en.wikipedia.org/wiki/Online_analytical_processing)。

Microsoft 提供[Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services)，可讓您設計、 部署及查詢的表單中的 OLAP 資料_cube_或_表格式模型_。 Cube 是多維度資料庫。 _維度_就像是 facet 的資料，或是因素： 您可以使用維度來識別特定資料子集，您想要彙總或分析。 例如，時間是重要維度，很多，所以，使許多 OLAP 方案包含多個定義配量和彙總資料時所要使用預設的行事曆。 

基於效能考量，OLAP 資料庫通常計算摘要 (或_彙總_) 事先，然後將它們儲存為更快速地擷取。 摘要根據*量值*，代表可以套用至數值資料的公式。 您使用維度來定義資料的子集，並透過該資料計算量值。 例如，您要用於量值計算特定產品線的總銷售額減去稅金，報告特定供應商、 年度至今累積薪資付費，等等的平均貨運成本的多個季。

短的多維度運算式，MDX 是查詢 cube 所使用的語言。 MDX 查詢通常會包含資料定義，其中包含一個或多個維度，以及至少一個量值、 thogh MDX 查詢可以取得也更複雜，並將包含循環 windows、 累計平均或加總，依百分位數。 

以下是當您啟動建立 MDX 查詢時可能會很有幫助的其他某些詞彙：

+ *配量*採用的 cube 子集使用從單一維度的值。

+ 「切割」 藉由在多個維度上指定值範圍來建立 Subcube。

+ 「向下鑽研」 會從摘要巡覽至詳細資料。

+ 「向上鑽研」 會從詳細資料移至更高層級的彙總。

+ 「彙總」 會摘要維度上的資料。

+ 「樞紐」 會輪流選取 Cube 或資料。

本主題提供更多的基本語法的範例 cube 上的查詢： 

+ [如何建立 MDX 查詢使用 R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR 應用程式開發介面

**olapR** 封裝支援兩種建立 MDX 查詢的方法：

- **使用 MDX 產生器。** 使用封裝中的 R 函數來產生簡單的 MDX 查詢中，選擇 cube 中，並設定座標軸和交叉分析篩選器。 這是用來建置有效的 MDX 查詢，如果您沒有存取傳統的 OLAP 工具，或不需要深入了解 MDX 語言。

    可以使用此方法，建立不是所有可能的 MDX 查詢，因為 MDX 可能會很複雜。 不過，此 API 支援大多數最常用與實用作業，包括在 N 維度中的配量、 細分、 向下鑽研、 rollup 和樞紐分析。

+ **複製-貼上 MDX 格式不正確。** 手動建立，然後貼上任何 MDX 查詢中。 這個選項最適合您有現有的 MDX 查詢，以您想要重複使用，或如果您想要建置的查詢太複雜， **olapR**來處理。 

    建置您的 MDX 使用任何用戶端公用程式，例如 SSMS 或 Excel，並儲存定義 MDX 查詢的字串。 您提供做為引數的這個 MDX 字串*SSAS 查詢處理常式*中**olapR**封裝。 函數會將查詢傳送到指定的 Analysis Services 伺服器，並回會將結果傳送給 R，假設您有當然查詢 cube 的權限。

如需如何建置 MDX 的範例查詢，或執行現有的 MDX 查詢，請參閱 <<c0> [ 如何建立 MDX 查詢使用 R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)。

## <a name="known-issues"></a>已知問題

### <a name="tabular-models-not-supported"></a>不支援表格式模型

+ 如果您連接到 Analysis services 表格式執行個體`explore`函式會報告成功傳回的值為 TRUE。 但是，表格式模型物件的不相容的型別，而且無法瀏覽。

+ 您可以使用 DAX 或 MDX 查詢表格式模型。 如果您設計有效的 MDX 查詢，針對表格式模型使用外部工具，然後將查詢貼到此應用程式開發介面時，查詢會傳回 NULL 結果，並不會報告錯誤。

## <a name="resources"></a>資源

如果您不熟悉 OLAP 或 MDX 查詢，請參閱下列維基百科文章︰ [OLAP Cube](https://en.wikipedia.org/wiki/OLAP_cube)
[MDX 查詢](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>範例

如果您想要深入了解 Cube，您可以遵循 Analysis Services 教學課程直到第 4 課： [建立 OLAP Cube](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)，以建立用於這些範例的 Cube

您也可以下載現有的 Cube 作為備份，並將它還原到 Analysis Services 的執行個體。 例如，您可以下載 [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)之完整處理的 Cube (壓縮格式)，並將它還原到 SSAS 執行個體。 如需詳細資訊，請參閱 [備份與還原](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)或 [Restore-ASDatabase Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)。
