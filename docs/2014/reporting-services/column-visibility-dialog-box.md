---
title: 資料行可見性對話方塊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.columnvisibility.f1
- "10127"
ms.assetid: ca59d1cd-d782-4298-aa61-4f312c32eb50
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bf9f11b8b56333dba7c0d2a5066712017ea194cb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215258"
---
# <a name="column-visibility-dialog-box"></a>資料行可見性對話方塊
  使用 **[資料行可見性]** 對話方塊在報表第一次執行時顯示或隱藏選取的資料行，或使用其他報表項目來切換資料行的可見性。  
  
## <a name="options"></a>選項。  
 **一開始執行報表時**  
 選擇一個選項以指出報表項目最初顯示在報表中的方式。  
  
 **顯示**  
 選擇此選項，以顯示報表項目。  
  
 **隱藏**  
 選擇此選項，以隱藏報表項目。  
  
 **顯示或隱藏 依據運算式**  
 選擇此選項即可使用運算式改變初始可見性。  
  
 輸入要評估的運算式`Boolean`的值`True`隱藏項目和`False`顯示項目。 請按一下 [運算式]\(*fx*) 按鈕來編輯運算式。  
  
 **此報表項目可以切換顯示**  
 選擇這個選項可顯示一個切換影像，好讓使用者在 HTML 報表檢視器中顯示或隱藏這個報表項目。  
  
 輸入或選取您想要顯示切換影像之報表中的文字方塊名稱，例如 Textbox1。 您所選的文字方塊必須位於這個報表項目的目前範圍或涵蓋範圍中。 例如，若要切換與子群組相關之資料列的可見性，請選取與父群組有關之資料列中的文字方塊。 若要切換圖表的可見性，請選取與圖表位於相同涵蓋範圍的文字方塊，例如，報表主體或矩形。  
  
## <a name="see-also"></a>另請參閱  
 [運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [將展開或摺疊動作新增至項目中 &#40;報表產生器及 SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [映像&#40;報表產生器及 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [報表設計師 F1 說明](tools/report-designer-f1-help.md)  
  
  
