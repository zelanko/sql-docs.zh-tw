---
title: "使用 Insight 小工具來監視 SQL Operations Studio（預覽）中的伺服器與資料庫 |Microsoft 文件"
description: "了解 SQL Operations Studio（預覽）中的 Insight 小工具。"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d810e0b5ed89b93ac3d56a12758285fbd297092b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 中管理伺服器和資料庫的 Insight 小工具

Insight 小工具會根據您監視伺服器和資料庫所用的 TRANSACT-SQL (T-SQL) 查詢，將之轉換成可提供深入解析資訊的視覺效果。 

Insights 是可自訂圖表和圖形加入至伺服器和資料庫監視儀表板。 檢視在摘要深入資訊，您的伺服器和資料庫，然後向下鑽研到詳細資訊，並啟動您所定義的管理動作。 

您可以建立類似下列範例的絕佳伺服器和資料庫管理儀表板：

![資料庫儀表板](media/insight-widgets/database-dashboard.png)


若要著手開始建立不同類型的 Insight 小工具，請參閱下列教學課程：

- [建置自訂的 Insight 小工具](tutorial-build-custom-insight-sql-server.md)
- *啟用內建的 Insight 小工具*
   - [啟用效能監視 insight](tutorial-qds-sql-server.md)
   - [啟用資料表空間使用量深入資訊](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>SQL 查詢 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]若要避免引進其他語言或大量的使用者介面，因此它會嘗試使用 T-SQL 盡可能以最小的 JSON 組態尚未嘗試。 使用 T-SQL 深入解析小工具會利用無數的有用可以轉換成具洞察力的小工具的 T-SQL 查詢現有來源的數目。

Insight 小工具是由一個或兩個 T-SQL 查詢所組成：
* *Insight 小工具查詢*是必要的且查詢會傳回小工具中出現的資料。
* 若要建立 Insight 詳細資料頁面，才需要 *Insight 詳細資料查詢*。

Insight 小工具查詢定義了轉譯計數、圖表或圖形的資料集。在 Insight 詳細資料面板中，可以使用 Insight 詳細資料查詢以表格格式來列出相關的 Insight 詳細資訊。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 會執行 Insight 小工具查詢，並將查詢結果集對應至圖表的資料集，然後會將其轉譯。當使用者開啟 Insight 的詳細資料時，它會執行 Insight 詳細資料查詢，並在對話方塊中以方格檢視來列印結果。

基本概念是在撰寫 T-SQL 查詢時，讓它可用來當做計數、圖表和圖形小工具的資料集。 

## <a name="summary"></a>摘要

T-SQL 查詢及其結果集決定了 Insight 小工具行為。若要建置有效的 Insight 小工具，關鍵考量便是撰寫圖表類型的查詢，或是將正確的圖表類型對應至現有查詢。



## <a name="additional-resources"></a>其他資源
- [查詢編輯器](tutorial-sql-editor.md)

