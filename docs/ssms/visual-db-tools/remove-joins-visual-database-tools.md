---
title: 移除聯結 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- removing joins
- joins [SQL Server], removing
- deleting joins
ms.assetid: ccc212a1-fd13-48d6-85e5-5ff310c34bbd
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6e1de076e5882be92a1ed3b9f2d16eac7c5e062f
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65098205"
---
# <a name="remove-joins-visual-database-tools"></a>移除聯結 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果不要使用內部聯結或外部聯結來聯結資料表，則可以移除其間的聯結。 例如，您可以移除 [查詢和檢視設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 自動在兩個資料表間建立的聯結。  
  
> [!NOTE]  
> 移除查詢中的聯結，並不會改變資料庫的基礎關聯性。  
  
如果兩個聯結的資料表是查詢的一部份，並且移除其間的所有聯結條件，則產生的查詢會成為兩個資料表相乘，亦即成為 CROSS JOIN。  
  
### <a name="to-remove-a-join"></a>若要移除聯結  
  
-   在 [圖表窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)中，選取要移除之聯結的聯結線，然後按 DELETE 鍵。 可以一次選取和刪除多重聯結線。  
  
查詢和檢視設計工具會移除聯結線，並隨即變更 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中的陳述式。  
  
## <a name="see-also"></a>另請參閱  
[自動聯結資料表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)  
[手動聯結資料表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)  
[使用聯結查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
