---
title: 修改追蹤範本 (SQL Server Profiler) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- modifying traces
ms.assetid: b81df2a1-e202-43d8-92b0-0beb145f0116
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: afa7876575dca287f492f07cc69d6dd7dfe27222
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035748"
---
# <a name="modify-a-trace-template-sql-server-profiler"></a>修改追蹤範本 (SQL Server Profiler)
  本主題說明如何使用 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 來修改追蹤範本。  
  
### <a name="to-modify-a-trace-template"></a>若要修改追蹤範本  
  
1.  在 [檔案] 功能表上，指向 [範本]，再按一下 [編輯範本]。  
  
2.  在 [追蹤範本屬性] 對話方塊的 [一般] 索引標籤上，您可以修改伺服器類型和範本名稱，或選擇使用該伺服器類型的預設範本。  
  
3.  在 [事件選取範圍]索引標籤上，使用方格控制項，在追蹤檔案中新增或移除事件和資料行，如下所示：  
  
    -   若要加入事件，請在 **[事件]** 資料行中展開適當的事件類別目錄，然後選取事件名稱。  
  
    -   當您加入事件時，依預設將包含所有有關的資料行。 若要從追蹤中移除某個事件的資料行，請清除該事件在資料行中的核取方塊。  
  
    -   若要加入篩選，在 **[編輯篩選]** 對話方塊中按一下資料行名稱，然後指定篩選準則。 您也可以用滑鼠右鍵按一下資料行名稱，然後按一下 [編輯資料行篩選] 以啟動 [編輯篩選] 對話方塊。 按一下 **[確定]** 以加入篩選。  
  
4.  按一下 [儲存]，或按一下 [另存新檔]，以另一個名稱儲存追蹤範本。  
  
## <a name="see-also"></a>另請參閱  
 [指定追蹤檔案的事件及資料行&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [從執行中的追蹤衍生範本 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [從追蹤檔案或追蹤資料表衍生範本 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler 範本和權限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  