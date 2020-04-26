---
title: 視圖篩選資訊（SQL Server Profiler） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: 8d002dea-376a-452c-b3ca-3e93656ed75f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8496eee2134d9f89163fce6b6ad3ef07ba49b1af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63276795"
---
# <a name="view-filter-information-sql-server-profiler"></a>檢視篩選資訊 (SQL Server Profiler)
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，在事件類別的資料行上檢視篩選。  
  
### <a name="to-view-filter-information"></a>若要檢視篩選資訊  
  
1.  開啟追蹤檔案、追蹤資料表或 SQL 指令碼，然後在 [檔案]  功能表上按一下 [屬性]  。 如果您正在編輯追蹤範本或正在建立新追蹤，請略過此步驟。  
  
2.  在 [事件選取範圍]  索引標籤上，以滑鼠右鍵按一下要檢視之篩選的資料行名稱，然後按一下 [編輯資料行篩選]  。  
  
3.  在 [編輯篩選]  對話方塊中，展開篩選比較運算子，查看所指定條件已指派的值。 對於您要檢視篩選資訊的所有資料行，重複步驟 2 和 3。  
  
> [!NOTE]  
>  已指派值的比較運算子會顯示為粗體格式。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
