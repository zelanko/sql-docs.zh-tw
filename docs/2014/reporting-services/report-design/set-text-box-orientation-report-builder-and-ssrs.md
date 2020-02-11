---
title: 設定文字方塊方向 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 64bd53f4-2f31-4732-8c2e-64c7b54b6972
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6acffc286e913d35846b2eeb156cf1980b42fab3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104982"
---
# <a name="set-text-box-orientation-report-builder-and-ssrs"></a>設定文字方塊方向 (報表產生器及 SSRS)
  文字方塊可以有不同的方向：水平、垂直 (從上到下閱讀文字)，或是旋轉 270 度 (從下到上閱讀文字)。 因為方向會設定在文字方塊而不是文字上，所以方向會套用到文字方塊中的所有文字。 您不能針對文字的各個部分指定不同的方向。 手動調整資料行寬度及資料列高度，以配合旋轉的文字大小。  
  
 您用來指定文字方向的 WritingMode 屬性無法在 [**文字方塊屬性**] 對話方塊中使用。 您需要開啟 [屬性] 窗格，然後在該處設定屬性。 WritingMode 屬性可用的值為**水準**（從左至右的文字讀取）、**垂直**（從上往下閱讀文字）、 **Rotate270** （從上往上閱讀文字）。 您必須手動調整資料行寬度及資料列高度，以便容納文字。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-text-orientation"></a>若要設定文字方向  
  
1.  建立新的報表或開啟現有的報表。  
  
2.  如果 [屬性] 窗格並未開啟，請按一下 **[檢視]** 索引標籤，並選取 **[屬性]** 核取方塊。  
  
3.  按一下您想要變更文字方向的文字方塊。  
  
4.  在 [屬性] 窗格中找出 [WritingMode] 屬性，然後在下拉式清單中選取要套用到文字方塊的文字方向。  
  
    > [!NOTE]  
    >  當 [屬性] 窗格中的屬性組織成類別目錄時，WritingMode 會位於 [當地語系化]  類別目錄中。  
  
5.  在清單方塊中，選取 **[Horizontal]** 、 **[Vertical]** 或 **[Rotate270]** 。  
  
## <a name="see-also"></a>另請參閱  
 [文字方塊 &#40;報表產生器及 SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [教學課程：格式化文字 &#40;報表產生器&#41;](../tutorial-format-text-report-builder.md)  
  
  
