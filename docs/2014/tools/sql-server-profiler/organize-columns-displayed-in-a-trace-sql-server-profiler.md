---
title: 組織追蹤內顯示的資料行 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- organizing trace columns displayed [SQL Server]
- arranging trace columns displayed
- traces [SQL Server], data columns
ms.assetid: 6b923f94-0eb1-467e-82f6-ceed43f77017
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e1a884f7c45accefb248029d148feb8b521e6ff4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52763930"
---
# <a name="organize-columns-displayed-in-a-trace-sql-server-profiler"></a>組織追蹤內顯示的資料行 (SQL Server Profiler)
  您可以在追蹤資料表或在 [追蹤檔案屬性] 對話方塊中選取 [組織資料行]，以將追蹤內的資料行加以群組；在定義追蹤時，也可以進行群組。 群組資料行可讓您以更佳的方式分析 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 追蹤輸出。 如需詳細資訊，請參閱[使用 SQL Server Profiler 檢視和分析追蹤](view-and-analyze-traces-with-sql-server-profiler.md)。  
  
 [組織資料行] 可讓您依照所選取的資料行，來群組追蹤事件，或是群組並彙總追蹤事件。  
  
-   選取多個資料行來進行群組，只會群組追蹤事件。 當您選擇多個資料行進行群組時，追蹤視窗會依照您為了進行群組而選取的資料行之值，來群組並顯示事件。 下列範例顯示如果選擇 **Duration** 和 **StartTime** 資料行以進行群組，追蹤視窗方格將如何顯示。 請注意，會先依照 **Duration** 資料行之值的遞增順序，接著再依照 **StartTime** 值來顯示。  
  
|Duration|StartTime|EventClass|ClientProcessID|  
|--------------|---------------|----------------|---------------------|  
||12/12/2006 3:16:43 PM|SQL:StmtStarting|2124|  
|0|12/12/2006 5:39:23 PM|稽核登入|648|  
|1|12/12/2006 5:24:44 PM|SQL:StmtStarting|2124|  
|25|12/12/2006 5:24:44 PM|SQL:StmtCompleted|648|  
  
-   只選擇一個資料行來進行群組，則可群組並彙總追蹤事件。 當您只選擇一個資料行來進行群組時，追蹤視窗會根據該資料行的值來群組並顯示事件，並將其下的所有事件都摺疊起來。 在您選擇用來進行群組的資料行中，事件左邊會出現一個加號 (**+**)，而其下已摺疊的事件數目，則會顯示在事件右邊的括弧內。 下列範例顯示如果只選擇 **EventClass** 資料行來進行群組，追蹤視窗方格將如何顯示。 請注意，所有事件都會組識在 **EventClass** 資料行之下。 若要檢視所有事件，請按一下加號，展開並顯示該類型的所有事件類別。  
  
|EventClass|StartTime|Duration|ClientProcessID|  
|----------------|---------------|--------------|---------------------|  
|+ ExistingConnection (6)||||  
|+ SQL:BatchStarting (25)||||  
|+ SQL:StmtCompleted (11)||||  
|+ SQL:SmtStarting (21)||||  
  
### <a name="to-group-data-columns-displayed-in-a-trace"></a>若要群組追蹤內顯示的資料行  
  
1.  開啟現有的追蹤檔或資料表。  
  
2.  在 [檔案] 功能表上，按一下 [屬性]。  
  
3.  在 [追蹤檔案屬性] 或 [追蹤資料表屬性] 對話方塊中，按一下 [事件選取範圍] 索引標籤。  
  
4.  在 [事件選取範圍] 索引標籤上，按一下 [組織資料行]。  
  
5.  在 [組織資料行] 對話方塊中，選取您要顯示在群組中的資料行，然後按一下 [向上]，將它們移到 [群組] 下方。 將您要移動的所有資料行都移到 [群組] 下方之後，就可以使用 [向上] 和 [向下] 按鈕，重新排列它們的順序。  
  
     將資料行名稱移入 [群組] 清單，表示會先依照 [群組] 清單中最上方資料行之值，再依照 [群組] 清單中第二個資料行之值 (依此類推)，來組織所顯示的追蹤。  
  
6.  按一下 [組織資料行] 對話方塊中的 [確定]，然後在 [追蹤資料表屬性] 或 [追蹤檔案屬性] 對話方塊中按一下 [確定]。  
  
     在 [追蹤資料表屬性] 或 [追蹤檔案屬性] 對話方塊中按一下 [確定] 之後，資料行會在顯示的追蹤內重新組織。 您移到 [群組] 清單中最上方位置的資料行，會位於追蹤顯示內最左邊的方格位置。 追蹤內的資料列，會根據已納入 [群組] 清單中的資料行之值，依遞增順序進行組織。 為了進行群組而選擇的資料行，會固定顯示在畫面中，但是您可以左右捲動以檢視其他資料行。  
  
7.  若要取消群組所顯示的追蹤資料，請按一下 [檢視] 功能表上的 [群組檢視] 以取消選取。 若要再還原為群組檢視，請再按一下 [檢視] 功能表上的 [群組檢視]，以重新選取它。  
  
### <a name="to-group-and-aggregate-data-columns-in-a-trace"></a>若要群組並彙總追蹤內的資料行  
  
1.  開啟現有的追蹤檔或資料表。  
  
2.  在 [檔案] 功能表上，按一下 [屬性]。  
  
3.  在 [追蹤檔案屬性] 或 [追蹤資料表屬性] 對話方塊中，按一下 [事件選取範圍] 索引標籤。  
  
4.  在 [事件選取範圍] 索引標籤上，按一下 [組織資料行]。  
  
5.  在 [組織資料行] 對話方塊中，選取您要群組並彙總所顯示的追蹤事件的資料行。 按一下 [向上]，將資料行名稱移到 [群組] 下方。 視需要使用 [向上] 和 [向下] 按鈕，重新排列 [資料行] 下方的其餘資料行。  
  
6.  按一下 [組織資料行] 對話方塊中的 [確定]，然後在 [追蹤資料表屬性] 或 [追蹤檔案屬性] 對話方塊中按一下 [確定]。  
  
     在 [追蹤資料表屬性] 或 [追蹤檔案屬性] 對話方塊中按一下 [確定] 之後，資料行會在顯示的追蹤內重新組織。 其他所有的資料行，都會彙總在已移入 [群組] 清單的資料行下方。 在您為了進行彙總而選擇的資料行中，按一下事件左邊的加號 (**+**)，即可展開它並檢視該類型的所有事件。 為了進行彙總而選擇的資料行，會固定顯示在畫面中，但是您可以左右捲動以檢視其他資料行。  
  
7.  若要還原為追蹤資料的標準檢視，請按一下 [檢視] 功能表上的 [彙總檢視]，這樣會取消選取。 若要再還原為彙總檢視，請再按一下 [檢視] 功能表上的 [彙總檢視] 以重新選取它。 請注意，您也可以按一下 [檢視] 功能表上的 [群組檢視]，顯示已群組的追蹤事件，但不摺疊它們。  
  
## <a name="see-also"></a>另請參閱  
 [建立追蹤 &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)   
 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)   
 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md)  
  
  
