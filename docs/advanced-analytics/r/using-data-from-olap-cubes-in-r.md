---
title: "在 R 中使用 OLAP Cube 的資料 | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: bdd86896b43d79b5d7cd00383476700735accff4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="using-data-from-olap-cubes-in-r"></a>在 R 中使用 OLAP Cube 的資料

**olapR** 封裝是 Microsoft R Server 和 SQL Server R 服務中提供之新的 R 封裝，可讓您執行 MDX 查詢，並在您的 R 解決方案中使用 OLAP Cube 的資料。

透過此封裝，您不需要建立連結的伺服器或清除扁平化資料列集；您可以直接在 R 中使用 OLAP 資料。

## <a name="overview"></a>概觀

OLAP Cube 是包含預先計算之「量值」 彙總的多維度資料庫，這些量值通常會擷取關鍵業務指標，例如銷售金額、銷售計數或其他數值。 OLAP Cube 廣泛用於擷取和儲存一段時間的重要商務資料。 OLAP 資料可供各種工具、儀表板和視覺效果取用，以進行商務分析。 如需詳細資訊，請參閱 [線上分析處理](https://en.wikipedia.org/wiki/Online_analytical_processing)

**olapR** 封裝支援兩種建立 MDX 查詢的方法： 

- 您可以使用 R 樣式 API 來選擇 Cube、座標軸和交叉分析篩選器，以產生簡單的 MDX 查詢。 即使您無法存取傳統 OLAP 工具或未深入了解 MDX 語言，也可以使用這些函數來建立有效的 MDX 查詢。

  請注意，在 **olapR** 封裝中使用此方法並無法建立所有 MDX 查詢，因為 MDX 可能非常複雜。 不過，它支援所有最常見和實用的作業，包括在 N 維度中進行配量、切割、向下鑽研、彙總和樞紐。

+ 您可以手動建立再貼上任何 MDX 查詢。 如果您有想要重複使用的現有 MDX 查詢，或您想要建立的查詢太複雜而 **olapR** 無法處理，此選項會很有用。 

  有了此方法，您就可以使用任何用戶端公用程式 (例如 SSMS 或 Excel) 建立 MDX 查詢，再將此查詢當做傳遞至此封裝所提供之「SSAS 查詢處理常式」  的字串引數使用。 **olapR** 函數會將查詢傳送到指定的 Analysis Services 伺服器，並將結果傳回 R。

如需如何建立 MDX 查詢或執行現有 MDX 查詢的範例，請參閱 [如何使用 R 建立 MDX 查詢](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)。


## <a name="mdx-basics"></a>MDX 基本概念

您可以使用 MDX (多維度運算式) 查詢語言擷取 Cube 中的資料。 因為 OLAP Cube (或 Analysis Services 資料庫) 中的資料是多維度而不是表格式，所以 MDX 支援複雜的語法以及各種篩選和配量資料的作業：

+ 「配量」 藉由針對一個維度挑選一個值來擷取 Cube 子集，因而產生比一個維度還要小的 Cube。 

+ 「切割」 藉由在多個維度上指定值範圍來建立 Subcube。

+ 「向下鑽研」 會從摘要巡覽至詳細資料。

+ 「向上鑽研」 會從詳細資料移至更高層級的彙總。

+ 「彙總」 會摘要維度上的資料。

+ 「樞紐」 會輪流選取 Cube 或資料。

本主題提供更多範例，下列範例示範查詢 Cube 的基本語法。
[如何使用 R 建立 MDX 查詢](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)


## <a name="known-issues"></a>已知問題

### <a name="tabular-models-not-supported-currently"></a>目前不支援表格式模型

您可以連接到 Analysis Services 的表格式執行個體， `explore` 函數會報告成功並傳回值 TRUE，但表格式模型物件不是相容類型，而且無法探索。 

表格式模型支援 MDX 查詢，但針對表格式模型的有效 MDX 查詢會傳回 NULL 結果，而且不會報告錯誤。

## <a name="resources"></a>資源

如果您不熟悉 OLAP 或 MDX 查詢，請參閱下列維基百科文章︰ [OLAP Cube](https://en.wikipedia.org/wiki/OLAP_cube)
[MDX 查詢](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>範例

如果您想要深入了解 Cube，您可以遵循 Analysis Services 教學課程直到第 4 課： [建立 OLAP Cube](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)，以建立用於這些範例的 Cube

您也可以下載現有的 Cube 作為備份，並將它還原到 Analysis Services 的執行個體。 例如，您可以下載 [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)之完整處理的 Cube (壓縮格式)，並將它還原到 SSAS 執行個體。 如需詳細資訊，請參閱 [備份與還原](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)或 [Restore-ASDatabase Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)。

## <a name="see-also"></a>另請參閱
[如何使用 R 建立 MDX 查詢](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

[Analysis Services MDX 查詢設計工具](http://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26)



