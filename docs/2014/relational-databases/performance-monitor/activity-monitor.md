---
title: 活動監視器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Activity Monitor [SQL Server]
ms.assetid: 1e6c430d-3a2a-468e-a3d5-ef5459c36c15
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 683e1c41e6f0edb45cd7c0da1b52622818d441b9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031413"
---
# <a name="activity-monitor"></a>活動監視器
  活動監視器顯示有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序以及這些處理序如何影響目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的詳細資訊。  
  
## <a name="benefits-of-activity-monitor"></a>活動監視器的優點  
 活動監視器是一個索引標籤式文件視窗具有下列可展開及摺疊的窗格：**概觀**，**作用中使用者工作**，**資源等候**， **資料檔案 I/O**，和**最近且費時的查詢**。 展開任何窗格時，活動監視器會查詢執行個體以便取得相關資訊。 摺疊某個窗格時，該窗格的所有查詢活動就會停止。 您也可以同時展開一或多個窗格，以便檢視不同種類的執行個體活動。  
  
 中包含的資料行**作用中使用者工作**，**資源等候**，**資料檔案 I/O**，和**最近且費時的查詢**窗格中，您可以下列方式自訂顯示：  
  
1.  若要重新排列資料行的順序，請按一下資料行標題並將它拖曳至標題功能區中的其他位置。  
  
2.  若要排序資料行，請按一下資料行名稱。  
  
3.  若要篩選一個或多個資料行，請按一下資料行標題中的下拉式箭頭，然後選取一個值。  
  
## <a name="related-tasks"></a>相關工作  
 若要開始使用 [活動監視器]，請使用下列工作：  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何開啟 [活動監視器] 以及如何設定 [活動監視器] 的重新整理間隔。|[開啟活動監視器 &#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)|  
|伺服器效能和活動監視主題的連結。|[伺服器效能與活動監視](../performance/server-performance-and-activity-monitoring.md)|  
  
  