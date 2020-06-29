---
title: 緩時變維度資料行 (緩時變維度精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6283887cbddb9844e0ac769281184f588dc2a94d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430255"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>緩時變維度資料行 (緩時變維度精靈)
  使用 **[緩時變維度資料行]** 對話方塊，以選取每個緩時變維度資料行的變更類型。  
  
 若要深入了解這個精靈，請參閱＜ [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **維度資料行**  
 從清單中選取維度資料行。  
  
 **變更類型**  
 選取 [固定屬性]  ，或選取兩種變更屬性類型的其中之一。 資料行中的值不會變更時，請使用 **[固定屬性]** ； [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 會將變更視為錯誤。 使用 **[變更屬性]** 以變更的值覆寫現有的值。 使用 **[記錄屬性]** 在新記錄中儲存變更的值，同時將先前的記錄標示為過期。  
  
 **移除**  
 選取維度資料行，並按一下 [移除]  從對應資料行清單中將其移除。  
  
## <a name="see-also"></a>另請參閱  
 [使用緩時變維度精靈來設定輸出](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
