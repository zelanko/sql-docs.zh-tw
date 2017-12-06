---
title: "建立追蹤範本 (SQL Server Profiler) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- saving trace template
ms.assetid: 025868b0-3790-4cda-8757-5a58327bfba0
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c22c0835d1f5f15e4961cc07bd426af268396c7e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="create-a-trace-template-sql-server-profiler"></a>建立追蹤範本 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]本主題描述如何使用建立新的追蹤範本[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。  
  
### <a name="to-create-a-trace-template"></a>若要建立追蹤範本  
  
1.  在 **[檔案]** 功能表上，指向 **[範本]**，然後按一下 **[新增範本]**。  
  
2.  在 [追蹤範本屬性] 對話方塊中，從 [選取伺服器類型] 清單中選取伺服器類型。  
  
3.  在 **[新範本名稱]** 方塊中，輸入範本名稱。  
  
4.  (選擇性) 按一下 **[以現有的範本作為新範本的基礎]**，然後從清單中選取範本。  
  
     所有事件、資料行與篩選會依所選取範本的指定來初始設定。  
  
5.  (選擇性) 按一下 **[作為所選取伺服器類型的預設範本]**。  
  
6.  在 **[事件選取範圍]** 索引標籤上，新增、移除或修改事件、資料行或篩選。  
  
7.  在 **[事件選取範圍]**索引標籤上，使用方格控制項，在追蹤檔案中新增或移除事件和資料行，如下所示：  
  
    -   若要加入事件，請在 **[事件]** 資料行中展開適當的事件類別目錄，然後選取事件名稱。  
  
    -   當您加入事件時，依預設將包含所有有關的資料行。 若要從追蹤中移除某個事件的資料行，請清除該事件在資料行中的核取方塊。  
  
    -   若要加入篩選，在 **[編輯篩選]** 對話方塊中按一下資料行名稱，然後指定篩選準則。 您也可以用滑鼠右鍵按一下資料行名稱，然後按一下 [編輯資料行篩選] 以啟動 [編輯篩選] 對話方塊。 按一下 **[確定]** 以加入篩選。  
  
8.  按一下 **[儲存].**  
  
## <a name="see-also"></a>另請參閱  
 [指定追蹤檔案的事件及資料行 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [從執行中的追蹤 &#40; 衍生範本SQL Server Profiler &#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [從追蹤檔案或追蹤資料表 &#40; 衍生範本SQL Server Profiler &#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler 範本和權限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
