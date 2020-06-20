---
title: 在指令碼工作和指令碼元件中設定中斷點來偵錯指令碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3a05344f1fc20e575566d0a0fa527ac64b32363f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968396"
---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>在指令碼工作和指令碼元件中設定中斷點來偵錯指令碼
  此程序描述如何在用於指令碼工作和指令碼元件的指令碼中設定中斷點。  
  
 在腳本中設定中斷點之後，[**設定中斷點- \<object name> ** ] 對話方塊會列出中斷點，以及內建的中斷點。  
  
> [!IMPORTANT]  
>  在某些情況下，會忽略指令碼工作和指令碼元件的中斷點。 如需詳細資訊，請參閱撰寫腳本工作的程式碼和偵錯工具中**的腳本工作一節** [，以及 [](../control-flow/script-task.md)編碼和偵測腳本元件] （. 中的**腳本元件**一節。/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md.  
  
### <a name="to-set-a-breakpoint-in-script"></a>在指令碼中設定中斷點  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  按兩下內含要在其中設定中斷點之指令碼的封裝。  
  
3.  若要開啟指令碼工作，請按一下 [控制流程]  索引標籤，然後按兩下指令碼工作。  
  
4.  若要開啟指令碼元件，請按一下 [資料流程]  索引標籤，然後按兩下指令碼元件。  
  
5.  按一下 [指令碼]  ，然後按一下 [編輯指令碼]  。  
  
6.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 中，找出要在其上設定中斷點的指令碼行，以滑鼠右鍵按一下該行，並指向 [中斷點]  ，然後按一下 [插入中斷點]  。  
  
     中斷點圖示隨即出現在程式碼行上。  
  
7.  在 **[檔案]** 功能表上按一下 **[結束]** 。  
  
8.  按一下 [確定]  。  
  
9. 若要儲存封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
  
