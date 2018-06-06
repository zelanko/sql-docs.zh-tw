---
title: 使用 OLAP cube 的資料在 R （SQL Server 機器學習） |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0753fc84ea6516da63e1e49dc68063780b99361b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="using-data-from-olap-cubes-in-r"></a>在 R 中使用 OLAP cube 的資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**OlapR**封裝是 R 封裝，提供由 Microsoft 用於機器學習 Server 和 SQL Server，可讓您執行 MDX 查詢以從 OLAP cube 取得資料。 此套件中，您不需要建立連結的伺服器，或清除扁平化的資料列集。您可以取得 OLAP 資料直接從。

本文說明的 API，以及的 R 使用者可能是多維度 cube 資料庫的新手 OLAP 和 MDX 的概觀。

> [!IMPORTANT]
> Analysis Services 的執行個體可以支援傳統的多維度 cube 或表格式模型中，但執行個體無法支援這兩種類型的模型。 因此，您嘗試建立對 cube 的 MDX 查詢之前，請確認 Analysis Services 執行個體包含多維度模型。

## <a name="what-is-an-olap-cube"></a>什麼是 OLAP cube？

OLAP 是短的線上分析處理。 OLAP 方案廣泛用於擷取和儲存一段時間的重要商務資料。 OLAP 資料可供各種工具、儀表板和視覺效果取用，以進行商務分析。 如需詳細資訊，請參閱[線上分析處理](https://en.wikipedia.org/wiki/Online_analytical_processing)。

Microsoft 提供[Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services)，可讓您設計、 部署及查詢的表單中的 OLAP 資料_cube_或_表格式模型_。 Cube 是多維度資料庫。 _維度_就像是 facet 的資料，或是因素： 您可以使用維度來識別特定資料子集，您想要彙總或分析。 例如，時間是重要維度，很多，所以，使許多 OLAP 方案包含多個定義配量和彙總資料時所要使用預設的行事曆。 

基於效能考量，OLAP 資料庫通常計算摘要 (或_彙總_) 事先，然後將它們儲存為更快速地擷取。 摘要根據*量值*，代表可以套用至數值資料的公式。 您使用維度來定義資料的子集，並透過該資料計算量值。 例如，您要用於量值計算特定產品線的總銷售額減去稅金，報告特定供應商、 年度至今累積薪資付費，等等的平均貨運成本的多個季。

短的多維度運算式，MDX 是查詢 cube 所使用的語言。 MDX 查詢通常會包含資料定義包含一或多個維度和至少一個量值，MDX 查詢可以取得也更複雜，而且包括輪流 windows、 累積平均值、 總和、 排列次序或依百分位數。 

以下是當您啟動建立 MDX 查詢時可能會很有幫助的其他某些詞彙：

+ *配量*採用的 cube 子集使用從單一維度的值。

+ 「切割」 藉由在多個維度上指定值範圍來建立 Subcube。

+ 「向下鑽研」 會從摘要巡覽至詳細資料。

+ 「向上鑽研」 會從詳細資料移至更高層級的彙總。

+ 「彙總」 會摘要維度上的資料。

+ 「樞紐」 會輪流選取 Cube 或資料。

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>如何使用 olapR 建立 MDX 查詢

下列文章提供詳細的建立，或對 cube 執行查詢的語法範例：

+ [如何建立 MDX 查詢使用 R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR 應用程式開發介面

**olapR** 封裝支援兩種建立 MDX 查詢的方法：

- **使用 MDX 產生器。** 使用封裝中的 R 函數來產生簡單的 MDX 查詢，方式是選擇 cube，然後設定 軸和交叉分析篩選器。 這是用來建置有效的 MDX 查詢，如果您沒有存取傳統的 OLAP 工具，或不需要深入了解 MDX 語言。

    可以使用此方法，建立不是所有的 MDX 查詢，因為 MDX 可能會很複雜。 不過，此 API 支援大多數最常用與實用作業，包括在 N 維度中的配量、 細分、 向下鑽研、 rollup 和樞紐分析。

+ **複製-貼上 MDX 格式不正確。** 手動建立，然後貼上任何 MDX 查詢中。 這個選項最適合您有現有的 MDX 查詢，以您想要重複使用，或如果您想要建置的查詢太複雜， **olapR**來處理。

    在建置您的 MDX 使用任何用戶端公用程式，例如 SSMS 或 Excel 之後, 將儲存的查詢字串。 提供這個 MDX 字串做為引數*SSAS 查詢處理常式*中**olapR**封裝。 提供者會將查詢傳送到指定的 Analysis Services 伺服器，並回會將結果傳遞到。 

如需如何建置 MDX 的範例查詢，或執行現有的 MDX 查詢，請參閱 <<c0> [ 如何建立 MDX 查詢使用 R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)。

## <a name="known-issues"></a>已知問題

本節列出有關的一些已知的問題和常見問題的解答**olapR**封裝。

### <a name="tabular-model-support"></a>表格式模型支援

如果您連接到包含表格式模型中，Analysis services 執行個體`explore`函式會報告成功傳回的值為 TRUE。 不過，表格式模型物件不同於多維度物件，而且多維度資料庫的結構是不同的表格式模型。

雖然 DAX （資料分析運算式） 通常會搭配表格式模型的語言，您可以設計有效的 MDX 查詢，針對表格式模型中，如果您已經熟悉 MDX。 您無法使用 olapR 建構函式來建立有效的 MDX 查詢，針對表格式模型。

不過，MDX 查詢會從表格式模型擷取資料的效率不佳的方式。 如果您需要在 R 中使用表格式模型取得資料，請改為考慮下列方法：

+ 啟用 DirectQuery 模型上，將伺服器新增為 SQL Server 中連結的伺服器。 
+ 如果在關聯式資料超市上建置表格式模型時，請直接從來源取得的資料。

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>如何判斷執行個體是否包含表格式或多維度模型

單一 Analysis Services 執行個體可以包含一種模型，但它可以包含多個模型。 原因是表格式模型和控制的方式是進行儲存及處理資料的多維度模型的基本差異。 例如，表格式模型儲存在記憶體中，並利用執行非常快速的計算資料行存放區索引。 在多維度模型中，資料會儲存在磁碟上，預先定義及使用 MDX 查詢擷取彙總。

如果您連接到 Analysis Services 使用 SQL Server Management Studio 之類的用戶端，您可以立即判斷出支援的模型類型，藉由查看資料庫的圖示。

您也可以檢視和查詢來判斷哪些類型的模型執行個體支援的伺服器屬性。 **伺服器模式**屬性支援兩個值：_多維度_或_表格式_。

請參閱下列文件的兩種模型類型的一般資訊：

+ [比較多維度和表格式模型](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

請參閱下列文件的查詢伺服器屬性的相關資訊：

+ [OLE DB for OLAP 結構描述資料列集](https://docs.microsoft.com/sql/analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>不支援回寫

您不可能將自訂 R 計算結果寫回 cube。

一般情況下，即使已啟用回寫 cube，支援有限的作業，並可能還需要額外的設定。 我們建議您進行此類作業使用 MDX。

+ [啟用寫入的維度](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [寫入的資料分割](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [設定資料格資料的自訂存取](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>長時間執行的 MDX 查詢封鎖 cube 處理

雖然**olapR**封裝執行只讀取的作業，長時間執行的 MDX 查詢可以建立防止在處理 cube 的鎖定。 一律在以了解應傳回多少資料，事先測試 MDX 查詢。

如果您嘗試連接到已鎖定的 cube，您可能會無法連線到 SQL Server 資料倉儲發生錯誤。 建議的解決方式包括： 啟用遠端連線，檢查伺服器或執行個體名稱及其他等等。不過，請考慮先前開啟連線的可能性。

SSAS 系統管理員可以防止識別並終止開啟工作階段鎖定問題。 Timeout 屬性也可以套用至伺服器層級強制終止長時間執行的所有查詢的 MDX 查詢。

## <a name="resources"></a>資源

如果您不熟悉 OLAP 或 MDX 查詢，請參閱這些維基百科文章： 

+ [OLAP cube](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 查詢](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
