---
title: 工作3：針對供應商知識庫清理資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 647c924a-9b91-4294-8d96-e81416e4e90e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 13201a8b904a5fc5232b9fa860710e4e39cce67a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064761"
---
# <a name="task-3-cleansing-data-against-the-suppliers-knowledge-base"></a>工作 3：針對供應商知識庫清理資料
  在這項工作中，您會執行電腦輔助的清理程序。 DQS 會根據為了針對選取的知識庫分析及清理資料所指定的臨界值，使用進階演算法與信賴等級。 如需詳細資訊，請參閱[使用 DQS （內部）知識清理資料](https://msdn.microsoft.com/library/hh213061.aspx)。

1.  按一下 [**啟動**] 以啟動電腦輔助的清理程式。

     ![清理程序的 [清理] 頁面](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-01.jpg "清理程序的 [清理] 頁面")

2.  清理程式完成時，**請在 [分析工具] 索引**標籤中檢查**統計資料**。來源統計資料會提供已處理的記錄數目、找到正確的記錄數目、DQS 更正的記錄數目、有 DQS 建議變更的記錄數目，以及不正確記錄數目。 在右邊的清單方塊中，您可以看到清理程序中每一個相關定義域的更正值、建議值及完整性 (資料存在的程度) 和精確度 (資料可用於預定用途的程度) 等值。

     ![清理結果](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-02.jpg "清理結果")

3.  按 **[下一步]** 以切換至 [**管理及查看結果**] 頁面。

## <a name="next-step"></a>後續步驟
 [工作 4：管理和檢視結果](../../2014/tutorials/task-4-manaing-and-viewing-results.md)


