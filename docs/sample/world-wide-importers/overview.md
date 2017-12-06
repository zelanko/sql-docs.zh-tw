---
title: "概觀 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology: samples
ms.custom: 
ms.date: 01/30/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d4dcb00-b93e-44db-9d67-061702bba41a
caps.latest.revision: "3"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 658c1b3ffd44cd2194c75d6ad45888e24e0772c1
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="wide-world-importers-overview"></a>寬 World Importers 概觀
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]這是虛構的公司 Wide World Importers 和 SQL Server 和 Azure SQL Database 的 WideWorldImporters 範例資料庫中所述的工作流程的概觀。  

Wide World Importers （生平） 是批發新式貨物匯入工具和 San Francisco 灣區從作業系統的散發者。

為批發商，大部分轉售給個人公司的生平的客戶。 生平銷售零售客戶在美國，包括特殊存放區，超級市場，電腦存放區、 觀光引力商店，以及某些個人。 若要透過網路代理程式升級的產品生平的代表人員的其他 wholesalers 也銷售生平。 雖然所有生平的客戶目前以在美國，公司想要推送擴充其他國家/地區。

生平供應商提供包括新式、 玩具製造商和其他新式 wholesalers 購買商品。 視需要以達到客戶訂單，它們內建在生平倉儲和重新排列從供應商的貨物。 也購買大量的封裝資料，而這些較小的數量的客戶銷售是方便。

最近生平開始銷售例如 chilli edible novelties 各種巧克力。  公司之前沒有處理 chilled 項目。 現在，為了要符合需求的食物，他們必須監視在其 chiller 聊天室和任何其擁有 chiller 區段的卡車溫度。

## <a name="workflow-for-warehouse-stock-items"></a>倉儲庫存項目工作流程

項目都入庫了，分散方式的一般流程如下所示：
- 生平會建立採購單，並送出至供應商的訂單。
- 供應商的項目傳送，生平收到其備有存貨它們在其倉儲中。
- 從生平客戶訂購項目
- 生平填客戶訂單，與在倉儲中，內建項目，並沒有足夠的存貨，當他們另外訂購了其他內建從供應商。
- 某些客戶不想等候庫存中所沒有的項目。 如果他們另外訂購了假設不同的五個內建的項目和四個可供使用，他們想要接收的四個項目和追加剩下的項目。 項目將它們傳送稍後在個別的出貨。
- 生平發票客戶針對內建的項目，通常會將訂單轉換為發票。
- 客戶可能訂購庫存中所沒有的項目。 這些項目是交貨。
- 生平送交客戶透過自己的傳遞 van，或透過其他 couriers 或運費方法的內建項目。
- 客戶付費生平發票。
- 定期生平付款供應商的訂單上的項目。 這是通常在一段時間後它們收到的貨品。

## <a name="data-warehouse-and-analysis-workflow"></a>資料倉儲和分析工作流程

雖然生平的小組會使用 SQL Server Reporting Services 從 WideWorldImporters 資料庫產生營運報表，它們也需要對其資料執行分析，並需要產生策略的報表。 小組 WideWorldImportersDW 資料庫中建立維度資料模型。 這個資料庫會填入 Integration Services 封裝。

SQL Server Analysis Services 用來建立分析資料模型，從維度資料模型中的資料。 SQL Server Reporting Services 用來產生策略的報表，直接從維度的資料模型，以及從分析模型。 Power BI 用來從相同的資料建立儀表板。 使用儀表板上的網站，並在手機和平板電腦上。 *注意： 這些資料模型和報表尚無法使用*

## <a name="additional-workflows"></a>其他工作流程

這些是額外的工作流程。
- 當客戶生平問題信用資訊不會接收好，基於某些原因，或者貨物故障。 這些會被視為負的發票。
- 生平定期計算內建的項目，以確保他們的系統上顯示為可用的內建數量都是正確的手上的數量。 （執行此動作的程序稱為 stocktake）。
- 冷聊天室溫度。 Perishable 貨物會儲存在 refrigerated 聊天室。 從這些聊天室的感應器資料會內嵌至資料庫以進行監視和分析用途。
- 一種載具，追蹤的位置。 傳輸的生平貨物的工具包括感應器追蹤的位置。 這個位置是一次內嵌到資料庫中進行監視及進一步分析。

## <a name="fiscal-year"></a>會計年度

公司的運作方式的財務的年份，從 11 月 1 日開始。

## <a name="terms-of-use"></a>使用規定

此處所述的範例資料庫和範例程式碼的授權： [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

範例資料庫包含已載入從 data.gov 和自然 EarthData 的公用資料。 在這裡可以使用規定： [http://www.naturalearthdata.com/about/terms-of-use/](http://www.naturalearthdata.com/about/terms-of-use/)
