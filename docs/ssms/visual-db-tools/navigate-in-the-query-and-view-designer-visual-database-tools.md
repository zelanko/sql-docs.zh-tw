---
title: "在查詢和檢視表設計工具中巡覽 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- View Designer, navigating
- shortcuts [SQL Server]
- Query Designer [SQL Server], navigating
- keyboard shortcuts [Visual Database Tools]
ms.assetid: 1c65acef-6dfa-463a-bf37-5a5335fe3865
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 134e017c94bbf364d74c3914149a09be3deaa9a3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="navigate-in-the-query-and-view-designer-visual-database-tools"></a>在查詢和檢視表設計工具中巡覽 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 在查詢和檢視表設計工具中，您可以使用鍵盤或滑鼠來工作。 各種特定的方法請參考以下各表。  
  
## <a name="any-pane"></a>任何窗格  
  
|**若要**|**按鍵**|**按一下**|  
|----------|-------------|-------------|  
|在 [查詢和檢視設計師] 各窗格間移動|F6、SHIFT+F6|目標窗格中的任何位置|  
  
> [!TIP]  
> 您可以使用快速鍵 CTRL+TAB，將焦點變更至 [查詢和檢視設計師] 窗格以外的窗格。  
  
## <a name="diagram-pane"></a>圖表窗格  
  
|**若要**|**按鍵**|**按一下**|  
|----------|-------------|-------------|  
|在各資料表、其他表格化物件 (Table-Structured Object) 和聯結線 (如果有的話) 之間移動|TAB 或 SHIFT+TAB|要移至的資料表、表格化物件或聯結線|  
|在資料表或表格化物件的資料行之間移動|方向鍵|要移至的資料行|  
|選擇選取的資料行以供輸出|空白鍵或加號鍵|資料行名稱旁邊的核取方塊|  
|從查詢輸出中移除選取的資料行|空白鍵或減號鍵|資料行名稱旁邊的核取方塊|  
|從查詢中移除選取的資料表、表格化物件或聯結線|DELETE|按一下滑鼠右鍵，再選擇 [移除]。|  
  
> [!NOTE]  
> 如果選取多個項目，按下此按鍵會影響所有選取的項目。 按住 CTRL 鍵，同時在要選取的各項目上按一下滑鼠，即可選取多個項目。  
  
如需詳細資訊，請參閱[圖表窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)。  
  
## <a name="criteria-pane"></a>準則窗格  
  
|若要|按鍵|按一下|  
|------|---------|---------|  
|在資料格間移動|方向鍵、TAB 或 SHIFT+TAB|目標資料格|  
|移至所選取資料行的最後一列|CTRL+向下鍵||  
|移至所選取資料行的第一個資料列|CTRL+向上鍵||  
|移至方格可見部分中的左上資料格|CTRL+HOME||  
|移至右下資料格|CTRL+END||  
|在下拉式清單中移動|向上鍵或向下鍵|資料格裡的按鈕|  
|選取整個方格資料行|CTRL+ 空白鍵|資料行標題|  
|切換編輯模式或資料格選擇模式|F2||  
|將資料格中選取的文字複製到剪貼簿 (編輯模式)|CTRL+C||  
|剪下資料格中選取的文字，放到剪貼簿中 (編輯模式)|CTRL+X||  
|貼上剪貼簿中的文字 (編輯模式)|CTRL+V||  
|編輯資料格時切換插入模式或覆寫模式|INS||  
|切換輸出資料行中的核取方槐|空白鍵|核取方塊|  
|清除資料格的選取內容|DELETE||  
|清除選取方格資料行的所有值|DELETE||  
|在現有資料列間插入資料列|選取方格資料列後按 INS||  
|新增 [或...] 資料行|選取任一個 [或...] 資料行後按 INS||  
  
> [!NOTE]  
> 如果選取多個項目，按下此按鍵會影響所有選取的項目。  
  
如需詳細資訊，請參閱[準則窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)。  
  
## <a name="sql-pane"></a>SQL 窗格  
在 SQL 窗格中工作時，可使用標準的 Windows 編輯鍵 (例如 CTRL + 方向鍵) 在文字間移動，以及 [編輯] 功能表上的 [剪下]、[複製] 和 [貼上] 命令。  
  
> [!NOTE]  
> 您只能插入文字；沒有覆寫模式。  
  
如需詳細資訊，請參閱 [SQL 窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)。  
  
## <a name="results-pane"></a>結果窗格  
  
|**若要**|**按鍵**|**按一下**|  
|----------|-------------|-------------|  
|在資料格間移動|方向鍵、TAB 或 SHIFT+TAB|目標資料格|  
|移至目前資料列的第一或最後一個資料格|HOME 或 END||  
|移至目前資料行的第一個資料列|CTRL+向上鍵||  
|移至左上資料格|CTRL+HOME||  
|移至第一個資料行裡最底下的資料格|CTRL+向下鍵||  
|選取至資料格裡的第一個字元|SHIFT+HOME||  
|選取至資料格裡的最後一個字元|SHIFT+END||  
|切換編輯模式或資料格選擇模式|F2||  
|編輯資料格時切換插入模式或覆寫模式|INS||  
|從資料表中刪除一個資料列|DELETE||  
|恢復目前資料格中的變更|在有變更內容的資料格中按 ESC||  
|恢復目前資料列中的變更|在尚未變更的任一個資料格中按 ESC||  
|在資料格中輸入 Null|CTRL+0||  
|將選取的資料行或資料列複製到剪貼簿|CTRL+C||  
|將資料格中選取的文字複製到剪貼簿 (編輯模式)|CTRL+C||  
|將資料格中選取的文字剪下到剪貼簿 (編輯模式)|CTRL+X||  
|貼上剪貼簿中的文字 (編輯模式)|CTRL+V||  
  
> [!NOTE]  
> 如果選取多個項目，按下此按鍵會影響所有選取的項目。  
  
如需詳細資訊，請參閱[結果窗格 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
