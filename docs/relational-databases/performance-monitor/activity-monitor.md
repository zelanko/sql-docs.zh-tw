---
title: 活動監視器 | Microsoft Docs
ms.custom: ''
ms.date: 04/07/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server]
ms.assetid: 1e6c430d-3a2a-468e-a3d5-ef5459c36c15
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 1332575178ac4ac94802e948b1725164419fa6ad
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2019
ms.locfileid: "67580759"
---
# <a name="activity-monitor"></a>活動監視器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
活動監視器顯示有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序以及這些處理序如何影響目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的詳細資訊。  
  
活動監視器是一個索引標籤式文件視窗，其中包含下列可展開且可摺疊的窗格：[概觀]  、[處理序]  、[資源等候]  、[資料檔案 I/O]  和 [最近的費時查詢]  和 [使用中的費時查詢]  。 展開任何窗格時，活動監視器會查詢執行個體以便取得相關資訊。 摺疊某個窗格時，該窗格的所有查詢活動就會停止。 您可以同時展開一或多個窗格，以便檢視不同種類的執行個體活動。  
 
## <a name="customize-columns"></a>自訂資料行 
對於包含在 [處理序]  、[資源等候]  、[資料檔案 I/O]  和 [最近的費時查詢]  和 [使用中的費時查詢]  窗格中的資料行，您可以如下所示自訂顯示：  
  
1.  若要重新排列資料行順序，請按一下資料行標題並將它拖曳至標題功能區中的其他位置。  
  
2.  若要排序資料行，請按一下資料行名稱。  
  
3.  若要篩選一個或多個資料行，請按一下資料行標題中的下拉式箭頭，然後選取一個值。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="more-information"></a>詳細資訊  
   
|||  
|-|-|  
|描述如何開啟 [活動監視器] 以及如何設定 [活動監視器] 的重新整理間隔。|[開啟活動監視器 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)|  
|伺服器效能和活動監視主題的連結。|[伺服器效能與活動監視](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|  
  
  
