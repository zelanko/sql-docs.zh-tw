---
title: 資料列可見度對話方塊（報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10126"
ms.assetid: 117fb20c-2fda-437e-bcc5-9010d6d4b53b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d5ad7e47457aa2d1f1d5e36adec7e988de7b8bbb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66102344"
---
# <a name="row-visibility-dialog-box-report-builder"></a>資料列可見性對話方塊 (報表產生器)
  使用 **[資料列可見性]** 對話方塊在報表第一次執行時顯示或隱藏選取的資料列，或使用其他報表項目來切換資料列的可見性。  
  
## <a name="options"></a>選項。  
 **一開始執行報表時**  
 選擇一個選項以指出資料列最初顯示在報表中的方式。  
  
 **顯示**  
 選取此選項，以顯示資料列。  
  
 **隱藏**  
 選取此選項，以隱藏資料列。  
  
 **依據運算式顯示或隱藏**  
 選取此選項即可使用運算式改變初始可見性。  
  
 輸入會評估為 `Boolean` 值的運算式，`True` 會隱藏項目，`False` 會顯示項目。 按一下 [**運算式**] （*fx*）按鈕來編輯運算式。  
  
 **此報表項目可以切換顯示**  
 選擇這個選項可顯示一個切換影像，讓使用者在 HTML 報表檢視器中顯示或隱藏這個資料列。  
  
 輸入或選取您想要顯示切換影像之報表中的文字方塊名稱，例如 Textbox1。 您所選的文字方塊必須位於這個報表項目的目前範圍或涵蓋範圍中。 例如，若要切換與子群組相關之資料列的可見性，請選取與父群組有關之資料列中的文字方塊。 若要切換圖表的可見性，請選取與圖表位於相同涵蓋範圍的文字方塊，例如，報表主體或矩形。  
  
## <a name="see-also"></a>另請參閱  
 [運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [將展開或折迭動作新增至 &#40;報表產生器和 SSRS 的專案&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [&#40;報表產生器和 SSRS&#41;的影像](report-design/images-report-builder-and-ssrs.md)   
 [對話方塊、窗格和嚮導的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [影像屬性對話方塊、一般 &#40;報表產生器及 SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
