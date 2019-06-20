---
title: 指定追蹤檔案的事件及資料行 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- adding events
- traces [SQL Server], data columns
- deleting events
- removing events
- traces [SQL Server], events
ms.assetid: 7da715a3-2f03-4063-b6a4-20fd7b44e675
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33e11dde29a9f2b016f5f70fa3c12bd728928f93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267423"
---
# <a name="specify-events-and-data-columns-for-a-trace-file-sql-server-profiler"></a>指定追蹤檔案的事件及資料行 (SQL Server Profiler)
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]來指定追蹤的事件類別及資料行。  
  
### <a name="to-specify-events-and-data-columns-for-a-trace"></a>若要指定追蹤的事件及資料行  
  
1.  在 [追蹤屬性]  或 [追蹤範本屬性]  對話方塊上，按一下 [事件選取範圍]  索引標籤。  
  
     **[事件選取範圍]** 索引標籤包含方格控制項。 方格控制項是包含每一個可追蹤事件類別的資料表。 資料表針對每個事件類別包含一個資料列。 依據您所連接之伺服器的類型及版本，事件類別會有些許不同。 事件類別在方格的 [事件]  資料行中識別，並依事件類別目錄分組。 其餘資料行會列出可針對每個事件類別傳回的資料行。  
  
2.  在 [事件選取範圍]  索引標籤上，使用方格控制項在追蹤檔案中新增或移除事件及資料行。  
  
3.  若要將事件從追蹤中移除，請清除每個事件類別之 [事件]  資料行中的核取方塊。  
  
4.  若要在追蹤中加入事件，請核取每個事件類別之 [事件]  資料行中的方塊，或是核取對應至事件的資料行。  
  
> [!IMPORTANT]  
>  如果追蹤將會與「系統監視器」或「效能監視器」的資料產生關聯，則 [開始時間]  及 [結束時間]  資料行都必須納入追蹤中。  
  
 當您納入事件類別時，若有核取事件所對應的方塊，則每個相關聯的資料行也都會納入追蹤中。 若您核取了特定資料行的方塊，就只會將該資料行加入追蹤中。  
  
1.  若要從事件類別中移除資料行，請清除事件類別資料列中資料行的核取方塊，或是以滑鼠右鍵按一下資料行標頭，然後選取 [取消選取資料行]  選項。  
  
2.  您可以選擇將篩選套用至追蹤。 如需詳細資訊，請參閱[篩選追蹤中的事件 &#40;SQL Server Profiler&#41;](filter-events-in-a-trace-sql-server-profiler.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
