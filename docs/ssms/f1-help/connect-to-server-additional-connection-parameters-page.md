---
title: "連接到伺服器 (其他連接參數頁面) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
ms.assetid: ba34b01a-6289-4eb8-8341-fa3d9ec87b3f
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7befc61bcf4a973aa0593e476bcce76f5751f40b
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-additional-connection-parameters-page"></a>連接到伺服器 (其他連接參數頁面)
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 的 [連接到]**** 對話方塊會將最常用的連接字串值呈現為選項。 使用 [其他連接參數]**** 頁面可將更多連接參數新增到連接字串。  
  
-   其他連接參數可以是任何 ODBC 連接參數。  
  
-   其他連接參數應該使用以下格式來新增：**;parameter1=value1;parameter2=value2**。  
  
-   使用 [其他連接參數]**** 頁面新增的參數會新增到使用 [連接到]**** 對話方塊選項所選取的參數中。  
  
-   提供之每一個參數的最後一個執行個體都會覆寫該參數之前的任何執行個體。 使用 [其他連接參數]**** 頁面新增的參數會遵循及取代 [登入]**** 或 [連接屬性]**** 索引標籤內提供的參數。 例如，如果 [登入]**** 索引標籤提供 **SERVER1** 當作 [伺服器名稱]****，而且 [其他連接參數]**** 頁面包含 **;SERVER=SERVER2**，將會對 **SERVER2** 進行連接。  
  
-   使用 [其他連接參數]**** 頁面新增的參數一定會以純文字格式傳遞。  
  
    > [!IMPORTANT]  
    > 請勿在 [其他連接參數]**** 頁面上包含登入認證和密碼。 當透過網路傳遞認證和密碼時，將不會加密。 請改用 [登入]**** 索引標籤。  
  
## <a name="task-list"></a>工作清單  
  
### <a name="to-show-the-additional-connection-parameters-page"></a>顯示其他連接參數頁面  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 的 [查詢]**** 功能表上，指向 [連接]****，然後按一下 [連接]****。  
  
2.  在 [連接到]**** 對話方塊中，按一下 [選項]****，然後按一下 [其他連接參數]**** 索引標籤。  
  
## <a name="examples"></a>範例  
  
### <a name="example-a-connecting-to-the-database-engine"></a>範例 A：連接到 Database Engine  
若要連接到 ACCOUNTING 伺服器上的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 資料庫，請在 [其他連接參數]**** 頁面內輸入以下程式碼：  
  
```  
;SERVER=ACCOUNTING;DATABASE=AdventureWorks2012  
```  
  
### <a name="example-b-connecting-to-analysis-services"></a>範例 B：連接到 Analysis Services  
若要連接到 Analysis Servers 並使得接聽通知的所有資料分割都得以即時查詢 (略過快取)，同時將回寫逾時值設定為 5，請在 [其他連接參數]**** 頁面內輸入以下程式碼：  
  
```  
;Real Time Olap=TRUE;Writeback Timeout=5  
```  
  

