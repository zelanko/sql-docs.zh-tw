---
title: "指令碼工作和指令碼元件中設定中斷點來偵錯指令碼 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96815b337311c4ba8d16e10c25891c728e7a0c74
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>在指令碼工作和指令碼元件中設定中斷點來偵錯指令碼
  此程序描述如何在用於指令碼工作和指令碼元件的指令碼中設定中斷點。  
  
 您的指令碼中設定中斷點後**設定中斷點的\<物件名稱 >**對話方塊會列出中斷點與內建的中斷點。  
  
> [!IMPORTANT]  
>  在某些情況下，會忽略指令碼工作和指令碼元件的中斷點。 如需詳細資訊，請參閱**偵錯指令碼工作**一節中[編碼和偵錯指令碼工作](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)和**偵錯指令碼元件**一節中[編碼和偵錯指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="to-set-a-breakpoint-in-script"></a>在指令碼中設定中斷點  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  按兩下內含要在其中設定中斷點之指令碼的封裝。  
  
3.  若要開啟指令碼工作，請按一下**控制流程**索引標籤，然後再按兩下 指令碼工作。  
  
4.  若要開啟指令碼元件，請按一下**資料流程**索引標籤，然後再按兩下 指令碼元件。  
  
5.  按一下**指令碼**，然後按一下 **編輯指令碼**。  
  
6.  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)，找出您想要設定中斷點，請以滑鼠右鍵按一下該行，指向指令碼的行**中斷點**，然後按一下 **插入中斷點**。  
  
     中斷點圖示隨即出現在程式碼行上。  
  
7.  在 **[檔案]** 功能表上按一下 **[結束]**。  
  
8.  按一下 **[確定]**。  
  
9. 若要儲存封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
  
