---
title: Visual Database Tool 設計工具 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [SQL Server]
- View Designer
- Visual Database Tools [SQL Server]
- Database Diagram Designer
- Query Designer [SQL Server]
- design tools [Visual Database Tools]
- Table Designer
- Visual Database Tools [SQL Server], designers
- Properties window [Visual Database Tools]
ms.assetid: bd0ca68e-6f69-42dd-bcb5-ce511673769c
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ce2c27eb14fdafe41d30792f1464e190b92ffdf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="visual-database-tool-designers"></a>Visual Database Tool 設計工具
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Visual Database Tools 是設計組合工具，可用來使用資料來源。 您可以使用這些工具來建立查詢、設計或修改資料庫結構，或是更新資料。 這些工具包括資料庫圖表設計工具、資料表設計師以及查詢和檢視設計師。  
  
## <a name="properties-window"></a>屬性視窗  
[屬性] 視窗並非專屬於 Visual Database Tools，但可在其中進行許多修改動作。 其顯示目前所選取項目 (例如，資料表) 的屬性，並可讓您編輯這些屬性 (從屬性名稱到資料行定序的所有屬性)。 某些屬性可以在屬性視窗中查看，但必須以不同工具修改。  
  
## <a name="database-diagram-designer"></a>資料庫圖表設計工具  
資料庫圖表設計工具提供了讓您其中視覺化地建立、編輯和顯示資料庫中之資料表和關聯性的視窗。  
  
若要顯示資料庫圖表設計工具，請開啟現有的圖表或以滑鼠右鍵按一下物件總管中的 [資料庫] 節點，再從下拉式功能表中選擇 [新增資料庫圖表]。  
  
設計工具開啟後，[資料庫圖表] 功能表會出現在主功能表中。 此功能表可存取設計師的特殊功能。  
  
> [!NOTE]  
> 此設計師使用 Microsoft SQL Server 資料庫。  
>   
> 這個版本的 Visual Database Tools 不支援 Microsoft SQL Server 7 (含) 之前版本。  
  
## <a name="table-designer"></a>資料表設計工具  
資料表設計師是一種視覺化工具，可以讓您設計並以視覺化方式呈現所連接之 Microsoft SQL Server 資料庫中的單一資料表。  
  
資料表設計師有兩個窗格。 上方區域顯示方格；方格中的每個資料列各描述一個資料庫資料行。 方格將顯示每個資料庫資料行的基本屬性：資料行名稱、資料類型和允許 null 值的設定。  
  
[資料表設計師] 下方的 [資料行屬性] 索引標籤，顯示在上方區域反白顯示之資料行的其他屬性。  
  
從 [資料表設計師]，您也可以在方格區按一下滑鼠右鍵，存取可用以建立和修改資料表關聯性、條件約束、索引和索引鍵的對話方塊。  
  
若要顯示資料表設計工具，請開啟現有的資料表或以滑鼠右鍵按一下物件總管中的 [資料表] 節點，再從下拉式功能表中選擇 [新增資料表]。  
  
設計師一旦開啟，[資料表設計師] 功能表會出現在主功能表中。 此功能表可存取設計師的特殊功能。  
  
> [!NOTE]  
> 此設計師使用 Microsoft SQL Server 資料庫。  
>   
> 這個版本的 Visual Database Tools 不支援 Microsoft SQL Server 7 (含) 之前版本。  
  
## <a name="query-and-view-designer"></a>查詢和檢視表設計工具  
[查詢和檢視設計師] 實際上是兩個使用非常相似的方式運作的工具。 某些主要差異在於：  
  
-   檢視儲存於資料庫，而查詢和 Visual Studio 資料庫專案一起儲存。  
  
-   [查詢設計工具] 可使用任何的資料來源，而 [檢視設計工具] 只能使用 SQL Server。  
  
-   [查詢設計工具] 可讓您設計 SELECT、INSERT、UPDATE 和 DELETE DML 陳述式，而檢視只能包含 SELECT 陳述式。  
  
### <a name="view-designer"></a>檢視設計工具  
[檢視設計師] 可讓您設計和視覺化現有檢視，或是在所連接的 Microsoft SQL Server 資料庫中建立新的檢視。  
  
檢視設計師有四個窗格：圖表窗格、準則窗格、SQL 窗格和結果窗格。 如需這些每個窗格的詳細資訊，請參閱[查詢和檢視表設計工具 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)。  
  
若要顯示檢視表設計工具，請開啟現有的檢視或以滑鼠右鍵按一下物件總管中的 [檢視] 節點，再從下拉式功能表中選擇 [新增檢視]。  
  
設計工具開啟後，[查詢設計工具] 功能表會出現在主功能表中。 此功能表可存取設計師的特殊功能。  
  
> [!NOTE]  
> 此設計師使用 Microsoft SQL Server 資料庫。  
>   
> 這個版本的 Visual Database Tools 不支援 Microsoft SQL Server 7 (含) 之前版本。  
  
## <a name="see-also"></a>另請參閱  
[設計資料庫圖表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-database-diagrams-visual-database-tools.md)  
[設計資料表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
