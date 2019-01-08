---
title: R-SQL Server Machine Learning 服務中使用 OLAP cube 的資料
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 347698d2df937b7b64c941ceac81906dcaabbeae
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432631"
---
# <a name="using-data-from-olap-cubes-in-r"></a>在 R 中使用 OLAP cube 的資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**OlapR**封裝是 R 封裝，提供由 Microsoft 與 Machine Learning Server 和 SQL Server 搭配使用，可讓您執行 MDX 查詢，以從 OLAP cube 取得資料。 使用此套件中，您不需要建立連結的伺服器，或清除扁平化資料列集;您可以直接從 r 取得 OLAP 資料

本文說明 API，以及 R 使用者可能是多維度 cube 資料庫的新手 OLAP 和 MDX 的概觀。

> [!IMPORTANT]
> Analysis Services 的執行個體可以支援傳統的多維度 cube 或表格式模型中，但執行個體無法支援這兩種類型的模型。 因此，您嘗試建立對 cube 的 MDX 查詢之前，請確認 Analysis Services 執行個體包含多維度模型。

## <a name="what-is-an-olap-cube"></a>什麼是 OLAP cube？

OLAP 是簡短的線上分析處理。 OLAP 方案廣泛用於擷取和儲存一段時間的重要商務資料。 OLAP 資料可供各種工具、儀表板和視覺效果取用，以進行商務分析。 如需詳細資訊，請參閱 <<c0> [ 線上分析處理](https://en.wikipedia.org/wiki/Online_analytical_processing)。

Microsoft 提供[Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services)，這可讓您設計、 部署及查詢 OLAP 資料的形式_cube_或是_表格式模型_。 Cube 是多維度資料庫。 _維度_等層面的資料或在 r 中的因素是您用來識別特定資料子集，您想要彙總或分析的維度。 例如，時間是重要維度，這麼多，使許多的 OLAP 方案包含多個定義配量和彙總資料時使用預設的行事曆。 

基於效能考量，OLAP 資料庫通常計算摘要 (或_彙總_) 事先，然後再將它們儲存為更快速地擷取。 摘要根據*量值*，代表可以套用至數值資料的公式。 您會使用維度來定義資料的子集，並再將量值計算該資料。 比方說，您會使用的量值來計算特定產品線的總銷售額減去稅金，以報告特定供應商、 年初至今累積的薪資，付費，等等的平均貨運成本的多個季。

MDX 中，短的多維度運算式，是用來查詢 cube 的語言。 MDX 查詢通常會包含資料定義包含一或多個維度和至少一個量值，雖然 MDX 查詢可以取得可能更複雜，並包括輪流 windows、 累積平均值、 總和、 陣序規範或百分位數。 

以下是當您開始建立 MDX 查詢時可能會很有幫助的一些其他詞彙：

+ *配量*採用的 cube 子集，藉由使用來自單一維度的值。

+ 「切割」 藉由在多個維度上指定值範圍來建立 Subcube。

+ 「向下鑽研」 會從摘要巡覽至詳細資料。

+ 「向上鑽研」 會從詳細資料移至更高層級的彙總。

+ 「彙總」 會摘要維度上的資料。

+ 「樞紐」 會輪流選取 Cube 或資料。

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>如何使用 olapR 建立 MDX 查詢

下列文章提供詳細的建立，或針對 cube 執行查詢的語法的範例：

+ [如何建立使用 R 的 MDX 查詢](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 封裝支援兩種建立 MDX 查詢的方法：

- **使用 MDX 產生器。** 在封裝中使用 R 函數，來產生簡單的 MDX 查詢中，選擇的 cube，然後設定 軸和交叉分析篩選器。 這是簡單的方法，來建置有效的 MDX 查詢，如果您不需要存取傳統 OLAP 工具，或不需要深入了解 MDX 語言。

    可以使用此方法中，建立不是所有的 MDX 查詢，因為 MDX 可能非常複雜。 不過，此 API 支援大部分的最常見和實用的作業，包括在 N 維度中的配量、 分析、 向下鑽研、 彙總套件和樞紐分析。

+ **複製-貼上語式正確的 MDX。** 手動建立，然後再貼上任何 MDX 查詢。 如果您有現有的 MDX 查詢，以您想要重複使用，或如果您想要建置的查詢太過複雜的這個選項會是最佳**olapR**來處理。

    在建置使用任何用戶端公用程式，例如 SSMS 或 Excel，MDX 之後儲存的查詢字串。 提供此 MDX 字串做為引數*SSAS 查詢處理常式*中**olapR**封裝。 提供者會將查詢傳送至指定的 Analysis Services 伺服器，並傳回結果。 

如範例，示範如何建立 MDX 查詢，或執行現有 MDX 查詢，請參閱 <<c0> [ 如何建立 MDX 查詢使用 R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)。

## <a name="known-issues"></a>已知問題

本節列出有關的一些已知的問題和常見問題**olapR**封裝。

### <a name="tabular-model-support"></a>表格式模型支援

如果您連接到包含表格式模型中，Analysis services 執行個體`explore`函式會報告成功，傳回的值為 TRUE。 表格式模型物件屬於不同於多維度物件，但多維度資料庫的結構是不同的表格式模型中。

雖然 DAX （資料分析運算式） 通常使用表格式模型的語言，您可以設計有效的 MDX 查詢，針對表格式模型中，如果您已經很熟悉 MDX。 您無法使用 olapR 建構函式來建置有效的 MDX 查詢，針對表格式模型。

不過，MDX 查詢會從表格式模型擷取資料的效率不佳的方式。 如果您需要取得在 R 中使用表格式模型中的資料，請改為考慮下列方法：

+ 啟用 DirectQuery 的模型，並將伺服器新增為 SQL Server 中連結的伺服器。 
+ 如果表格式模型關聯式資料超市上所建置，請直接從來源取得的資料。

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>如何判斷執行個體是否包含表格式或多維度模型

單一的 Analysis Services 執行個體可以包含只有一種模型類型，但它可以包含多個模型。 原因時，即是表格式模型和控制的方式儲存和處理資料的多維度模型的基本差異。 比方說，表格式模型會儲存在記憶體，並利用執行非常快速的計算資料行存放區索引。 在多維度模型中，資料會儲存在磁碟上，預先定義和使用 MDX 查詢擷取彙總。

如果您連接到 Analysis Services 使用 SQL Server Management Studio 之類的用戶端，您可以立即判斷一目瞭然模型所支援的類型，藉由查看資料庫的圖示。

您也可以檢視和查詢來判斷哪一種模型執行個體支援的伺服器屬性。 **伺服器模式**屬性支援兩個值：_多維度_或是_表格式_。

請參閱下列文章中有兩種模型類型的一般資訊：

+ [比較多維度和表格式模型](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

請參閱下列文章中有查詢伺服器屬性的相關資訊：

+ [OLE DB for OLAP 結構描述資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>不支援回寫

您不可能的自訂 R 計算結果寫回 cube。

一般情況下，即使在 cube 中啟用回寫時，支援只有有限的作業，並可能需要額外的設定。 我們建議您針對這類作業使用 MDX。

+ [可寫入維度](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [寫入的資料分割](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [設定資料格資料的自訂存取](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>長時間執行的 MDX 查詢會封鎖 cube 處理

雖然**olapR**封裝執行只有讀取的作業，長時間執行的 MDX 查詢可以建立防止在處理 cube 的鎖定。 一律在好讓您知道應傳回多少資料，事先測試您的 MDX 查詢。

如果您嘗試連接到已鎖定的 cube，您可能會發生無法連線到 SQL Server 資料倉儲的錯誤。 建議的解決方式包括啟用遠端連線，檢查伺服器或執行個體名稱，以及等等，不過，請考慮先前開啟的連接的可能性。

SSAS 系統管理員可以防止透過識別並結束開啟的工作階段鎖定問題。 Timeout 屬性也可以套用至伺服器層級來強制結束長時間執行的所有查詢的 MDX 查詢。

## <a name="resources"></a>資源

如果您不熟悉 OLAP 或 MDX 查詢，請參閱下列維基百科文章： 

+ [OLAP cube](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 查詢](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
