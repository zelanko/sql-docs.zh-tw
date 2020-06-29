---
title: 在方案中新增或移除 Integration Services 專案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- Integration Services projects, adding
- SQL Server Integration Services projects, adding
- SSIS projects, adding
- projects [Integration Services], adding
ms.assetid: f01f6475-b63c-41dc-82ac-b62162b3adf7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 29f64f915f241ec274cf4a7babdf9937fe6c4131
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439625"
---
# <a name="add-or-remove-an-integration-services-project-in-a-solution"></a>在方案中加入或移除 Integration Services 專案
  下列程序將描述如何在方案中加入或移除 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
 只有當您可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中看到方案時，才能將專案加入至現有的方案，或從方案中移除專案。 如果您已在中選取 [**永遠顯示方案**] 選項 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 則會顯示方案，即使該方案僅包含一個專案也一樣。 否則，只有當方案包含多個專案時，[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 才會顯示該方案。 其他專案可以是 [!INCLUDE[ssIS](../includes/ssis-md.md)] 專案或其他類型的專案。  
  
## <a name="adding-an-integration-services-project"></a>加入 Integration Services 專案  
 當您加入專案時，可以讓 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 建立全新的空白專案，也可以加入已經針對不同方案建立的專案。 只有當您可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中看到方案時，才能將專案加入至現有的方案。  
  
#### <a name="to-add-a-new-integration-services-project-to-a-solution"></a>將新的 Integration Services 專案加入至方案  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟您要在其中加入新 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案的方案，並執行下列其中之一：  
  
    -   以滑鼠右鍵按一下方案，再按一下 [加入]****，然後按一下 [新增專案]****。  
  
    -   在 [檔案]**** 功能表上，指向 [加入]****，然後按一下 [新增專案]****。  
  
2.  在 [加入新專案]**** 對話方塊中，按一下 [範本]**** 窗格內的 [Integration Services 專案]****。  
  
3.  (選擇性) 編輯專案名稱及位置。  
  
4.  按一下 [確定]****。  
  
#### <a name="to-add-an-existing-integration-services-project-to-a-solution"></a>將現有的 Integration Services 專案加入方案  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟您要在其中加入現有 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案的方案，並執行下列其中之一：  
  
    -   以滑鼠右鍵按一下方案，指向 [加入]****，然後按一下 [現有專案]****。  
  
    -   在 [檔案]**** 功能表上，按一下 [加入]****，然後按一下 [現有專案]****。  
  
2.  在 [加入現有專案]**** 對話方塊中，瀏覽以找出您要加入的專案，然後按一下 [開啟]****。  
  
3.  專案會加入方案總管**** 中的方案資料夾。  
  
## <a name="removing-an-integration-services-project"></a>移除 Integration Services 專案  
 只有當您可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中看到方案時，才能從方案中移除專案。 看見方案之後，您就可以只保留一個專案，並移除其他所有專案。 等到只剩下一個專案之後，[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 就不會再顯示方案資料夾，而且您也不能移除最後一個專案。  
  
#### <a name="to-remove-an-integration-services-project-from-a-solution"></a>從方案中移除 Integration Services 專案  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟您要從中移除 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案的方案。  
  
2.  在方案總管中，以滑鼠右鍵按一下專案，然後按一下 [卸載專案]****。  
  
3.  按一下 [確定]**** 以確認移除。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 專案](integration-services-ssis-projects-and-solutions.md)   
 [建立新的 Integration Services 專案](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
  
