---
title: 篩選追蹤中的伺服器處理序識別碼 (SPID) (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5262d9a261e1fa9cb6cb0950f8509253d7eaced5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47744696"
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>篩選追蹤中的伺服器處理序識別碼 (SPID) (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，篩選追蹤中的伺服器處理序識別碼 (SPID)。  
  
### <a name="to-filter-system-ids-in-a-trace"></a>若要篩選追蹤系統識別碼  
  
1.  在 **[檔案]** 功能表上按一下 **[新增追蹤]**，然後連接到 SQL Server 的執行個體。  
  
     會出現 [追蹤屬性]  對話方塊。  
  
    > [!NOTE]  
    >  如果選取 [進行連線後立即啟動追蹤]，將不會顯示 [追蹤屬性] 對話方塊，而是開始追蹤。 若要關閉這個設定，請在 [工具] 功能表上按一下 [選項]，然後清除 [進行連線後立即啟動追蹤] 核取方塊。  
  
2.  在 **[追蹤名稱]** 方塊中，輸入追蹤的名稱。  
  
3.  在 [使用範本] 名稱清單中，選取追蹤範本。  
  
4.  選擇性，指定要儲存追蹤結果的目的地檔案或資料表。  
  
5.  在 [事件選取範圍] 索引標籤上，按一下 [SPID] 資料行標題，以啟動 [編輯篩選] 對話方塊。 您也可以用滑鼠右鍵按一下資料行標題，然後選擇 [編輯資料行篩選]。 如果 [SPID] 資料行未出現，請核取 [顯示所有資料行] 方塊。  
  
6.  在 [編輯篩選] 對話方塊中，展開適當的比較運算子，然後輸入 SPID 作為比較的值。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
