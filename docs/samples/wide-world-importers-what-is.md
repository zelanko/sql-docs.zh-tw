---
title: Wide World 匯入工具-適用于 SQL 的範例資料庫 |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 872892d307883bb7df31b08de701b2030d9aeb1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68794603"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>適用于 Microsoft SQL 的 Wide World 匯入範例資料庫
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
這是針對 SQL Server 和 Azure SQL Database 在 WideWorldImporters 範例資料庫中解決的虛構全公司匯入工具和工作流程的總覽。  

Wide World 匯入工具（WWI）是一家批發的 novelty 商品匯入工具，以及從三藩市廳區域運作的散發者。

身為批發商，WWI 的客戶大多是轉銷個人的公司。 WWI 銷售給美國各地的零售客戶，包括專業商店、超市、運算店、旅遊遊樂設施店及某些個人。 WWI 也會透過代表 WWI 促銷產品的代理程式網路，銷售給其他 wholesalers。 雖然所有 WWI 的客戶目前都是以美國為基礎，但公司打算將擴充功能推送至其他國家/地區。

WWI 會從供應商購買貨物，包括 novelty 和玩具製造商，以及其他 novelty wholesalers。 他們會在其 WWI 倉儲中存貨貨物，並視需要向供應商重新排序，以履行客戶訂單。 他們也購買大量的封裝材料，並以較小的數量銷售，以方便客戶使用。

最近 WWI 開始銷售各種 edible novelties，例如 chilli 巧克力。  該公司先前不需要處理 chilled 專案。 現在，為了符合食物處理需求，他們必須監視 chiller 室的溫度，以及任何有 chiller 區段的卡車。

## <a name="workflow-for-warehouse-stock-items"></a>倉儲庫存專案的工作流程

如何儲存和散發專案的一般流程如下所示：
- WWI 會建立採購單，並將訂單提交給供應商。
- 供應商會傳送專案，WWI 會在其倉儲中接收並將它們股票。
- 從 WWI 訂購專案的客戶
- WWI 會以倉儲中的內建專案填滿客戶訂單，而當他們沒有足夠的存貨時，就會向供應商訂購額外的存貨。
- 有些客戶不想要等待非庫存中的專案。 如果它們訂購的是五個不同的股票專案，而且有四個可用的專案，他們會想要接收四個專案，並將剩餘的專案延期。 此專案稍後會在個別的出貨中傳送。
- WWI 存貨專案的發票客戶，通常是藉由將訂單轉換成發票。
- 客戶可能會訂購不在庫存中的專案。 這些專案都是缺貨的。
- WWI 會透過自己的遞送 van，或透過其他 couriers 或運費方法，將股票商品傳遞給客戶。
- 客戶需支付發票以進行 WWI。
- WWI 會定期向供應商支付訂單上的專案。 這通常是在收到貨物之後的一段時間。

## <a name="data-warehouse-and-analysis-workflow"></a>資料倉儲和分析工作流程

當 WWI 的小組使用 SQL Server Reporting Services 從 WideWorldImporters 資料庫產生作業報表時，他們也需要對其資料執行分析，而且需要產生策略性的報表。 小組已在資料庫 WideWorldImportersDW 中建立維度資料模型。 這個資料庫會由 Integration Services 封裝填入。

SQL Server Analysis Services 是用來從維度資料模型中的資料建立分析資料模型。 SQL Server Reporting Services 是用來直接從維度資料模型產生策略性報表，也會從分析模型。 Power BI 是用來從相同的資料建立儀表板。 儀表板會用於網站，以及手機和平板電腦上。 *注意：這些資料模型和報表尚無法使用*

## <a name="additional-workflows"></a>其他工作流程

這些是額外的工作流程。
- 當客戶因為某種原因或貨物發生錯誤而未收到良好的情況時，WWI 會發出點數注意事項。 這些會被視為負面發票。
- WWI 會定期計算存貨專案的數量，以確保在其系統上顯示為可用的存貨數量是正確的。 （執行這項作業的程式稱為 stocktake）。
- 冷室溫度。 壞商品會儲存在冷飲室。 這些房間的感應器資料會內嵌到資料庫中，以供監視和分析之用。
- 車輛位置追蹤。 WWI 傳輸貨物的車輛包括追蹤位置的感應器。 這個位置會再次內嵌到資料庫中，以進行監視及進一步分析。

## <a name="fiscal-year"></a>會計年度

公司營運的財務年度會在11月1日開始運作。

## <a name="terms-of-use"></a>使用規定

範例資料庫和範例程式碼的授權如下所述： [license .txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

範例資料庫包含已從 data.gov 和天然 EarthData 載入的公用資料。 使用條款如下：[https://www.naturalearthdata.com/about/terms-of-use/](https://www.naturalearthdata.com/about/terms-of-use/)
