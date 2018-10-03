---
title: 設定文字方塊方向 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 64bd53f4-2f31-4732-8c2e-64c7b54b6972
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 1e5639e83d3d0abcb9999d03ea0ce954c8824556
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119578"
---
# <a name="set-text-box-orientation-report-builder-and-ssrs"></a>設定文字方塊方向 (報表產生器及 SSRS)
  文字方塊可以有不同的方向：水平、垂直 (從上到下閱讀文字)，或是旋轉 270 度 (從下到上閱讀文字)。 因為方向會設定在文字方塊而不是文字上，所以方向會套用到文字方塊中的所有文字。 您不能針對文字的各個部分指定不同的方向。 手動調整資料行寬度及資料列高度，以配合旋轉的文字大小。  
  
 WritingMode 屬性，用來指定文字方向，不適用於**文字方塊內容** 對話方塊。 您需要開啟 [屬性] 窗格，然後在該處設定屬性。 WritingMode 屬性可用的值為**水平**（閱讀文字由左到右），**垂直**（往下的閱讀文字，） **Rotate270** （閱讀文字由下至上）。 您必須手動調整資料行寬度及資料列高度，以便容納文字。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-text-orientation"></a>若要設定文字方向  
  
1.  建立新的報表或開啟現有的報表。  
  
2.  如果 [屬性] 窗格並未開啟，請按一下 **[檢視]** 索引標籤，並選取 **[屬性]** 核取方塊。  
  
3.  按一下您想要變更文字方向的文字方塊。  
  
4.  找出的 WritingMode 屬性，在 [屬性] 窗格中，並在下拉式清單中選取要套用到文字方塊中的文字方向。  
  
    > [!NOTE]  
    >  當 [屬性] 窗格中的屬性組織成類別目錄時，WritingMode 會位於 [當地語系化] 類別目錄中。  
  
5.  在清單方塊中，選取 **[Horizontal]**、 **[Vertical]** 或 **[Rotate270]**。  
  
## <a name="see-also"></a>另請參閱  
 [文字方塊&#40;報表產生器及 SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [教學課程：格式化文字 &#40;報表產生器&#41;](../tutorial-format-text-report-builder.md)  
  
  
