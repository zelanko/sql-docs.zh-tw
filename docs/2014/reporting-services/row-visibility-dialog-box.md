---
title: 資料列可見性對話方塊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.rowvisibility.f1
- "10126"
ms.assetid: 557ecf70-62b1-47f5-9322-0ebdc809d018
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d2fbe61ee783fa0c762cda3fc2a282296d8df04b
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294866"
---
# <a name="row-visibility-dialog-box"></a>資料列可見性對話方塊
  使用 **[資料列可見性]** 對話方塊在報表第一次執行時顯示或隱藏選取的資料列，或使用其他報表項目來切換資料列的可見性。  
  
## <a name="options"></a>選項。  
 **一開始執行報表時**  
 選擇一個選項以指出報表項目最初顯示在報表中的方式。  
  
 **顯示**  
 選取此選項，以顯示報表項目。  
  
 **隱藏**  
 選取此選項，以隱藏報表項目。  
  
 **顯示或隱藏 依據運算式**  
 選取此選項即可使用運算式改變初始可見性。  
  
 輸入會評估為 `Boolean` 值的運算式，`True` 會隱藏項目，`False` 會顯示項目。 請按一下 [運算式]\(**fx**) 按鈕來編輯運算式。  
  
 **此報表項目可以切換顯示**  
 選擇這個選項可顯示一個切換影像，好讓使用者在 HTML 報表檢視器中顯示或隱藏這個報表項目。  
  
 輸入或選取您想要顯示切換影像之報表中的文字方塊名稱，例如 Textbox1。 您所選的文字方塊必須位於這個報表項目的目前範圍或涵蓋範圍中。 例如，若要切換與子群組相關之資料列的可見性，請選取與父群組有關之資料列中的文字方塊。 若要切換圖表的可見性，請選取與圖表位於相同涵蓋範圍的文字方塊，例如，報表主體或矩形。  
  
## <a name="see-also"></a>另請參閱  
 [運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [將展開或摺疊動作新增至項目中 &#40;報表產生器及 SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [影像 &#40;報表產生器及 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [報表設計師 F1 說明](tools/report-designer-f1-help.md)  
  
  
