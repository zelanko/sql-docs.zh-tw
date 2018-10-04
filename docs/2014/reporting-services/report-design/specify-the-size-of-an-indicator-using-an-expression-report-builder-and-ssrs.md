---
title: 使用運算式指定指標的大小 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ab0b86f1-4882-4258-a2b6-c612faecfa4b
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5a7cd9ee7026dbc662d381a76ad66be2dbbb61d6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206248"
---
# <a name="specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs"></a>使用運算式指定指標的大小 (報表產生器及 SSRS)
  除了色彩、方向和形狀之外，您還可以使用大小，將指標的視覺影像最大化。  
  
 指標包含一個名稱為 IndicatorStates 的指標狀態集合。 IndicatorStates 集合通常有多個狀態。 每個狀態都是集合的成員，而且會以一個圖示表示。 這些所有狀態就構成 IndicatorsStates 集合。  
  
 若要動態設定圖示的大小，您要在報表產生器的 [屬性] 窗格中設定 IndicatorsStates 集合的成員屬性。 如果看不到 **[屬性]** 窗格，按一下 **[檢視]** 索引標籤，然後選取 **[屬性]**。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，您可以使用 **[屬性]** 視窗來設定成員屬性。 如果 **[屬性]** 視窗未開啟，請按下 F4 鍵。  
  
 [屬性] 窗格可存取指標之 IndicatorStates 集合的屬性。 您可以使用運算式設定 IndicatorStates 集合成員的 ScaleFactor 屬性，以便將圖示設定為不同的大小。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。  
  
 在此程序所用的運算式也用來產生不同大小的指標，顯示的報表[指標&#40;報表產生器及 SSRS&#41;](indicators-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-the-indicator-icon-size-using-an-expression"></a>若要使用運算式指定指標圖示大小  
  
1.  按一下您想要變更的指標。  
  
2.  在 [屬性] 窗格中，找出 IndicatorStates 屬性。  
  
     如果 [屬性] 窗格是依類別目錄排列，您將會在 [狀態] 類別目錄中找到 IndicatorStates。  
  
3.  按一下 IndicatorStates 旁的省略符號 **(...)** 按鈕。 **[IndicatorState 集合編輯器]** 對話方塊隨即開啟。  
  
     選取集合的所有成員。  
  
4.  在 [複選屬性] 清單中，按一下 ScaleFactor 旁的向下箭頭，然後按一下 [運算式]。  
  
5.  在 **[運算式]** 對話方塊中，撰寫運算式。  
  
     下列範例運算式會根據 **SalesYTD** 欄位的值，將圖示變成不同的大小。  
  
     `=IIF(Fields!SalesYTD.value = 0,0,Fields!SalesYTD.value/Max(Fields!SalesYTD.value,"Indicator"))`  
  
     如需詳細資訊，請參閱[運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [指標 &#40;報表產生器及 SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  
