---
title: 使用 Insight 小工具來監視 SQL Operations Studio （預覽）中的伺服器與資料庫 |Microsoft 文件
description: 了解 SQL Operations Studio（預覽）中的 Insight 小工具。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article"
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77f34ceebb4f02c829b2df3efcae5e64c2eaa1bf
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2018
ms.locfileid: "34235927"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 使用 insight 小工具管理資料庫與伺服器

Insight 小工具採用您所用的 Transact-SQL (T-SQL) 查詢，以監控伺服器與資料庫並將它們轉換為可深入解析的視覺圖表。 

Insights 是可以新增至伺服器與資料庫監控儀表板的客製圖表與圖形。 一目了然地檢視您的伺服器與資料庫，進而深入了解更多細節，並啟動您自定義的管理操作。 

您可以建立類似下列範例的絕佳伺服器和資料庫管理儀表板：

![資料庫儀表板](media/insight-widgets/database-dashboard.png)


若要著手開始建立不同類型的 Insight 小工具，請參閱下列教學課程：

- [建置自訂的 Insight 小工具](tutorial-build-custom-insight-sql-server.md)
- *啟用內建的 Insight 小工具*
   - [啟用效能監視 insight](tutorial-qds-sql-server.md)
   - [啟用資料表空間使用量深入資訊](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>SQL 查詢 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 若要避免引進其他語言或大量的使用者介面，因此它會嘗試使用 T-SQL 盡可能以最小的 JSON 組態尚未嘗試。 使用 T-SQL 設定深入了解 widget 會利用無數的有用可以轉換成具洞察力的 widget 的 T-SQL 查詢現有來源的數目。

Insight 小工具是由一個或兩個 T-SQL 查詢所組成：
* *Insight 小工具查詢*是必要的且查詢會傳回小工具中出現的資料。
* 若要建立 Insight 詳細資料頁面，才需要*Insight 詳細資料查詢*。

Insight 小工具查詢定義了轉譯計數、圖表或圖形的資料集。 在 Insight 詳細資料面板中，可以使用 Insight 詳細資料查詢以表格格式來列出相關的 Insight 詳細資訊。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]會執行 Insight 小工具查詢，並將查詢結果集對應至圖表的資料集，然後會將其轉譯。 當使用者開啟 Insight 的詳細資料時，它會執行 Insight 詳細資料查詢，並在對話方塊中以方格檢視來列印結果。

基本概念是在撰寫 T-SQL 查詢時，讓它可用來當做計數、圖表和圖形小工具的資料集。 

## <a name="summary"></a>摘要

T-SQL 查詢及其結果集決定了 Insight 小工具行為。 若要建置有效的 Insight 小工具，關鍵考量便是撰寫圖表類型的查詢，或是將正確的圖表類型對應至現有查詢。



## <a name="additional-resources"></a>其他資源
- [查詢編輯器](tutorial-sql-editor.md)

