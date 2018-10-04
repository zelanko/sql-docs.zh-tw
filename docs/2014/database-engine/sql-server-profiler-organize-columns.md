---
title: SQL Server Profiler-組織資料行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.organize.columns.f1
ms.assetid: bf5674f4-da5e-43f9-aeb2-76ca37993790
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7cf6f979058fd1003440e17fb5c479e136413bcf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217998"
---
# <a name="sql-server-profiler---organize-columns"></a>SQL Server Profiler - 組織資料行
  使用 **[組織資料行]** 對話方塊來選取在追蹤中所顯示的群組或彙總事件的資料行，讓您易於檢視和分析大型追蹤檔案或資料表。  
  
 彙總會移動和摺疊在追蹤中的各事件類別類型之下的所有事件。 加號 (**+**) 會出現在事件類別名稱的左邊。 按一下加號會展開事件類別，使您可以檢視該類型的所有事件。  
  
 群組會將特定類型的所有事件類別，組織在一起並顯示在追蹤視窗中。 不過，事件並不會摺疊在事件類別類型之下。  
  
 當您群組或彙總追蹤視窗顯示中的事件時，針對要進行群組或彙總所選取的資料行會固定地顯示在視窗中，但是您可以向左或向右捲動，以檢視所有其他資料行。  
  
 若要存取此對話方塊，請開啟現有的追蹤檔案或資料表，然後按一下 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] [檔案] 功能表上的 [屬性]。 在 **[追蹤屬性]** 對話方塊中，按一下 **[事件選取範圍]** 索引標籤，然後按一下 **[組織資料行]**。 在建立新的追蹤時，您也可以按一下 **[事件選取範圍]** 索引標籤上的 **[組織資料行]** 。  
  
## <a name="options"></a>選項。  
 **群組**  
 將 [群組] 之下的資料行名稱移至追蹤視窗中的群組或彙總事件類別。  
  
 若要彙總事件，請將一個資料行移至 **[群組]**。 這會使特定類型的所有事件，都摺疊在追蹤視窗顯示中的事件類別類型名稱之下。 加號 (**+**) 會出現在事件類別名稱的左邊。 按一下加號即可展開事件類別類型並檢視所有事件。 按一下 **[檢視]** 功能表上的 **[彙總檢視]** 或 **[群組檢視]** ，您可以設定開啟或關閉彙總和群組。  
  
 若要群組事件，請將多個資料行移至 **[群組]**。 這會使特定類型的所有事件群組在追蹤視窗顯示中，但是不會將事件摺疊在每個事件類別類型名稱之下。 按一下 [檢視] 功能表上的 **[群組檢視]** ，您可以在群組檢視和非群組檢視之間來回切換。 當多個資料行移至 **[群組]** 時，不能使用切換至 **[彙總檢視]** 的選項。  
  
 **資料行**  
 可移至 [群組] 的資料行清單。 按一下 [資料行] 左邊的加號 (**+**) 即可展開清單。  
  
 **向上**  
 選取資料行之後，按一下 [向上] 將資料行向上移至 [群組]。 您也可以按一下 **[向上]** ，來重新排列追蹤視窗所顯示的資料行。  
  
 **向下**  
 選取資料行之後，按一下 [向下] 將資料行從 [群組] 中移出。 您也可以按一下 **[向下]** ，來重新排列追蹤視窗所顯示的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [組織追蹤內顯示的資料行&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [建立追蹤&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [建立追蹤範本&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
  
