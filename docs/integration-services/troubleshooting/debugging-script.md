---
title: "指令碼偵錯 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Script task [Integration Services], debugging
- debugging [Integration Services], scripts
- scripts [Integration Services], debugging
ms.assetid: fddf57d8-8607-4f88-85a0-1b683087b491
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 338484d5f437833ecdcaffb39ce3b5bc5ec8ea8f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="debugging-script"></a>偵錯指令碼
  您可以撰寫指令碼工作和指令碼元件在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 中使用的指令碼。  
  
 您可以在 VSTA 中設定中斷點和編寫中斷點指令碼。 您可以在 VSTA 中管理中斷點，但您也可以使用「[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」提供的 [設定中斷點] 對話方塊管理中斷點。 如需詳細資訊，請參閱[偵錯控制流程](../../integration-services/troubleshooting/debugging-control-flow.md)。  
  
 [設定中斷點] 對話方塊包含指令碼中斷點。 這些中斷點出現在中斷點清單的底部，並顯示中斷點所在之函數的行號和名稱。 您可以從 [設定中斷點] 對話方塊刪除指令碼中斷點。  
  
 在執行階段，於指令碼中程式碼行上設定的中斷點會與封裝上或封裝的工作和容器上設定的中斷點整合。 偵錯工具可以從指令碼中的中斷點執行到封裝、工作或容器上設定的中斷點，反之亦可。 例如，封裝可能具有以封裝接收到 **OnPreExecute** 和 **OnPostExecute** 事件時發生之中斷條件設定的中斷點，而且封裝還可擁有在其指令碼行上具有中斷點的指令碼工作。 在此案例中，封裝可以暫停與 **OnPreExecute** 事件相關之中斷條件的執行，而執行到指令碼中的中斷點，並最終執行到與 **OnPostExecute** 事件相關的中斷條件。  
  
 如需偵錯指令碼工作和指令碼元件的詳細資訊，請參閱 [指令碼工作的程式碼撰寫和偵錯](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) 和 [指令碼元件的程式碼撰寫和偵錯](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="to-set-a-breakpoint-in-visual-studio-for-applications"></a>在 Visual Studio for Applications 中設定中斷點  
  
-   [在指令碼工作和指令碼元件中設定中斷點來偵錯指令碼](../../integration-services/extending-packages-scripting/debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component.md)  
  
## <a name="see-also"></a>另請參閱  
 [疑難排解封裝開發的工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  

