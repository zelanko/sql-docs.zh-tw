---
title: 建立追蹤範本
titleSuffix: SQL Server Profiler
description: 探索如何在 SQL Server Profiler 中建立新的追蹤範本。 了解如何將篩選新增至範本，以及如何新增或移除事件和資料行。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 025868b0-3790-4cda-8757-5a58327bfba0
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: af272f50f281a8c3a564913cfb91be8abcab2898
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774874"
---
# <a name="create-a-trace-template-sql-server-profiler"></a>建立追蹤範本 (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]來建立新追蹤範本。  
  
### <a name="to-create-a-trace-template"></a>若要建立追蹤範本  
  
1.  在 **[檔案]** 功能表上，指向 **[範本]** ，然後按一下 **[新增範本]** 。  
  
2.  在 [追蹤範本屬性] 對話方塊中，從 [選取伺服器類型] 清單中選取伺服器類型。  
  
3.  在 **[新範本名稱]** 方塊中，輸入範本名稱。  
  
4.  (選擇性) 按一下 **[以現有的範本作為新範本的基礎]** ，然後從清單中選取範本。  
  
     所有事件、資料行與篩選會依所選取範本的指定來初始設定。  
  
5.  (選擇性) 按一下 **[作為所選取伺服器類型的預設範本]** 。  
  
6.  在 **[事件選取範圍]** 索引標籤上，新增、移除或修改事件、資料行或篩選。  
  
7.  在 **[事件選取範圍]** 索引標籤上，使用方格控制項，在追蹤檔案中新增或移除事件和資料行，如下所示：  
  
    -   若要加入事件，請在 **[事件]** 資料行中展開適當的事件類別目錄，然後選取事件名稱。  
  
    -   當您加入事件時，依預設將包含所有有關的資料行。 若要從追蹤中移除某個事件的資料行，請清除該事件在資料行中的核取方塊。  
  
    -   若要加入篩選，在 **[編輯篩選]** 對話方塊中按一下資料行名稱，然後指定篩選準則。 您也可以用滑鼠右鍵按一下資料行名稱，然後按一下 [編輯資料行篩選] 以啟動 [編輯篩選] 對話方塊。 按一下 **[確定]** 以加入篩選。  
  
8.  按一下 [儲存]。  
  
## <a name="see-also"></a>另請參閱  
 [指定追蹤檔案的事件及資料行 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [從執行中的追蹤衍生範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [從追蹤檔案或追蹤資料表衍生範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler 範本和權限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
