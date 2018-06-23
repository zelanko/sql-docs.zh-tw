---
title: 將框線新增至報表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81412f94-2991-4e58-bc05-5ccc0cbf2a75
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 4295a712f277047c4e205d83c44bbc0ff444db32
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144882"
---
# <a name="add-a-border-to-a-report-report-builder-and-ssrs"></a>在報表中加入框線 (報表產生器及 SSRS)
  您可以藉由將框線加入頁首、頁尾和報表主體本身來在報表中加入框線，而不必加入線條或矩形。  
  
 如果加入了出現在頁首和頁尾的報表框線，不要抑制報表第一頁和最後一頁的頁首及頁尾。 如果抑制顯示，則報表第一頁和最後一頁之上方或下方的框線將被切斷。 如需詳細資訊，請參閱[頁首和頁尾 &#40;報表產生器及 SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-border-to-a-report"></a>在報表中加入框線  
  
1.  在頁首內以滑鼠右鍵按一下任何項目的外部，然後按一下 [頁首屬性]。 以您所要的樣式，在 **[框線]** 索引標籤上加入左框線、上框線和右框線。  
  
    > [!NOTE]  
    >  如果您不要在報表中使用頁首，您可以將放在報表主體周圍，框線或您可以加入標頭從**插入** 索引標籤。  
  
2.  在設計介面上以滑鼠右鍵按一下主體內任何項目的外部，然後按一下 [主體屬性]。 以您所要的樣式，在 **[框線]** 索引標籤上加入左框線和右框線。  
  
3.  在頁尾內以滑鼠右鍵按一下任何項目的外部，然後按一下 [頁尾屬性]。 以您所要的樣式，在 **[框線]** 索引標籤上加入左框線、下框線和右框線。  
  
## <a name="see-also"></a>另請參閱  
 [矩形和線條&#40;報表產生器和 SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md)  
  
  