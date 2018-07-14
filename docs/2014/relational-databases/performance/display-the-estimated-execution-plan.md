---
title: 顯示估計的執行計畫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6b8fe5d5f733592ae51f91b4e8b9956b8489e1a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280857"
---
# <a name="display-the-estimated-execution-plan"></a>顯示估計的執行計畫
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]產生圖形化的估計執行計畫。 產生估計執行計畫時，不會執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢或批次。 不過，所產生的執行計畫會顯示若是真的執行查詢， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 最有可能使用的查詢執行計畫。  
  
 若要使用這個功能，使用者必須具有適當的權限來執行要產生圖形執行計畫的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢，而且必須獲得查詢所參考的所有資料庫的 SHOWPLAN 權限。  
  
### <a name="to-display-the-estimated-execution-plan-for-a-query"></a>若要顯示查詢的評估執行計畫  
  
1.  在工具列上，按一下 [Database Engine 查詢]。 您也可以按一下 [開啟檔案] 工具列按鈕並找出現有的查詢，以開啟現有的查詢並顯示估計的執行計畫。  
  
2.  輸入您要顯示估計執行計畫的查詢。  
  
3.  在 [查詢] 功能表上，按一下 [顯示估計執行計畫]，或按一下 [顯示估計執行計畫] 工具列按鈕。 估計執行計畫會顯示在結果窗格中的 [執行計畫] 索引標籤。 若要檢視其他資訊，請將滑鼠暫時放在邏輯與實體運算子的圖示上，即可在顯示的 [工具提示] 中檢視運算子的說明與屬性。 或者，您可以在 [屬性] 視窗中檢視運算子屬性。 如果沒有看到 [屬性] 視窗，請以滑鼠右鍵按一下運算子，然後按一下 [屬性]。 選取運算子以檢視其屬性。  
  
4.  若要改變執行計劃的顯示，請以滑鼠右鍵按一下 [執行計畫]，然後選取 [放大]、[縮小]、[自訂顯示比例] 或 [縮放至適當比例]。 [放大] 與 [縮小] 可讓您以固定量放大或縮小執行計畫。 [自訂顯示比例] 可讓您定義自己的顯示倍率，例如縮放至百分之 80。 [縮放至適當比例] 會放大執行計畫，以符合結果窗格的大小。  
  
  
