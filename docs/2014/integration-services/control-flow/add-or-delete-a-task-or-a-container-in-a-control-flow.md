---
title: 在控制流程中新增或刪除工作或容器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f13db8a1e22c88c4433cd8928479a6ed1af540f6
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380156"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>在控制流程中加入或刪除工作或容器
  當您在控制流程設計師中工作時，[ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中的 [工具箱] 會列出 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供用於在封裝中建立控制流程的工作。 如需工具箱的詳細資訊，請參閱 [SSIS 工具箱](../ssis-toolbox.md)。  
  
 封裝可以包含同一工作的多個執行個體。 工作的每個執行個體都在封裝中唯一識別，且您可以對每個執行個體進行不同的設定。  
  
 如果您刪除工作，則亦會刪除將工作連接到控制流程中其他工作及容器的優先順序條件約束。  
  
 下列程序將描述如何在封裝的控制流程中加入或刪除工作或容器。  
  
### <a name="to-add-a-task-or-a-container-to-a-control-flow"></a>將工作或容器加入控制流程  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  若要開啟 [工具箱]，請按一下 [檢視] 功能表上的 [工具箱]。  
  
5.  展開 [控制流程項目] 和 [維護工作]。  
  
6.  將工作和容器從 [工具箱] 拖曳至 [控制流程] 索引標籤的設計介面。  
  
7.  透過將其連接子拖曳至控制流程中的另一元件，連接封裝控制流程內的工作或容器。  
  
8.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-delete-a-task-or-a-container-from-a-control-flow"></a>從控制流程中刪除工作或容器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。 執行下列其中之一：  
  
    -   按一下 [控制流程] 索引標籤，以滑鼠右鍵按一下您要移除的工作或容器，然後按一下 [刪除]。  
  
    -   開啟 [封裝總管]。 從 [可執行檔] 資料夾，以滑鼠右鍵按一下您要移除的工作或容器，然後按一下 [刪除]。  
  
3.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](integration-services-tasks.md)   
 [Integration Services 容器](integration-services-containers.md)   
 [[控制流程]](control-flow.md)  
  
  
