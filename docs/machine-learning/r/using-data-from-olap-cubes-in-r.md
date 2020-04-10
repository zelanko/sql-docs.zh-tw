---
title: 在 R 中使用 OLAP Cube 的資料
description: 本文將說明 olapR API，並為可能不熟悉多維度 Cube 資料庫的 R 使用者概述 OLAP 和 MDX。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 99f67fb0fb52717eaa42e229a1b60c82f6223fad
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117231"
---
# <a name="using-data-from-olap-cubes-in-r"></a>在 R 中使用 OLAP Cube 的資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapR** 套件是由 Microsoft 提供的 R 套件，用於搭配 Machine Learning Server 和 SQL Server 使用，可讓您執行 MDX 查詢並從 OLAP Cube 取得資料。 透過此套件，您不需要建立連結的伺服器或清除扁平化資料列集；您可以直接從 R 中取得 OLAP 資料。

本文將說明 API，並為可能不熟悉多維度 Cube 資料庫的 R 使用者概述 OLAP 和 MDX。

> [!IMPORTANT]
> Analysis Services 的執行個體可支援傳統多維度 Cube 或表格式模型，但一個執行個體無法同時支援這兩種類型的模型。 因此，在您嘗試對 Cube 建立 MDX 查詢之前，請先確認 Analysis Services 執行個體是否包含多維度模型。

## <a name="what-is-an-olap-cube"></a>什麼是 OLAP Cube？

OLAP 是線上分析處理 (Online Analytical Processing) 的簡稱。 OLAP 解決方案廣泛用於擷取和儲存一段時間的重要商務資料。 OLAP 資料可供各種工具、儀表板和視覺效果取用，以進行商務分析。 如需詳細資訊，請參閱[線上分析處理](https://en.wikipedia.org/wiki/Online_analytical_processing)。

Microsoft 提供 [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services)，可讓您以「Cube」  或「表格式模型」  的形式來設計、部署和查詢 OLAP 資料。 Cube 是多維度資料庫。 「維度」  如同資料的 Facet 或 R 中的因子：您可以使用維度來識別您想要彙總或分析的某些特定資料子集。 例如，「時間」是很重要的維度，因此許多 OLAP 解決方案都包含多個預設定義的行事曆，以便在配量和彙總資料時使用。 

基於效能的考量，OLAP 資料庫通常會事先計算摘要 (或彙總  )，然後將其儲存，以便快速擷取。 摘要的基礎是「量值」  ，其代表可套用至數值資料的公式。 您可以使用維度來定義資料的子集，然後透過該資料來進算量值。 例如，您可以使用量值來計算特定產品線在多個季度中減去稅金後的總銷售額、報告特定供應商的平均運送成本和年初至今累計的薪資支付總額等等。

MDX (多維度運算式的簡稱) 是用來查詢 Cube 的語言。 MDX 查詢通常包含一個資料定義 (其中有一個或多個維度)，以及至少一個量值，但 MDX 查詢也可以更複雜，並且包含滾動視窗、累計平均值、總和、排名或百分位數。 

以下是開始建立 MDX 查詢時，可能對您有所幫助的一些其他詞彙：

+ 「配量」  會使用單一維度中的值來取得 Cube 的子集。

+ 「切割」  藉由在多個維度上指定值範圍來建立 Subcube。

+ 「向下鑽研」  會從摘要巡覽至詳細資料。

+ 「向上鑽研」  會從詳細資料移至更高層級的彙總。

+ 「彙總」  會摘要維度上的資料。

+ 「樞紐」  會輪流選取 Cube 或資料。

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>如何使用 olapR 建立 MDX 查詢

下列文章提供用來對 Cube 建立或執行查詢的語法範例詳細資料：

+ [如何使用 R 建立 MDX 查詢](../../machine-learning/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 封裝支援兩種建立 MDX 查詢的方法：

- **使用 MDX 產生器。** 選擇 Cube，然後設定軸和交叉分析篩選器，即可使用套件中的 R 函式來產生簡單的 MDX 查詢。 如果您無法存取傳統 OLAP 工具或未深入了解 MDX 語言，這是您可以輕鬆建置有效 MDX 查詢的方式。

    並非所有 MDX 查詢都可以使用此方法來建立，因為 MDX 可能很複雜。 不過，此 API 支援大部分最常見和實用的作業，包括在 N 維度中進行配量、切割、向下鑽研、彙總和樞紐。

+ **複製及貼上格式正確的 MDX。** 手動建立再貼上任何 MDX 查詢。 如果您有想要重複使用的現有 MDX 查詢，或您想要建立的查詢太複雜而 **olapR** 無法處理，這是最佳選項。

    使用任何用戶端公用程式 (例如 SSMS 或 Excel) 建置 MDX 之後，請儲存查詢字串。 提供此 MDX 字串作為 *olapR* 套件中 [SSAS 查詢處理常式]  的引數。 提供者會將查詢傳送到指定的 Analysis Services 伺服器，並將結果傳回 R。 

如需如何建立 MDX 查詢或執行現有 MDX 查詢的範例，請參閱 [如何使用 R 建立 MDX 查詢](../../machine-learning/r/how-to-create-mdx-queries-using-olapr.md)。

## <a name="known-issues"></a>已知問題

本節列出 **olapR** 套件的一些已知問題和常見問題。

### <a name="tabular-model-support"></a>表格式模型支援

如果您連線到包含表格式模型的 Analysis Services 執行個體，則 `explore` 函式會回報成功，且傳回值為 TRUE。 不過，表格式模型物件與多維度物件不同，而多維度資料庫的結構也與表格式模型的結構不同。

雖然通常與表格式模型搭配使用的語言是 DAX (資料分析運算式)，但如果您已經熟悉 MDX，可以針對表格式模型設計有效的 MDX 查詢。 您不能使用 olapR 建構函式來對表格式模型建置有效的 MDX 查詢。

不過，MDX 查詢從表格式模型中取出資料的方式較無效率。 如果您需要從表格式模型中取得在 R 中使用的資料，請考慮下列方法：

+ 在模型上啟用 DirectQuery，並在 SQL Server 中將伺服器新增為連結的伺服器。 
+ 如果表格式模型建置在關聯式資料超市上，請直接從來源取得資料。

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>如何判斷執行個體是否包含表格式或多維度模型

單一 Analysis Services 執行個體只能包含一種模型類型，但可以包含多個模型。 這是因為表格式模型和多維度模型之間有一些基本差異，控制了資料的儲存和處理方式。 例如，表格式模型會儲存在記憶體中，並利用資料行存放區索引來執行非常快速的計算。 在多維度模型中，資料會儲存在磁碟上，而彙總會預先定義，並使用 MDX 查詢來加以擷取。

如果您使用用戶端 (例如 SQL Server Management Studio) 連線到 Analysis Services，可以查看資料庫的圖示來一覽支援的模型類型。

您也可以檢視並查詢伺服器屬性，以判斷執行個體支援的模型類型。 **伺服器模式**屬性支援兩個值：「多維度」  或「表格式」  。

如需有關這兩種模型類型的一般資訊，請參閱下列文章：

+ [比較多維度和表格式模型](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

如需查詢伺服器屬性的相關資訊，請參閱下列文章：

+ [OLE DB for OLAP 結構描述資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>不支援回寫

無法將自訂 R 計算的結果寫回 Cube。

一般來說，即使已啟用 Cube 的回寫功能，也只能支援有限的作業，而且可能需要額外的設定。 我們建議您針對這類作業使用 MDX。

+ [可寫入維度](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [可寫入的資料分割](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [設定資料格資料的自訂存取權](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>長時間執行的 MDX 查詢會封鎖 Cube 處理

雖然 **olapR** 套件只會執行讀取作業，但長時間執行的 MDX 查詢可以建立鎖定來防止處理 Cube。 請務必預先測試 MDX 查詢，以了解應傳回多少資料。

如果您嘗試連線到已鎖定的 Cube，您可能會收到無法連線到 SQL Server 資料倉儲的錯誤。 建議的解決方案包括啟用遠端連線、檢查伺服器或執行個體名稱等等；不過，請考量先開啟連線的可能性。

SSAS 系統管理員可以藉由識別和終止開啟的工作階段，來防止鎖定問題。 逾期屬性也可以套用至伺服器層級上的 MDX 查詢，以強制終止所有長時間執行的查詢。

## <a name="resources"></a>資源

如果您不熟悉 OLAP 或 MDX 查詢，請參閱下列維基百科文章︰ 

+ [OLAP Cube](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 查詢](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
