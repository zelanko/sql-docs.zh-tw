---
title: 緩時變維度資料行 (緩時變維度精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fb87a00ded7034696f45b2855f5f931ef44eadfa
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290294"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>緩時變維度資料行 (緩時變維度精靈)
  使用 **[緩時變維度資料行]** 對話方塊，以選取每個緩時變維度資料行的變更類型。  
  
 若要深入了解這個精靈，請參閱＜ [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **維度資料行**  
 從清單中選取維度資料行。  
  
 **變更類型**  
 選取 [固定屬性]，或選取兩種變更屬性類型的其中之一。 資料行中的值不會變更時，請使用 **[固定屬性]** ； [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 會將變更視為錯誤。 使用 **[變更屬性]** 以變更的值覆寫現有的值。 使用 **[記錄屬性]** 在新記錄中儲存變更的值，同時將先前的記錄標示為過期。  
  
 **移除**  
 選取維度資料行，並按一下 [移除] 從對應資料行清單中將其移除。  
  
## <a name="see-also"></a>另請參閱  
 [使用緩時變維度精靈來設定輸出](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
