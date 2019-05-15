---
title: SQL 窗格 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], SQL pane
- View Designer, SQL pane
- SQL pane [Visual Database Tools]
ms.assetid: dbabab18-0614-415b-a2ef-9bcd0d320d5c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 89c1d77d7c231b96381d8a2f9f9edb70f02b08a5
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105623"
---
# <a name="sql-pane-visual-database-tools"></a>SQL 窗格 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以使用 [SQL] 窗格建立您自己的 SQL 陳述式，也可以使用 [準則] 窗格和 [圖表] 窗格建立陳述式。在這個情況中，SQL 陳述式會在 [SQL] 窗格中建立。 當您建置查詢時，[SQL 窗格] 會自動進行簡單的可讀性更新及重新格式化。  
  
若要開啟 [SQL 窗格]，請先開啟查詢和檢視設計工具 (按一下 [資料庫] 功能表中的 [新增查詢]，以在伺服器總管中選取資料庫物件)。 接著在 [查詢設計工具] 功能表中指向 [窗格]按一下 [SQL]。  
  
您可以在 [SQL 窗格] 中：  
  
-   輸入 SQL 陳述式以建立新的查詢。  
  
-   根據您在 [圖表窗格] 和 [準則窗格] 所做的設定，修改由查詢和檢視設計工具所建立的 SQL 陳述式。  
  
-   輸入使用資料庫 (您目前所使用的資料庫) 特定功能的陳述式。  
  
> [!NOTE]  
> 請確定您完全暸解所使用資料庫的資料庫物件識別規則。 如需詳細資料，請參閱資料庫管理系統中的文件集。  
  
## <a name="statements-in-the-sql-pane"></a>SQL 窗格中的陳述式  
您可以直接在 [SQL 窗格] 中編輯目前查詢。 當移至其他窗格時，查詢和檢視設計工具將自動格式化陳述式，然後變更 [圖表窗格] 和 [準則窗格] 以符合陳述式。  
  
如果陳述式無法在 [圖表窗格] 和 [準則窗格] 中顯示，而這些窗格是可見的，查詢和檢視設計工具將顯示錯誤訊息，然後提供兩個選項：  
  
-   忽略陳述式無法在 [圖表窗格] 及 [準則窗格] 中表示。  
  
-   恢復無法顯示的變更，並還原成最新版本的 SQL 陳述式。  
  
如果您選擇忽略陳述是無法在 [圖表窗格] 及 [準則窗格] 中表示，則查詢和檢視設計工具會將其他窗格變為暗灰色，表示這些窗格不再反映 [SQL 窗格] 的內容。  
  
和其他 SQL 陳述式一樣，您可以繼續編輯和執行該陳述式。  
  
> [!NOTE]  
> 如果您輸入 SQL 陳述式，然後又變更 [圖表窗格] 和 [準則窗格] 來進一步變更查詢，查詢和檢視設計工具將重新建立並重新顯示 SQL 陳述式。 有時候，這個動作產生的 SQL 陳述式會不同於您原本輸入的陳述式 (雖然其結果相同)。 當您使用的搜尋條件牽涉到與 AND 和 OR 連結的幾個子句時，其不同之處最為明顯。  
  
## <a name="see-also"></a>另請參閱  
[建立查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[執行查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[圖表窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[準則窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[結果窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
  
