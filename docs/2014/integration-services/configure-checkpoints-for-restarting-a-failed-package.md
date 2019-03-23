---
title: 設定檢查點以重新啟動失敗的封裝 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 9afffa5a-d803-4653-8afc-386453fc163f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 220440313f0a06efb4ad55156a41fee18c61ab62
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376676"
---
# <a name="configure-checkpoints-for-restarting-a-failed-package"></a>設定檢查點以重新啟動失敗的封裝
  您可以藉由設定套用到檢查點的屬性，來設定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝，使之從失敗點重新啟動，而不必重新執行整個封裝。  
  
### <a name="to-configure-a-package-to-restart"></a>設定封裝以重新啟動  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含要設定之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 **方案總管**中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  以滑鼠右鍵按一下控制流程設計介面背景的任何位置，然後按一下 [屬性]。  
  
5.  將 SaveCheckpoints 屬性設定為`True`。  
  
6.  在 CheckpointFileName 屬性中輸入檢查點檔案的名稱。  
  
7.  將 CheckpointUsage 屬性設定為下列兩個值的其中一個：  
  
    -   選取 `Always`，將永遠從檢查點重新啟動封裝。  
  
        > [!IMPORTANT]  
        >  如果檢查點檔案不可用，則會產生錯誤。  
  
    -   選取 `IfExists`，只有當檢查點檔案可用時才會重新啟動封裝。  
  
8.  設定封裝可重新啟動的工作和容器。  
  
    -   以滑鼠右鍵按一下工作或容器，然後按一下 [屬性]。  
  
    -   FailPackageOnFailure 屬性設為`True`每個所選工作和容器。  
  
## <a name="see-also"></a>另請參閱  
 [使用檢查點來重新啟動封裝](packages/restart-packages-by-using-checkpoints.md)  
  
  
