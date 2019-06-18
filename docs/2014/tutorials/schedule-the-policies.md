---
title: 排程的原則 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 59417a54-55f1-4468-ba41-368aa852c2d4
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8becd7ad30acf1ea2a63feae4760091aede70c06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033500"
---
# <a name="schedule-the-policies"></a>排程原則
  在這項工作中，您將會排程匯入至先前工作中的最佳作法原則。  
  
### <a name="to-schedule-the-best-practices-policies"></a>若要排程最佳做法原則  
  
1.  在 物件總管 中，展開**管理**，展開**原則管理**，展開**原則**最佳做法原則，以滑鼠右鍵按一下，然後按一下  **屬性**。  
  
    > [!NOTE]  
    >  替代方式，輕鬆地查看哪些原則相關聯的最佳作法，並排序最佳做法類別目錄中，展開**管理**，展開**原則管理**，然後按一下  **原則**。 在 [檢視]  功能表上，按一下 [物件總管詳細資料]  。 在 [**物件總管詳細資料**] 窗格中，按一下**分類**標題，依類別排序的原則。 最佳作法原則有前置詞**Microsoft 最佳作法**。 以滑鼠右鍵按一下您想要設定，然後按一下 原則**屬性**。  
  
2.  在上**一般**頁面**開啟原則**對話方塊中，於**評估模式**清單中，按一下**排程**。  
  
3.  旁**排程**方塊中，按一下**挑選**來指定現有的排程，或按一下 **新增**即可建立新的排程。  
  
4.  您已設定排程之後，您可以選取**已啟用**來啟用排程的原則頁面頂端附近的核取方塊。  
  
5.  針對您要排程的每個原則重複步驟 1 到步驟 4。  
  
    > [!NOTE]  
    >  若要在已排程的原則執行後檢視評估結果，請開啟目標執行個體上的「原則記錄」記錄檔。 若要開啟記錄檔，以滑鼠右鍵按一下**原則管理**，然後按一下**檢視歷程記錄**。  
  
## <a name="summary"></a>總結  
 您設定排程的原則針對單一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體執行。 如果您要將排程的原則部署至多個執行個體，請繼續本教學課程中的下一個工作。  
  
## <a name="next-steps"></a>後續步驟  
 [將已排程的原則部署至多個執行個體](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  
