---
title: 追蹤屬性 （事件選取範圍 索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.traceproperties.eventsselection.f1
helpviewer_keywords:
- Trace Properties dialog box
ms.assetid: e1892f24-7272-4d5d-8926-6150cc82b2c3
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 64896beeb2e815f22662cd7d16aaf263135f8122
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089583"
---
# <a name="trace-properties-events-selection-tab"></a>追蹤屬性 (事件選取範圍索引標籤)
  使用 **[追蹤屬性]** 對話方塊的 **[事件選取範圍]** 索引標籤，來檢視或指定追蹤的事件和資料行。  
  
## <a name="options"></a>選項。  
 [事件] 資料行  
 選取或清除事件資料行中的核取方塊，來指定追蹤的事件。 依事件類別目錄所組織的**事件** 。 範本中所指定的事件類別會自動選取。 如需詳細資訊，請參閱 [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
 資料行  
 核取對應到所需事件和資料行的方塊，來指定追蹤的資料行。 依預設，針對追蹤內所包含的每個事件，都會核取所有相關的事件資料行。  
  
 按一下資料行標頭並輸入篩選準則，即可指定篩選。 篩選的資料行在 **[編輯篩選]** 對話方塊中，會以資料行標籤左方的篩選圖示指出。 如需詳細資訊，請參閱 [SQL Server Profiler - 編輯篩選](../../2014/database-engine/sql-server-profiler-edit-filter.md)。  
  
 **顯示所有事件**  
 顯示所有可用的事件。 依預設，僅會顯示在 **[事件選取範圍]** 方格中選取的資料列。 取消選取此方塊，即可隱藏 **[事件選取範圍]** 方格中所有未選取的事件。  
  
 **顯示所有資料行**  
 顯示所有可用的資料行。 依預設，僅會顯示選取的資料行。 取消選取此方塊，即可隱藏 **[事件選取範圍]** 方格中所有未選取的資料行。  
  
 **資料行篩選**  
 啟動 [編輯篩選] 對話方塊。 您可以使用此對話來編輯資料行篩選。  
  
 **組織資料行**  
 變更追蹤中資料行的順序，並且依據一或多個資料行對結果進行分組。  
  
## <a name="see-also"></a>另請參閱  
 [指定追蹤檔案的事件及資料行 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [組織追蹤內顯示的資料行&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [篩選追蹤中的事件&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [檢視篩選資訊 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [修改篩選&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [SQL Server Profiler 範本和權限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
