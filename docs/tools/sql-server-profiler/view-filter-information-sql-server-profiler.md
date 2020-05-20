---
title: 檢視篩選資訊
titleSuffix: SQL Server Profiler
description: 了解如何檢視 SQL Server Profiler 目前套用至資料行的篩選，以限制追蹤的事件。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 8d002dea-376a-452c-b3ca-3e93656ed75f
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 39c2d73e634d26ab28b890d72f08b55abfe2394b
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151627"
---
# <a name="view-filter-information-sql-server-profiler"></a>檢視篩選資訊 (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，在事件類別的資料行上檢視篩選。  
  
### <a name="to-view-filter-information"></a>若要檢視篩選資訊  
  
1.  開啟追蹤檔案、追蹤資料表或 SQL 指令碼，然後在 [檔案] 功能表上按一下 [屬性]。 如果您正在編輯追蹤範本或正在建立新追蹤，請略過此步驟。  
  
2.  在 [事件選取範圍] 索引標籤上，以滑鼠右鍵按一下要檢視之篩選的資料行名稱，然後按一下 [編輯資料行篩選]。  
  
3.  在 [編輯篩選] 對話方塊中，展開篩選比較運算子，查看所指定條件已指派的值。 對於您要檢視篩選資訊的所有資料行，重複步驟 2 和 3。  
  
> [!NOTE]  
>  已指派值的比較運算子會顯示為粗體格式。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
