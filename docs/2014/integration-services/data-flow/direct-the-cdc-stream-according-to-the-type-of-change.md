---
title: 依據變更類型來導向 CDC 資料流 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3afa531e-f425-40a4-a1bf-1c3e1727287e
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5dcd7b3041decbcaaa95dc0e157cf81d6971105f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37166879"
---
# <a name="direct-the-cdc-stream-according-to-the-type-of-change"></a>依據變更類型來導向 CDC 資料流
  若要加入及設定 CDC 分隔器轉換，封裝至少必須包含一個資料流程工作及一個 CDC 來源。  
  
 加入至封裝的 CDC 來源必須已選取 NetCDC 處理模式。 如需選取處理模式的詳細資訊，請參閱 [CDC 來源編輯器 &#40;連線管理員頁面&#41;](../cdc-source-editor-connection-manager-page.md)。  
  
### <a name="to-direct-the-cdc-stream-according-to-the-type-of-change"></a>若要依據變更類型來導向 CDC 資料流  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝加以開啟。  
  
3.  按一下 **[資料流程]** 索引標籤，然後將 CDC 分隔器從 **[工具箱]** 拖曳到設計介面。  
  
4.  將封裝中包含的 CDC 來源連接到 CDC 分隔器。  
  
5.  將 CDC 分隔器連接到一個或多個目的地。 您最多可以連接到三個不同的輸出。  
  
6.  選取下列其中一個輸出：  
  
    -   刪除輸出：導向 DELETE 變更資料列的輸出。  
  
    -   插入輸出：導向 INSERT 變更資料列的輸出。  
  
    -   更新輸出：導向 UPDATE 前/後變更資料列和合併變更資料列的輸出。  
  
7.  (選擇性) 您可以使用 **[進階編輯器]** 對話方塊來設定進階屬性。  
  
     **[進階編輯器]** 對話方塊包含可以程式設計方式設定的屬性。  
  
     若要開啟 **[進階編輯器]** 對話方塊：  
  
    -   在 **專案的** [資料流程] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 畫面中，以滑鼠右鍵按一下 CDC 分隔器，然後選取 **[顯示進階編輯器]**。  
  
     如需有關使用 CDC 分隔器的詳細資訊，請參閱＜Microsoft SQL Server Integration Services 的 CDC 元件＞。  
  
## <a name="see-also"></a>另請參閱  
 [CDC 分隔器](cdc-splitter.md)  
  
  
