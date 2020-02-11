---
title: 文字方塊 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10134"
- sql12.rtp.rptdesigner.textproperties.general.f1
- "10120"
- sql12.rtp.rptdesigner.textboxproperties.general.f1
ms.assetid: df49e4e3-f279-4c63-a03b-b70c095f4ba2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fb96831c54a67a6ea74ca984cb346dcaaf50a335
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104624"
---
# <a name="text-boxes-report-builder-and-ssrs"></a>文字方塊 (報表產生器及 SSRS)
  當您考慮文字方塊時，可能會考慮包含介面 (如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office PowerPoint) 文字的獨立方塊。 在報表產生器中，有些文字方塊就像那樣，而且這些文字方塊可以根據運算式，顯示標題、描述與標籤或動態文字的常值文字。 但是，資料表或矩陣 (Tablix 資料區) 中的每個資料格也都包含一個文字方塊，這個文字方塊可以使用報表中之獨立文字方塊的相同方式進行格式化。  
  
> [!NOTE]  
>  如果將報表資料集欄位值直接拖曳到報表設計介面，或報表設計介面上的文字方塊，則您在執行報表時，只能看到結果集中的第一個值。 若要查看欄位的所有值，則必須將欄位拖曳到資料表或矩陣中的資料格。 如此一來，當您執行報表時，將會看到該欄位中的所有值。  
  
 若要以自由形式配置顯示重複的文字，請在清單資料區中放置一個文字方塊。 當您想要重複多個值的形式時，請使用清單，例如，客戶發票表單會針對每個客戶重複一次。 如需詳細資訊，請參閱[&#40;報表產生器和 SSRS&#41;清單](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。  
  
 當您想要控制文字方塊配置和最後一個文字方塊下的空白字元時，使用矩形容器。 如需詳細資訊，請參閱[矩形和線條 &#40;報表產生器及 SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md)。  
  
 文字方塊中的運算式可以包含指向資料庫欄位的常值文字，也可以計算資料。 所有運算式都會顯示為預留位置文字，讓您可以格式化數字、色彩和其他外觀屬性。 您也可以在相同的文字方塊中結合預留位置與常值文字。  
  
 您可以在任何單一文字方塊中，使用多個字型、色彩、樣式和動作格式化文字。 如需詳細資訊，請參閱 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)(建立發票和表單的清單)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="GrowShrinkTextBox"></a>增加和縮小文字方塊  
 根據預設，文字方塊是固定的大小。 您可以讓文字方塊根據其內容垂直縮小或擴張。 如需詳細資訊，請參閱 [允許文字方塊擴張或縮小 &#40;報表產生器及 SSRS&#41;](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)(建立發票和表單的清單)。  
  
## <a name="orienting-a-text-box"></a>指定文字方塊的方向  
 指定文字方塊方向可協助您建立更容易閱讀的報表、支援特定地區設定的文字方向、在固定頁面大小的列印報表中容納更多資料行，並以更受觀迎的圖形方式建立報表。 文字方塊可以朝向不同的方向：水平、垂直，或旋轉 270 度。 垂直選項最常用於由上往下書寫的東亞洲語言。 在大部分轉譯器中，垂直選項會處理字符旋轉屬性，以便讓文字由上而下的方向書寫，但字元並不會側躺。 針對其他語言，在垂直和 270 度選項中，文字是側躺的。  
  
 您可以將方向套用至包含常值，來自報表資料集的欄位，或計算的資料等項目的文字方塊。 文字方塊可以在報表主體、資料表或矩陣，或報表首及尾上獨立呈現。  
  
 下圖顯示依月份群組的三種版本資料表報表。 包含月份值的文字方塊使用不同的文字方塊方向。  
  
 ![rs_TextBoxOrientation](../media/rs-textboxorientation.gif "rs_TextBoxOrientation")  
  
 方向是在文字方塊上設定，並套用至方塊中的所有文字。 您無法針對文字方塊的各個部分指定不同的方向。  
  
 若要快速地開始變更文字方向，請參閱[教學課程：將文字格式化 &#40;報表產生器&#41;](../tutorial-format-text-report-builder.md)中的旋轉文字一節。 如需詳細資訊，請參閱[&#40;報表產生器和 SSRS&#41;設定文字方塊方向](set-text-box-orientation-report-builder-and-ssrs.md)。  
  
##  <a name="HowTo"></a> 如何主題  
 [加入、移動或刪除文字方塊 &#40;報表產生器和 SSRS&#41;](add-move-or-delete-a-text-box-report-builder-and-ssrs.md)  
  
 [格式化文字方塊中的文字 &#40;報表產生器及 SSRS&#41;](format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
 [將文字方塊方向設定 &#40;報表產生器和 SSRS&#41;](set-text-box-orientation-report-builder-and-ssrs.md)  
  
 [允許文字方塊擴大或縮小 &#40;報表產生器和 SSRS&#41;](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另請參閱  
 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [格式化數字和日期 &#40;報表產生器及 SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)  
  
  
