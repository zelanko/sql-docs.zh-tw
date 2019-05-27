---
title: 追蹤檔案屬性 （事件選取範圍 索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracefileproperties.eventsselection.f1
helpviewer_keywords:
- Trace File Properties dialog box
ms.assetid: 158d442f-2225-4173-8545-fb1cf611b4d0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0a6c6da76bd89b4686791087e558ae1f329f57a3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088794"
---
# <a name="trace-file-properties-events-selection-tab"></a>追蹤檔案屬性 (事件選取範圍索引標籤)
  使用 **[追蹤檔案範本屬性]** 對話方塊的 **[事件選取範圍]** 索引標籤，以檢視追蹤的資料行屬性，或者從追蹤移除資料行。  
  
 若要檢視此視窗，請開啟追蹤檔案。 接著在 **[檔案]** 功能表上，按一下 **[屬性]**，然後按一下 **[事件選取範圍]** 索引標籤。  
  
## <a name="options"></a>選項。  
 [事件] 資料行  
 檢視依事件類別目錄所組織的追蹤事件。 起初會選取追蹤內的所有事件。 勾選方塊或勾選事件的資料行即可選取事件。 如果勾選事件方塊，就會選取所有適用於該事件的資料行。 如果勾選事件的資料行，就會勾選事件，也會自動勾選任何其他必要的資料行。 如果您正在檢視追蹤檔案或資料表，清除事件或資料行的核取方塊會減少追蹤視窗中的可見資料量，以便進行分析。 您也可以變更資料行篩選，來減少追蹤視窗中的可見資料量。 如需有關事件類別的詳細資訊，請參閱＜ [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md)＞。  
  
 資料行  
 檢視追蹤的資料行。 依預設，針對追蹤內所包含的每個事件，都會勾選追蹤內的所有相關資料行。  
  
 按一下資料行標頭並輸入篩選準則，即可指定篩選。 篩選的資料行在 **[編輯篩選]** 對話方塊中，會以資料行標籤左方的篩選圖示指出。  
  
 **顯示所有事件**  
 顯示所有可用的事件。 依預設，僅會顯示在 **[事件選取範圍]** 方格中選取的資料列。 取消選取此方塊，即可隱藏 **[事件選取範圍]** 方格中所有未選取的事件。 如果勾選 **[顯示所有事件]** 而且您正在檢視追蹤檔案或資料表，在追蹤內記錄的所有事件就會顯示在追蹤視窗中。  
  
 **顯示所有資料行**  
 顯示所有可用的資料行。 依預設，僅會顯示選取的資料行。 取消選取此方塊，即可隱藏 **[事件選取範圍]** 方格中所有未選取的資料行。  
  
 **資料行篩選**  
 啟動 [編輯篩選] 對話方塊，會在資料行標籤左方顯示篩選圖示，以便篩選資料行。 使用 **[編輯篩選]** 對話方塊，即可編輯資料行篩選。  
  
 **組織資料行**  
 選取要追蹤的 [事件] 和資料行之後，按一下 [組織資料行] 即可強制方格重新排序追蹤結果視窗中的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [指定追蹤檔案的事件及資料行 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [篩選追蹤中的事件&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [檢視篩選資訊 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [修改篩選&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [[SQL Server Profiler]](../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Profiler 範本和權限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
  
  
