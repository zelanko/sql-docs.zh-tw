---
title: 在 R 中使用 OLAP cube 的資料
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3063758e1186dc81e5ce9e70891403e7afd3a89f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345108"
---
# <a name="using-data-from-olap-cubes-in-r"></a>在 R 中使用 OLAP cube 的資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**OlapR**套件是由 Microsoft 提供的 R 封裝, 用於 Machine Learning Server 和 SQL Server, 可讓您執行 MDX 查詢以從 OLAP cube 取得資料。 使用此封裝時, 您不需要建立連結的伺服器或清除壓平合併的資料列集;您可以直接從 R 取得 OLAP 資料。

本文說明 API, 並概述適用于可能不熟悉多維度 cube 資料庫的 R 使用者的 OLAP 和 MDX。

> [!IMPORTANT]
> Analysis Services 的實例可以支援傳統多維度 cube 或表格式模型, 但實例無法同時支援這兩種類型的模型。 因此, 在您嘗試針對 cube 建立 MDX 查詢之前, 請先確認 Analysis Services 實例包含多維度模型。

## <a name="what-is-an-olap-cube"></a>什麼是 OLAP Cube？

OLAP 是線上分析處理的簡短。 OLAP 解決方案廣泛用於在一段時間內捕捉和儲存重要的商務資料。 OLAP 資料可供各種工具、儀表板和視覺效果取用，以進行商務分析。 如需詳細資訊, 請參閱[線上分析處理](https://en.wikipedia.org/wiki/Online_analytical_processing)。

Microsoft 提供[Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), 可讓您以_cube_或_表格式模型_的形式來設計、部署和查詢 OLAP 資料。 Cube 是多維度資料庫。 _維度_類似資料的 Facet 或 R 中的因素: 您可以使用維度來識別您想要摘要或分析的某些特定資料子集。 例如, 「時間」是很重要的維度, 因此許多 OLAP 解決方案都包含預設定義的多個行事曆, 以便在切割和匯總資料時使用。 

基於效能的考慮, OLAP 資料庫通常會事先計算摘要  (或匯總), 然後儲存它們以供更快速的抓取。 摘要是以*量值*為基礎, 代表可套用至數值資料的公式。 您可以使用維度來定義資料的子集, 然後計算該資料的量值。 例如, 您可以使用量值來計算在多季減去稅金的特定產品明細的總銷售額, 以報告特定供應商、年初累計薪資付費的平均運送成本等等。

MDX (多維度運算式的 short) 是用來查詢 cube 的語言。 MDX 查詢通常包含一個資料定義, 其中包含一或多個維度, 以及至少一個量值, 但 MDX 查詢可能會變得更複雜, 而且包含滾動視窗、累計平均值、總和、次序或百分位數。 

以下是當您開始建立 MDX 查詢時, 可能會有説明的一些其他詞彙:

+  切割會使用單一維度中的值來取得 cube 的子集。

+ 「切割」  藉由在多個維度上指定值範圍來建立 Subcube。

+ 「向下鑽研」  會從摘要巡覽至詳細資料。

+ 「向上鑽研」  會從詳細資料移至更高層級的彙總。

+ 「彙總」  會摘要維度上的資料。

+ 「樞紐」  會輪流選取 Cube 或資料。

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>如何使用 olapR 建立 MDX 查詢

下列文章提供針對 cube 建立或執行查詢的語法詳細範例:

+ [如何使用 R 建立 MDX 查詢](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

**olapR** 封裝支援兩種建立 MDX 查詢的方法：

- **使用 MDX 產生器。** 使用封裝中的 R 函數來產生簡單的 MDX 查詢, 方法是選擇 cube, 然後設定軸和交叉分析篩選器。 如果您沒有傳統 OLAP 工具的存取權, 或沒有對 MDX 語言的深入瞭解, 這就是建立有效 MDX 查詢的簡單方法。

    並非所有 MDX 查詢都可以使用這個方法來建立, 因為 MDX 可能很複雜。 不過, 此 API 支援大部分最常見且實用的作業, 包括在 N 個維度中的配量、骰子、明細、匯總和資料透視。

+ **複製-貼上格式正確的 MDX。** 以手動方式建立, 然後貼上任何 MDX 查詢。 如果您有想要重複使用的現有 MDX 查詢, 或如果您想要建立的查詢太複雜而無法處理**olapR** , 這個選項就是最佳選擇。

    使用任何用戶端公用程式 (例如 SSMS 或 Excel) 建立 MDX 之後, 請儲存查詢字串。 提供此 MDX 字串做為**olapR**封裝中*SSAS 查詢處理常式*的引數。 提供者會將查詢傳送到指定的 Analysis Services 伺服器, 並將結果傳回 R。 

如需如何建立 MDX 查詢或執行現有 MDX 查詢的範例, 請參閱[如何使用 R 建立 mdx 查詢](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)。

## <a name="known-issues"></a>已知問題

本節列出**olapR**套件的一些已知問題和常見問題。

### <a name="tabular-model-support"></a>表格式模型支援

如果您連接到包含表格式模型 Analysis Services 的實例, 此`explore`函式會回報成功, 傳回值為 TRUE。 不過, 表格式模型物件與多維度物件不同, 而多維度資料庫的結構與表格式模型不同。

雖然 DAX (資料分析運算式) 是通常與表格式模型搭配使用的語言, 如果您已經熟悉 MDX, 可以針對表格式模型設計有效的 MDX 查詢。 您不能使用 olapR 的函式, 針對表格式模型建立有效的 MDX 查詢。

不過, MDX 查詢是從表格式模型中取出資料的無效率方式。 如果您需要從表格式模型取得資料以用於 R, 請考慮下列方法:

+ 在模型上啟用 DirectQuery, 並在 SQL Server 中將伺服器新增為連結的伺服器。 
+ 如果表格式模型是建立在關聯式資料超市上, 請直接從來源取得資料。

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>如何判斷實例是否包含表格式或多維度模型

單一 Analysis Services 實例只能包含一種模型, 雖然它可以包含多個模型。 原因在於, 表格式模型和多維度模型之間有一些基本差異, 可控制資料的儲存和處理方式。 例如, 表格式模型會儲存在記憶體中, 並利用資料行存放區索引來執行非常快速的計算。 在多維度模型中, 資料會儲存在磁片上, 而且匯總會預先定義, 並使用 MDX 查詢加以取出。

如果您使用用戶端 (例如 SQL Server Management Studio) 連接到 Analysis Services, 您可以查看資料庫的圖示, 以概覽支援的模型類型。

您也可以查看並查詢伺服器屬性, 以決定實例支援的模型類型。 **伺服器模式**屬性支援兩個值: 多_維度_或_表格式_。

如需這兩種模型類型的一般資訊, 請參閱下列文章:

+ [比較多維度和表格式模型](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

如需查詢伺服器屬性的相關資訊, 請參閱下列文章:

+ [OLE DB for OLAP 結構描述資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>不支援回寫

無法將自訂 R 計算的結果寫回 cube。

一般來說, 即使已啟用 cube 的回寫功能, 只支援有限的作業, 而且可能需要額外的設定。 我們建議您針對這類作業使用 MDX。

+ [可寫入維度](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [可寫入的磁碟分割](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [設定資料格資料的自訂存取](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>長時間執行的 MDX 查詢會封鎖 cube 處理

雖然**olapR**封裝只會執行讀取作業, 但長時間執行的 MDX 查詢可以建立鎖定來防止處理 cube。 請務必事先測試 MDX 查詢, 以便知道應傳回多少資料。

如果您嘗試連接到已鎖定的 cube, 您可能會收到無法連線到 SQL Server 資料倉儲的錯誤。 建議的解決方式包括啟用遠端連線、檢查伺服器或實例名稱等等;不過, 請考慮先前開啟連接的可能性。

SSAS 系統管理員可以藉由識別和終止開啟的會話, 來防止鎖定問題。 Timeout 屬性也可以套用至伺服器層級的 MDX 查詢, 以強制終止所有長時間執行的查詢。

## <a name="resources"></a>資源

如果您不熟悉 OLAP 或 MDX 查詢, 請參閱這些維琪百科文章: 

+ [OLAP cube](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX 查詢](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
