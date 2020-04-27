---
title: SQL Server Profiler-尋找對話方塊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.find.f1
helpviewer_keywords:
- Find dialog box
ms.assetid: dfaeec04-93d3-4214-9fc1-38b80179b36b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 81ed454290a5ca62093fe9bdb619179106ca9985
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088860"
---
# <a name="sql-server-profiler---find-dialog-box"></a>SQL Server Profiler - 尋找對話方塊
  使用 [尋找]**** 對話方塊，即可針對追蹤搜尋特定字元或文字。 若要取消進行中的搜尋，請按下 ESC 鍵。  
  
 若要在 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 中開啟此對話方塊，請在 [編輯]**** 功能表上按一下 [尋找]**Find**。  
  
## <a name="options"></a>選項。  
 **尋找目標**  
 輸入您想要搜尋的文字。 搜尋會找出其中包含指定字串的字串。 例如，搜尋 "Completed" 會與 "SQL:BatchCompleted" 相符。 不支援萬用字元 (*、? 等等)。  
  
 **在資料行中搜尋**  
 按一下要搜尋的資料行，或按一下** \<[所有資料行]>** ，即可搜尋追蹤中的所有資料行。  
  
 **大小寫須相符**  
 尋找與 [尋找目標]**** 方塊中的大小寫相同的文字。 清除此核取方塊，即可在追蹤中同時尋找大寫與小寫文字字元的範例。  
  
 **全字拼寫須相符**  
 將搜尋限制為整個文字。 清除 [全字拼寫須相符]**** 核取方塊來搜尋文字內的所有字元。  
  
 **找下一個**  
 尋找 [尋找目標]**** 方塊中之字元的下一個範例。  
  
 **找上一個**  
 在追蹤中向後搜尋，以尋找 [尋找目標]**** 方塊中之字元的上一個範例。  
  
## <a name="see-also"></a>另請參閱  
 [追蹤 &#40;SQL Server Profiler 時，尋找值或資料行&#41;](../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)   
 [建立追蹤 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [SQL Server Profiler 範本和許可權](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
