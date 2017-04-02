---
title: "修改篩選 (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "篩選 [SQL Server], 修改"
  - "修改篩選, 修改"
  - "篩選 [SQL Server], 追蹤"
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# 修改篩選 (SQL Server Profiler)
  您可以將篩選加入包含追蹤定義的追蹤範本，以限制追蹤所蒐集的事件數目。 限制蒐集的事件數目可以降低追蹤的效能影響。 如果您設定追蹤範本的篩選，但發現追蹤並未蒐集您所需要的資訊種類，您就可以編輯篩選。  
  
### 若要修改篩選  
  
1.  在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 中，開啟您要修改的追蹤篩選範本。 在 [檔案] 功能表上，按一下 [範本]，然後選擇 [編輯範本]。  
  
2.  在 [追蹤範本屬性] 對話方塊的 [一般] 索引標籤中，從 [選取範本名稱] 清單中選取範本。  
  
3.  按一下 [事件選取範圍] 索引標籤。  
  
     **[事件選取範圍]** 索引標籤包含方格控制項。 方格控制項是包含每一個可追蹤事件類別的資料表。 資料表針對每個事件類別包含一個資料列。 事件類別可能會依您所連接的伺服器類型與版本而稍有不同。 事件類別在方格的 [事件] 資料行中識別，並依事件類別目錄分組。 其餘資料行會列出可針對每個事件類別傳回的資料行。  
  
4.  按一下 [資料行篩選]。  
  
5.  在 [編輯篩選] 對話方塊中，按一下您要編輯之比較運算子旁的值，然後輸入新的值或刪除一個值。 您也可以加入其他篩選。  
  
6.  按一下 [確定] 並儲存範本。  
  
## 另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  