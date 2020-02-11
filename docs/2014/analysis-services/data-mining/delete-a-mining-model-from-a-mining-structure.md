---
title: 從採礦結構中刪除採礦模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], mining models
- deleting mining models
- removing mining models
- mining models [Analysis Services], deleting
ms.assetid: 9ab1506b-856e-4762-a663-5adf15ac71e3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d4e32a40946eb9e513ad22cd837773187843151
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084776"
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>從採礦結構刪除採礦模型
  您可以使用資料採礦設計師、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 DMX 陳述式來刪除採礦模型。  
  
### <a name="delete-a-mining-model-using-sql-server-data-tools"></a>使用 SQL Server 資料工具刪除採礦模型  
  
1.  選取 ** 中的 [採礦模型]**[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 索引標籤。  
  
2.  以滑鼠右鍵按一下您想刪除的模型，然後選取 [刪除]****。  
  
     [刪除物件]**** 對話方塊就會開啟。  
  
3.  按一下 [確定]  。  
  
### <a name="delete-a-mining-model-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 刪除採礦模型  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟包含模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
2.  展開 [採礦結構]****，然後展開 [採礦模型]****。  
  
3.  以滑鼠右鍵按一下您想刪除的模型，然後選取 [刪除]****。  
  
     刪除模型並不會刪除定型資料，只刪除定型模型時建立的中繼資料和所有模式。  
  
### <a name="delete-a-mining-model-using-dmx"></a>使用 DMX 刪除採礦模型  
  
-   [捨棄 &#40;DMX&#41;的採礦模型](/sql/dmx/drop-mining-model-dmx)  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型工作和使用說明](mining-model-tasks-and-how-tos.md)  
  
  
