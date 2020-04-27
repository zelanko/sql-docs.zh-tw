---
title: 偵錯指令碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Script task [Integration Services], debugging
- debugging [Integration Services], scripts
- scripts [Integration Services], debugging
ms.assetid: fddf57d8-8607-4f88-85a0-1b683087b491
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c8eee57be7c7bb9167c24bec117fd2f88a5bb745
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62926329"
---
# <a name="debugging-script"></a>偵錯指令碼
  您可以撰寫指令碼工作和指令碼元件在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 中使用的指令碼。  
  
 您可以在 VSTA 中設定中斷點和編寫中斷點指令碼。 您可以在 VSTA 中管理中斷點，但您也可以使用「 **設計師」提供的 [設定中斷點]** [!INCLUDE[ssIS](../../includes/ssis-md.md)] 對話方塊管理中斷點。 如需詳細資訊，請參閱 [偵錯控制流程](debugging-control-flow.md)。  
  
 [設定中斷點]  對話方塊包含指令碼中斷點。 這些中斷點出現在中斷點清單的底部，並顯示中斷點所在之函數的行號和名稱。 您可以從 [設定中斷點]  對話方塊刪除指令碼中斷點。  
  
 在執行階段，於指令碼中程式碼行上設定的中斷點會與封裝上或封裝的工作和容器上設定的中斷點整合。 偵錯工具可以從指令碼中的中斷點執行到封裝、工作或容器上設定的中斷點，反之亦可。 例如，封裝可能具有以封裝接收到 **OnPreExecute** 和 **OnPostExecute** 事件時發生之中斷條件設定的中斷點，而且封裝還可擁有在其指令碼行上具有中斷點的指令碼工作。 在此案例中，封裝可以暫停與 **OnPreExecute** 事件相關之中斷條件的執行，而執行到指令碼中的中斷點，並最終執行到與 **OnPostExecute** 事件相關的中斷條件。  
  
 如需偵錯指令碼工作和指令碼元件的詳細資訊，請參閱 [指令碼工作的程式碼撰寫和偵錯](../extending-packages-scripting/task/coding-and-debugging-the-script-task.md) 和 [指令碼元件的程式碼撰寫和偵錯](../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="to-set-a-breakpoint-in-visual-studio-for-applications"></a>在 Visual Studio for Applications 中設定中斷點  
  
-   [在指令碼工作和指令碼元件中設定中斷點來對指令碼偵錯](../extending-packages-scripting/debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component.md)  
  
## <a name="see-also"></a>另請參閱  
 [套件開發的疑難排解工具](troubleshooting-tools-for-package-development.md)  
  
  
