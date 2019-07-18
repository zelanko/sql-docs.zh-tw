---
title: 自動聯結資料表 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- joins [SQL Server], creating
- joins [SQL Server], automatic
ms.assetid: f152af82-bcb6-49ca-af19-48cdb7fc9ac6
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 43bcfa304979b918d9588c8bdd8bd07f9296fa5f
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2019
ms.locfileid: "67682166"
---
# <a name="join-tables-automatically-visual-database-tools"></a>自動聯結資料表 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
當您將兩個或多個資料表新增至查詢時， [查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 會嘗試判斷它們是否相關。 如果相關聯，查詢和檢視設計師會自動在代表資料表或表格化物件的矩形之間加上聯結線 (Join Line)。  
  
在下列狀況下，查詢和檢視設計師會將資料表當做已聯結：  
  
-   資料庫包含指定資料表為相關聯的資訊。  
  
-   如果兩個資料行 (每個資料表各一個資料行) 的名稱和資料類型相同， 至少一個資料表中的資料行必須為主索引鍵。 例如，如果加入 `employee` 和 `jobs` 資料表，如果 `job_id` 資料行為 `jobs` 資料表的主索引鍵，如果每個資料表中稱為 `job_id` 的資料行有相同的資料類型，則查詢和檢視設計師將自動聯結資料表。  
  
    > [!NOTE]  
    > 查詢和檢視設計師將根據名稱和資料類型相同的資料行，來建立唯一的聯結。 如果可能有多個聯結，查詢和檢視設計師在根據它所找到的第一組符合的資料行來建立聯結之後就會停止。  
  
-   查詢和檢視設計師偵測到搜尋條件 (WHERE 子句) 實際上就是聯結條件 (Join Condition)。 例如，您可能加入資料表 `employee` 和 `jobs`，然後建立搜尋兩個資料表的 `job_id` 資料行中相同值的搜尋條件。 在進行此作業時，查詢和檢視設計師會偵測到搜尋條件將導致聯結，然後根據此搜尋條件來建立聯結條件。  
  
如果查詢和檢視設計師已建立不適用於您的查詢的聯結，就可以修改或移除聯結。 如需詳細資訊，請參閱[修改聯結運算子 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/modify-join-operators-visual-database-tools.md) 和[移除聯結 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-joins-visual-database-tools.md)。  
  
如果查詢和檢視設計師不會自動聯結查詢中的資料表，則可以自行建立聯結。 如需詳細資料，請參閱[手動聯結資料表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
[查詢和檢視表設計工具表示聯結的方式 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/how-the-query-and-view-designer-represents-joins-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
