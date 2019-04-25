---
title: 從採礦結構刪除採礦模型 |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b17489213e0f057d8f291095f01b65f97a977ff1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468841"
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>從採礦結構刪除採礦模型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以使用資料採礦設計師、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 DMX 陳述式來刪除採礦模型。  
  
### <a name="delete-a-mining-model-using-sql-server-data-tools"></a>使用 SQL Server 資料工具刪除採礦模型  
  
1.  選取 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的 [採礦模型] 索引標籤。  
  
2.  以滑鼠右鍵按一下您想刪除的模型，然後選取 [刪除]。  
  
     [刪除物件] 對話方塊就會開啟。  
  
3.  按一下 [確定] 。  
  
### <a name="delete-a-mining-model-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 刪除採礦模型  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，開啟包含模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
2.  展開 [採礦結構]，然後展開 [採礦模型]。  
  
3.  以滑鼠右鍵按一下您想刪除的模型，然後選取 [刪除]。  
  
     刪除模型並不會刪除定型資料，只刪除定型模型時建立的中繼資料和所有模式。  
  
### <a name="delete-a-mining-model-using-dmx"></a>使用 DMX 刪除採礦模型  
  
-   [DROP MINING MODEL &#40;DMX&#41;](../../dmx/drop-mining-model-dmx.md)  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型工作和操作說明](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
