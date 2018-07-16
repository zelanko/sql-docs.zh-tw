---
title: 針對工作或容器設定中斷點以偵錯封裝 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], breakpoints
- breakpoints [Integration Services]
- tasks [Integration Services], breakpoints
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
caps.latest.revision: 33
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b063089105af1de7656387be8cc12639498e7c37
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308108"
---
# <a name="debug-a-package-by-setting-breakpoints-on-a-task-or-a-container"></a>針對工作或容器設定中斷點以偵錯封裝
  此程序描述如何在封裝、工作、「For 迴圈」容器、「Foreach 迴圈」容器或「時序」容器中設定中斷點。  
  
### <a name="to-set-breakpoints-in-a-package-a-task-or-a-container"></a>若要在封裝、工作或容器中設定中斷點  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  按兩下要在其中設定中斷點的封裝。  
  
3.  在 [SSIS 設計師] 中，執行下列動作：  
  
    -   若要在封裝物件中設定中斷點，請按一下 [控制流程] 索引標籤，並將資料指標置於設計介面背景上的任意位置，再以滑鼠右鍵按一下，然後按一下 [編輯中斷點]。  
  
    -   若要在封裝控制流程中設定中斷點，請按一下 [控制流程] 索引標籤，並以滑鼠右鍵按一下工作、「For 迴圈」容器、「Foreach 迴圈」容器或「時序」容器，然後按一下 [編輯中斷點]。  
  
    -   若要在事件處理常式中設定中斷點，請按一下 [事件處理常式] 索引標籤，並以滑鼠右鍵按一下工作、「For 迴圈」容器、「Foreach 迴圈」容器或「時序」容器，然後按一下 [編輯中斷點]。  
  
4.  在 [設定中斷點 \<容器名稱>] 對話方塊中，選取要啟用的中斷點。  
  
5.  選擇性地修改每個中斷點的叫用計數類型和叫用計數數目。  
  
6.  若要儲存封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
## <a name="see-also"></a>另請參閱  
 [疑難排解封裝開發的工具](troubleshooting/troubleshooting-tools-for-package-development.md)   
 [在指令碼工作和指令碼元件中設定中斷點，偵錯指令碼](data-flow/transformations/script-component.md)   
 [編碼和偵錯指令碼工作](control-flow/script-task.md)   
 [編碼和偵錯指令碼元件](extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
