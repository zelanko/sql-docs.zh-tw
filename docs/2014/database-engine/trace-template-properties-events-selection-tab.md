---
title: 追蹤範本屬性 （事件選取範圍索引標籤） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.pro.tracetemplateproperties.eventsselection.f1
helpviewer_keywords:
- Trace Template Properties dialog box
ms.assetid: 5b202457-ab42-4902-8012-7f3f40aa09f5
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 097772336c66b6b1832a6e0bb16791fc107ec81a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031107"
---
# <a name="trace-template-properties-events-selection-tab"></a>追蹤範本屬性 (事件選取範圍索引標籤)
  使用 **[追蹤範本屬性]** 對話方塊的 **[事件選取範圍]** 索引標籤，來檢視、編輯或指定要包含在 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 追蹤範本中的事件類別和資料行。  
  
## <a name="options"></a>選項。  
 [事件] 資料行  
 選取或清除事件資料行中的核取方塊，來指定應追蹤的事件。 依事件類別目錄所組織的事件。  
  
 如果選取 **[一般]** 索引標籤上的 **[以現有的範本作為新範本的基礎]** ，就會根據指定的範本自動選取事件。 如需有關事件類別的詳細資訊，請參閱＜ [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md)＞。  
  
 資料行  
 勾選對應到所需事件和資料行的方塊，來指定應追蹤的資料行。 依預設，如果已勾選對應到事件的核取方塊，追蹤所包含之每個事件的所有相關事件資料行也都會被勾選。 如果勾選 **[一般]** 索引標籤上的 **[以現有的範本作為新範本的基礎]** ，就會根據指定的範本自動選取資料行和篩選。  
  
 按一下資料行標頭並輸入篩選準則，即可指定篩選。 篩選的資料行在 **[編輯篩選]** 對話方塊中，會以資料行標籤左方的篩選圖示指出。  
  
 **顯示所有事件**  
 顯示所有可用的事件。 如果您正在建立一個不是以現有的範本為基礎的新範本，這個選項依預設為核取的。 取消選取以隱藏 **[事件選取範圍]** 方格中所有未選取的事件。  
  
 **顯示所有資料行**  
 顯示所有可用的資料行。 如果您正在建立一個不是以現有的範本為基礎的新範本，這個選項依預設為核取的。 取消選取以隱藏 **[事件選取範圍]** 方格中所有未選取的資料行。  
  
 **資料行篩選**  
 啟動 [編輯篩選] 對話方塊，它會在資料行標籤的左方顯示篩選圖示。 使用 **[編輯篩選]** 對話方塊，即可編輯資料行篩選。  
  
 **組織資料行**  
 變更追蹤中資料行的順序，並且依據一或多個資料行對結果進行分組。  
  
## <a name="see-also"></a>另請參閱  
 [指定追蹤檔案的事件及資料行&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [組織追蹤內顯示的資料行&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [篩選追蹤中的事件&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [檢視篩選資訊 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [修改篩選&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [SQL Server Profiler 範本和權限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  