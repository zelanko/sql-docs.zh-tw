---
title: 設計檢視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.layoutview.f1
helpviewer_keywords:
- Layout View dialog box
ms.assetid: 6fa378aa-442f-4d2f-beab-02a0fb5cd3ce
caps.latest.revision: 37
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: a7f9b00eec64ae93fdb60fa0f7f6e591087d039a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031182"
---
# <a name="design-view"></a>設計檢視
  使用 [設計] 檢視，即可排列報表中的報表項目。 [設計] 檢視有時稱為設計介面或配置檢視。  
  
## <a name="report-design-surface"></a>報表設計介面  
 設計介面由三個區段組成：報表本文、頁首和頁尾。 使用 [工具箱]，即可選取要放入其中任一區段中的項目。 使用 [報表資料] 窗格可檢視影像、參數、資料來源和資料集，包括資料集查詢和欄位清單。 在您將報表項目加入到設計介面之後，請將資料集欄位從 **[報表資料]** 窗格拖曳到資料區，例如資料表、矩陣或清單。 報表設計介面中的每個項目都包含可利用屬性對話方塊或 [屬性] 窗格來管理的屬性。  
  
## <a name="toolbox"></a>工具箱  
 [工具箱] 會列出適用於您報表的資料區域和其他報表項目。 若要從 [工具箱] 加入報表項目，按兩下該項目，或將其拖曳到設計介面上。 接著，您可以使用物件控點來變更形狀和大小。  
  
## <a name="report-data-pane"></a>報表資料窗格  
 若要檢視 [報表資料] 窗格，請按一下 **[檢視]** 功能表上的 **[報表資料]**。 使用此窗格可定義參數、影像、資料來源和資料集，也可參考內建欄位 (例如 ReportName)。 若要加入新項目，按一下 **[新增]** 功能表，然後選取一個項目。 若要將導出欄位加入到現有的資料集，按一下 **[資料集]**，然後在 **[資料集屬性]** 對話方塊中選取 **[欄位]**。 選取一個項目，然後按一下 **[編輯]** 來開啟 **[屬性]** 對話方塊。 您也可以在 [報表資料] 窗格中，以滑鼠右鍵按一下項目來加入項目或更新其屬性。  
  
 將項目從 [報表資料] 窗格拖曳至設計介面上的資料區域和文字方塊，以便將資料和影像加入到報表中。  
  
 如需詳細資訊，請參閱 [Report Data Pane](../report-data/report-data-pane.md)。  
  
## <a name="grouping-pane"></a>群組窗格  
 群組的用途在於將報表資料組織為視覺階層以及計算總計。 使用 [群組] 窗格檢視針對資料表、矩陣或清單資料區域定義的群組。 根據預設，[群組] 窗格會將所選資料區域的所有群組顯示為扁平化清單。 [圖表] 和 [量測計] 資料區域會停用 [群組] 窗格。  
  
 若要查看群組之間的關聯性，請將 [群組] 窗格切換到 [進階] 模式。 這個模式會在對應於每個群組的資料區域中，顯示群組成員的階層、資料格的視覺顯示。  
  
 如需詳細資訊，請參閱＜ [Grouping Pane](grouping-pane.md)＞。  
  
## <a name="page-header-and-page-footer"></a>頁首和頁尾  
 頁首和頁尾可以分別沿著每個頁面的頂端和底部執行。 頁首和頁尾可以包含靜態文字、影像、線條、矩形、框線、背景色彩，以及背景影像。 若要將報表項目加入到頁首或頁尾，以滑鼠右鍵按一下設計介面，然後選取 [頁首] 或 [頁尾]。 頁首和頁尾區段就會出現在設計介面上。  
  
## <a name="properties-pane"></a>屬性窗格  
 使用 [屬性] 窗格可檢視目前在設計介面上選取之報表項目的屬性，或是檢視目前在 [群組] 窗格中選取之群組的屬性。 或者，您也可以用滑鼠右鍵按一下選取的報表項目或群組，然後按一下 [屬性]，為此報表項目或群組開啟對應的 [屬性] 對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [頁首和頁尾&#40;報表產生器和 SSRS&#41;](../report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [報表設計提示 &#40;報表產生器及 SSRS&#41;](../report-design/report-design-tips-report-builder-and-ssrs.md)  
  
  