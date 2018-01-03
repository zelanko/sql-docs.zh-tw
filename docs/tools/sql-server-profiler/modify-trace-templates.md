---
title: "修改追蹤範本 |Microsoft 文件"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- modifying trace templates
- SQL Server Profiler, templates
ms.assetid: 75b62a54-8d16-4599-bd2d-c42cfcc209f4
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27893076b4ec4ba25fb431d577b967571341bec5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="modify-trace-templates"></a>修改追蹤範本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]您可以修改儲存在本機電腦上的檔案所在的範本[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]正在執行。 您也可以修改從這些檔案中衍生的範本。 當您修改現有的範本時，可在 [追蹤屬性] 對話方塊的 [事件選取範圍] 索引標籤上，以原本設定屬性的相同順序來編輯範本屬性，如事件類別與資料行。 事件類別與資料行可以新增或移除，且篩選也可以變更。 範本遭修改後，即會建立使用者特定範本，而原始系統範本則不受影響。 如需詳細資訊，請參閱 [儲存追蹤及追蹤範本](../../tools/sql-server-profiler/save-traces-and-trace-templates.md)。  
  
 如果您不記得用來建立追蹤的原始範本 (或未儲存)，或者您日後想要執行相同的追蹤時，您可能需要從現有的追蹤檔中衍生範本。 使用現有的追蹤時，您可以檢視屬性，但是不能修改屬性。 若要修改屬性，請停止或暫停追蹤。 如需詳細資訊，請參閱[從追蹤檔案或追蹤資料表衍生範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md) 和[從執行中的追蹤衍生範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)。  
  
## <a name="to-modify-a-trace-template"></a>若要修改追蹤範本  
  
1.  在 [檔案] 功能表上，指向 [範本]，再按一下 [編輯範本]。  
  
2.  在 [追蹤範本屬性] 對話方塊的 [一般] 索引標籤上，您可以修改伺服器類型和範本名稱，或選擇使用該伺服器類型的預設範本。  
  
3.  在**事件選取範圍**索引標籤上，使用方格控制項，加入或移除事件和資料行在追蹤檔案中，，如下所示。  
  
    -   若要加入事件，請在 **[事件]** 資料行中展開適當的事件類別目錄，然後選取事件名稱。  
  
    -   當您加入事件時，依預設將包含所有有關的資料行。 若要從追蹤中移除某個事件的資料行，請清除該事件在資料行中的核取方塊。  
  
    -   若要加入篩選，在 **[編輯篩選]** 對話方塊中按一下資料行名稱，然後指定篩選準則。 您也可以用滑鼠右鍵按一下資料行名稱，然後按一下 [編輯資料行篩選] 以啟動 [編輯篩選] 對話方塊。 按一下 **[確定]** 以加入篩選。  
  
4.  按一下**儲存**，或按一下**存**儲存追蹤範本，另一個名稱。  
  
## <a name="next-steps"></a>後續步驟  
[啟動追蹤](../../tools/sql-server-profiler/start-a-trace.md)  
[建立追蹤](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
[修改現有的追蹤使用 TRANSACT-SQL](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
[指定使用 SQL Server Profiler 追蹤事件和資料行](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
[預存程序追蹤-setevent-transact-sql](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
