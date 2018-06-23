---
title: SQL Server Profiler-效能計數器限制 |Microsoft 文件
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
- sql12.pro.performancecounterlimit.f1
helpviewer_keywords:
- Performance Counters List dialog box
ms.assetid: d10140ef-36c4-449c-b365-1cff1b2524e4
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2548fbd28af45cbd888a183a739362f0e7767218
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034634"
---
# <a name="sql-server-profiler---performance-counters-limit"></a>SQL Server Profiler - 效能計數器限制
  使用 [效能計數器限制] 對話方塊，即可在與 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 追蹤建立相互關聯時，限制系統監視器效能記錄檔的資訊。 您可以使用此對話方塊，來選取應該顯示及用於建立相互關聯的計數器。  
  
 **[效能計數器限制]** 對話方塊，會以效能記錄檔所包含的效能物件和計數器來擴展。  
  
### <a name="to-select-performance-objects-and-counters-to-correlate-with-a-trace"></a>若要選取效能物件和計數器來建立追蹤的相互關聯  
  
1.  展開效能物件來查看哪些計數器已包含在效能記錄檔中。  
  
2.  核取您要與 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 追蹤檔建立相互關聯的計數器。  
  
     如果您要選取效能物件的所有計數器，請核取該效能物件相鄰的方塊。 核取最頂端的節點 (指出電腦)，就會選取效能記錄檔中所包含的所有效能物件和計數器。  
  
## <a name="see-also"></a>另請參閱  
 [使追蹤與 Windows 效能記錄資料相互關聯 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data.md)  
  
  