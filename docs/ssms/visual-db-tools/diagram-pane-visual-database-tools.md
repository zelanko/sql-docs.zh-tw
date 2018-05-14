---
title: 圖表窗格 (Visual Database Tools) | Microsoft Docs
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
- Query Designer [SQL Server], Diagram pane
- View Designer, Diagram pane
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 399dfc7b-e2e7-47d3-bd11-163cbe0ce13c
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a749cafa34c8db9d7cf2bc81c97e90da39e1bed3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="diagram-pane-visual-database-tools"></a>圖表窗格 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[圖表] 窗格會以圖形顯示您從資料連接所選取的資料表或資料表值物件。 同時還會顯示資料表或物件之間的任何聯結關聯性。  
  
您可以在 [圖表] 窗格中：  
  
-   加入或移除資料表及資料表值物件，並指定要輸出的資料行。  
  
-   建立或修改資料表和資料表值物件之間的聯結。  
  
當您在 [圖表] 窗格中進行變更時，[準則] 窗格和 [SQL] 窗格將自動更新以反映您所做的變更。 例如，如果您在 [圖表] 窗格的資料表或資料表值物件中選取某資料行進行輸出，[查詢和檢視設計師] 會將資料行加入 [準則] 窗格和 [SQL] 窗格中的 SQL 陳述式。  
  
[圖表] 窗格中的每一個資料表或資料值物件，都以個別視窗顯示。 每個矩形的標題列圖示都將表示該矩形代表的物件類型，如下表所示。  
  
## <a name="options"></a>選項。  
**資料表**  
列出可以加入 [圖表] 窗格的資料表。 若要新增資料表，請選取資料表，再按 [新增]。 若要一次新增數個資料表，請選取資料表，再按 [新增]。  
  
**檢視**  
列出可以加入 [圖表] 窗格的檢視。 若要新增檢視表，請選取檢視表，再按 [新增]。 若要一次新增數個檢視表，請選取檢視表，再按 [新增]。  
  
**函數**  
列出可加入 [圖表] 窗格的使用者定義函數。 若要新增函數，請選取函數，再按 [新增]。 若要一次新增數個函數，請選取函數，再按 [新增]。  
  
**區域資料表**  
列出由查詢所建立的資料表，而非屬於資料庫的資料表  
  
**同義字**  
列出可加入 [圖表] 窗格的同義資料表。 若要新增同義資料表，請選取同義資料表，再按 [新增]。 若要一次新增數個同義資料表，請選取同義資料表，再按一下 [新增]。  
  
|圖示|物件類型|  
|--------|---------------|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbi1.gif "Visual Database Tools 圖示")|Table|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbi2.gif "Visual Database Tools 圖示")|查詢或檢視|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbi3.gif "Visual Database Tools 圖示")|連結的資料表|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dvudficon.gif "Visual Database Tools 圖示")|使用者定義函數|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbi5.gif "Visual Database Tools 圖示")|連結的檢視|  
  
每一個矩形都會顯示資料表或資料表值物件的資料行。 資料行名稱旁邊的核取方塊和符號將說明資料行在查詢中的使用方式。 工具提示將說明資料類型和資料行大小等資訊。  
  
下表列出每一個資料表或資料表值物件矩形所使用的核取方塊和符號。  
  
|核取方塊或符號|描述|  
|-----------------------|---------------|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbi7.gif "Visual Database Tools 圖示")<br /><br />![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbi8.gif "Visual Database Tools 圖示")<br /><br />![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbi9.gif "Visual Database Tools 圖示")<br /><br />![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbia.gif "Visual Database Tools 圖示")|指定查詢結果集 (選取查詢) 中是否使用資料欄，或者是否在 UPDATE、INSERT FROM、製成資料表 (Make Table) 或 INSERT INTO 查詢中使用資料欄。 選取要新增到結果的資料行。 如果選取 [(所有資料行)]，所有資料行都將出現在輸出中。<br /><br />核取方塊所使用的圖示將根據您建立的查詢類型而有所改變。 建立刪除查詢時，您無法選取個別的資料行。|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbib.gif "Visual Database Tools 圖示")<br /><br />![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbic.gif "Visual Database Tools 圖示")|指示用來排列查詢結果 (ORDER BY 子句的一部分) 的資料欄。 如果排列順序為遞增，則圖示將以 A-Z 的方法呈現，如果為遞減排序，則為 Z-A。|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbid.gif "Visual Database Tools 圖示")|指示在彙總查詢中用來建立群組結果集 (GROUP BY 子句的一部分) 的資料欄。|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbie.gif "Visual Database Tools 圖示")|指示查詢 (WHERE 或 HAVING 子句的一部分) 的搜尋條件包含該資料欄。|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbif.gif "Visual Database Tools 圖示")|指示摘要輸出該資料欄內容 (包含在 SUM、AVG 或其他彙總函式)。|  
  
> [!NOTE]  
> 如果您沒有足夠的存取權限，或如果資料庫驅動程式無法傳回相關資訊，[查詢和檢視設計師] 將不會顯示資料表或資料表值物件的資料行。 在這種情況下，查詢和檢視設計師僅將顯示資料表或表格化物件的標題列。  
  
## <a name="joined-tables-on-the-diagram-pane"></a>圖表窗格中的聯結資料表  
如果查詢中使用聯結，與聯結相關的資料欄之間將出現聯結線 (Join Line)。 如果聯結的資料行未顯示 (例如，資料表或資料表值物件視窗最小化，或該聯結使用運算式)，[查詢和檢視設計師] 將在該矩形標題列上放置聯結線以表示資料表或資料表值物件。 查詢和檢視設計師可顯示每個聯結狀況的聯結線。  
  
聯結線中間的圖示形狀即表示資料表或表格化物件的聯結方式。 如果聯結子句使用等號 (=) 以外的運算子，聯結線圖示將顯示使用的運算子。 下表即說明聯結線使用的圖示。  
  
|聯結線圖示|描述|  
|------------------|---------------|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbih.gif "Visual Database Tools 圖示")|內部聯結 (使用等號建立)。|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbii.gif "Visual Database Tools 圖示")|使用「大於」運算子的內部聯結。 (聯結線圖式顯示的運算子即為聯結使用的運算子)|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbij.gif "Visual Database Tools 圖示")|外部聯結，將包括左邊資料表的所有資料列，即使該資料表在相關資料表並沒有相符項目。|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbik.gif "Visual Database Tools 圖示")|外部聯結，將包括右邊資料表的所有資料列，即使該資料表在相關資料表中並沒有相符項目。|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbil.gif "Visual Database Tools 圖示")|完整的外部聯結，將同時包括兩邊的資料表，即使該資料表在相關資料表中並沒有相符項目。|  
  
聯結線結束部分的圖示表示聯結的類型。 下表將列出聯結類型和聯結線結束部分顯示的圖示。  
  
|聯結線結束部分所顯示的圖示|描述|  
|-----------------------------|---------------|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbim.gif "Visual Database Tools 圖示")|一對一聯結|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbin.gif "Visual Database Tools 圖示")|一對多聯結|  
|![Visual Database Tools 圖示](../../ssms/visual-db-tools/media/dv3wbio.gif "Visual Database Tools 圖示")|查詢和檢視設計師無法決定聯結類型|  
  
## <a name="see-also"></a>另請參閱  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[準則窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
