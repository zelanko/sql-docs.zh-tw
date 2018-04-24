---
title: 活動監視器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Activity Monitor [SQL Server]
ms.assetid: 1e6c430d-3a2a-468e-a3d5-ef5459c36c15
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d879d8a766ec2aa368f6ab6efa9c24312d132421
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="activity-monitor"></a>活動監視器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  活動監視器顯示有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序以及這些處理序如何影響目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的詳細資訊。  
  
 活動監視器是一個索引標籤式文件視窗，其中包含下列可展開且可摺疊的窗格：[概觀]、[作用中使用者工作]、[資源等候]、[資料檔案 I/O] 和 [最近且費時的查詢]。 展開任何窗格時，活動監視器會查詢執行個體以便取得相關資訊。 摺疊某個窗格時，該窗格的所有查詢活動就會停止。 您可以同時展開一或多個窗格，以便檢視不同種類的執行個體活動。  
 
 ## <a name="customize-columns"></a>自訂資料行 
 對於包含在 [作用中使用者工作]、[資源等候]、[資料檔案 I/O] 和 [最近且費時的查詢] 窗格中的資料行，您可以如下所示自訂顯示：  
  
1.  若要重新排列資料行順序，請按一下資料行標題並將它拖曳至標題功能區中的其他位置。  
  
2.  若要排序資料行，請按一下資料行名稱。  
  
3.  若要篩選一個或多個資料行，請按一下資料行標題中的下拉式箭頭，然後選取一個值。  
  
## <a name="more-information"></a>詳細資訊  
   
|||  
|-|-|  
|描述如何開啟 [活動監視器] 以及如何設定 [活動監視器] 的重新整理間隔。|[開啟活動監視器 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)|  
|伺服器效能和活動監視主題的連結。|[伺服器效能與活動監視](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|  
  
  
