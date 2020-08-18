---
description: 在控制流程中加入或刪除工作或容器
title: 在控制流程中新增或刪除工作或容器 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bc573bfaf7f68102631e4e65c607e76062c147ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88350064"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>在控制流程中加入或刪除工作或容器

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  當您在控制流程設計師中工作時，[ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中的 [工具箱] 會列出 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供用於在封裝中建立控制流程的工作。 如需工具箱的詳細資訊，請參閱 [SSIS 工具箱](../../integration-services/ssis-toolbox.md)。  
  
 封裝可以包含同一工作的多個執行個體。 工作的每個執行個體都在封裝中唯一識別，且您可以對每個執行個體進行不同的設定。  
  
 如果您刪除工作，則亦會刪除將工作連接到控制流程中其他工作及容器的優先順序條件約束。  
  
 下列程序將描述如何在封裝的控制流程中加入或刪除工作或容器。  
  
## <a name="add-a-task-or-a-container-to-a-control-flow"></a>將工作或容器新增至控制流程  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  若要開啟 [工具箱]****，請按一下 [檢視]**** 功能表上的 [工具箱]****。  
  
5.  展開 [控制流程項目]**** 和 [維護工作]****。  
  
6.  將工作和容器從 [工具箱]**** 拖曳至 [控制流程]**** 索引標籤的設計介面。  
  
7.  透過將其連接子拖曳至控制流程中的另一元件，連接封裝控制流程內的工作或容器。  
  
8.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="delete-a-task-or-a-container-from-a-control-flow"></a>從控制流程中刪除工作或容器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。 執行下列其中一個動作：  
  
    -   按一下 [控制流程]**** 索引標籤，以滑鼠右鍵按一下您要移除的工作或容器，然後按一下 [刪除]****。  
  
    -   開啟 [封裝總管]****。 從 [可執行檔]**** 資料夾，以滑鼠右鍵按一下您要移除的工作或容器，然後按一下 [刪除]****。  
  
3.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  

## <a name="set-the-properties-of-a-task-or-container"></a>設定工作或容器的屬性
您可以使用 [屬性]**** 視窗來設定工作和容器的大部分屬性。 例外的是工作集合的屬性，以及因太複雜而無法使用 [屬性]**** 視窗設定的屬性。 例如，您無法在 [屬性]**** 視窗中設定「Foreach 迴圈」容器所使用的列舉值。 您必須使用工作或容器編輯器來設定這些複雜屬性。 大部分工作和容器編輯器都具有多個節點，而且每個節點都包含相關的屬性。 節點的名稱表示此節點所包含之屬性的主旨。  
  
 下列程序將描述如何使用 [屬性]**** 視窗或對應的工作或容器編輯器來設定工作或容器的屬性。  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-properties-window"></a>使用 [屬性] 視窗來設定工作或容器的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  在 [控制流程]**** 索引標籤的設計介面上，以滑鼠右鍵按一下工作或容器，然後按一下 [屬性]****。  
  
5.  在 [屬性]**** 視窗中更新屬性值。  
  
    > [!NOTE]  
    >  大部分的屬性都可以經由直接在文字方塊中輸入某個值，或從清單中選取某個值予以設定。 不過，有些屬性比較複雜，並具有自訂屬性編輯器。 若要設定這種屬性，請按一下文字方塊，然後按一下建立 ([...])**** 按鈕開啟自訂編輯器。  
  
6.  (選擇性) 建立屬性運算式，以動態方式更新工作或容器的屬性。 如需詳細資訊，請參閱[加入或變更屬性運算式](../../integration-services/expressions/add-or-change-a-property-expression.md)。  
  
7.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-task-or-container-editor"></a>使用工作或容器編輯器來設定工作或容器的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  在 [控制流程]**** 索引標籤的設計介面上，以滑鼠右鍵按一下工作或容器，然後按一下 [編輯]**** 開啟對應的工作或容器編輯器。  
  
     如需如何設定「For 迴圈」容器的資訊，請參閱[設定 For 迴圈容器](https://msdn.microsoft.com/library/b9cd7ea7-b198-4a35-8b16-6acf09611ca5)。  
  
     如需如何設定Foreach 迴圈容器的資訊，請參閱 [設定 Foreach 迴圈容器](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)。  
  
    > [!NOTE]  
    >  「時序」容器沒有任何自訂編輯器。  
  
5.  如果工作或容器編輯器具有多個節點，請按一下包含您要設定之屬性的節點。  
  
6.  (選擇性) 按一下 [運算式]****，然後在 [運算式]**** 頁面上建立屬性運算式，以動態方式更新工作或容器的屬性。 如需詳細資訊，請參閱[加入或變更屬性運算式](../../integration-services/expressions/add-or-change-a-property-expression.md)。  
  
7.  更新屬性值。  
  
8.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services 容器](../../integration-services/control-flow/integration-services-containers.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
