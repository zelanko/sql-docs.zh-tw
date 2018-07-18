---
title: Wide World Importers-sql 範例資料庫 |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5a1eef0650c520ff4757de627633d096ffa46ec8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993477"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Wide World Importers Microsoft sql 範例資料庫
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
這是虛構的公司 Wide World Importers 和適用於 SQL Server 和 Azure SQL Database WideWorldImporters 範例資料庫中所述的工作流程的概觀。  

批發新奇貨物匯入工具和 「 散發者 」 營運的舊金山灣區從 wide World Importers (WWI)。

批發商，為 WWI 的客戶會有大部分轉售給個人的公司。 WWI 銷售給零售客戶包括特殊存放區，超級市場，美各地電腦存放區、 觀光引力商店，以及某些人。 WWI 也銷售給其他經銷商透過升級為 WWI 的代表產品的代理程式的網路。 WWI 的客戶的所有目前在美國為基礎，而公司打算推送擴充其他國家/地區。

WWI 供應商提供包括新奇和玩具製造商，以及其他新式經銷商購買商品。 它們內建在其 WWI 倉儲和重新排列從供應商貨物，視需要以履行客戶訂單。 它們也購買大量的封裝資料，並銷售較小的數量中的這些客戶為了方便起見。

最近 WWI 開始銷售 edible novelties chilli 等各種巧克力。  該公司之前沒有處理 chilled 的項目。 現在，為了符合處理需求的食物，他們必須監視其 chiller 聊天室和任何其有 chiller 區段的卡車溫度。

## <a name="workflow-for-warehouse-stock-items"></a>倉儲庫存項目的工作流程

項目配備和分散的方式的一般流程如下所示：
- WWI 建立訂單，並送出給供應商的訂單。
- 供應商的項目傳送，WWI 收到其備有存貨它們在其倉儲中。
- 從 WWI 客戶訂單項目
- WWI 填滿的客戶訂單的股票項目在倉儲中，並當它們並沒有足夠庫存，順序其他庫存供應商。
- 有些客戶不想等候庫存中的項目。 如果他們說訂購五個不同股票的項目，和四個可供使用，他們想要接收的四個項目和追加剩下的項目。 項目將它們傳送更新版本中不同的出貨。
- WWI 發票股票項目中，的客戶通常會藉由將訂單轉換為發票。
- 客戶可能訂購庫存中的項目。 這些項目會缺貨。
- WWI 客戶透過自己的傳遞 van，或透過其他 couriers 或 freight 方法提供內建的項目。
- 客戶付費 WWI 發票。
- 定期 WWI 會將供應商支付訂單上的項目。 這是通常在一段時間後他們已收到的貨品。

## <a name="data-warehouse-and-analysis-workflow"></a>資料倉儲和分析工作流程

雖然為 WWI 的小組會使用 SQL Server Reporting Services，從 WideWorldImporters 資料庫產生操作報表，他們也必須對其資料執行分析，並需要產生策略的報表。 小組 WideWorldImportersDW 的資料庫中建立維度的資料模型。 此資料庫會填入 Integration Services 封裝。

SQL Server Analysis Services 用來建立分析資料模型，從維度資料模型中的資料。 SQL Server Reporting Services 用來產生策略的報告，直接從維度的資料模型，以及從分析的模型。 Power BI 用來從相同的資料建立儀表板。 使用於儀表板網站，或在手機和平板電腦上。 *注意： 這些資料模型和報表尚無法使用*

## <a name="additional-workflows"></a>額外的工作流程

這些是額外的工作流程。
- WWI 問題折讓客戶不會接收良好，基於某些原因，或貨品已故障。 這些會被視為負數的發票。
- WWI 定期計算內建的項目，以確保其系統上顯示為可用的庫存數量是正確的庫存的數量。 （執行此動作的程序稱為 stocktake）。
- 冷聊天室溫度。 Perishable 商品會儲存在 refrigerated 聊天室。 這些聊天室的感應器資料擷取至資料庫中的監視與分析之用。
- 車輛位置追蹤。 WWI 的運輸貨物的工具包括追蹤位置的感應器。 這個位置一次擷取至資料庫中的監視及進一步分析。

## <a name="fiscal-year"></a>會計年度

公司營運與財務的年份，從 11 月 1 日開始。

## <a name="terms-of-use"></a>使用規定

此處所述的範例資料庫和範例程式碼的授權： [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

範例資料庫包含已從 data.gov 和自然 EarthData 載入的公用資料。 使用規定如下： [http://www.naturalearthdata.com/about/terms-of-use/](http://www.naturalearthdata.com/about/terms-of-use/)
