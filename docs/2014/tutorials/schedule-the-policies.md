---
title: 排程原則 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63033500"
---
# <a name="schedule-the-policies"></a>排程原則
  在這項工作中，您將會排程匯入至先前工作中的最佳作法原則。  
  
### <a name="to-schedule-the-best-practices-policies"></a>若要排程最佳做法原則  
  
1.  在物件總管中，依序展開 [**管理**]、[**原則管理**] 和 [**原則**]，以滑鼠右鍵按一下最佳作法原則，然後按一下 [**屬性**]。  
  
    > [!NOTE]  
    >  或者，若要輕鬆查看與最佳作法相關聯的原則，以及排序最佳做法分類，請展開 [**管理**]，展開 [**原則管理**]，然後按一下 [**原則**]。 在 [檢視]**** 功能表上，按一下 [物件總管詳細資料]****。 在 [**物件總管詳細資料**] 窗格中，按一下 [**類別**] 標題，依類別目錄來排序原則。 最佳做法原則的前置詞為**Microsoft 的最佳作法**。 以滑鼠右鍵按一下您要設定的原則，然後按一下 [**屬性**]。  
  
2.  在 [**開啟原則**] 對話方塊的 [**一般**] 頁面上，按一下 [**評估模式**] 清單中的 [**排程**]。  
  
3.  在 [**排程**] 方塊旁，按一下 [**挑選**] 指定現有的排程，或按一下 [**新增**] 建立新的排程。  
  
4.  設定排程之後，您可以選取接近頁面頂端的 [**已啟用**] 核取方塊，以啟用排定的原則。  
  
5.  針對您要排程的每個原則重複步驟 1 到步驟 4。  
  
    > [!NOTE]  
    >  若要在已排程的原則執行後檢視評估結果，請開啟目標執行個體上的「原則記錄」記錄檔。 若要開啟記錄檔，請以滑鼠右鍵按一下 [**原則管理**]，然後按一下 [**查看歷程記錄**]。  
  
## <a name="summary"></a>摘要  
 您設定排程的原則針對單一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體執行。 如果您要將排程的原則部署至多個執行個體，請繼續本教學課程中的下一個工作。  
  
## <a name="next-steps"></a>後續步驟  
 [將已排程的原則部署至多個執行個體](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  
