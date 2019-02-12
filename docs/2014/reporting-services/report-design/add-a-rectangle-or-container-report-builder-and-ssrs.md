---
title: 新增矩形或容器 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10061"
- sql12.rtp.rptdesigner.rectangleproperties.general.f1
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 21bf1d94f179f9c48fb3b00f06d98cec105c9f27
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017209"
---
# <a name="add-a-rectangle-or-container-report-builder-and-ssrs"></a>加入矩形或容器 (報表產生器及 SSRS)
  當您希望使用圖形元素來區隔報表的區域、強調報表的區域或是提供一個或多個報表項目的背景時，請將矩形加入至報表中。 矩形也可當做容器使用，有助於控制資料區在報表中的轉譯方式。 您可以自訂矩形的外觀，其方式是編輯矩形屬性 (如背景色彩和框線色彩)。 如需使用矩形作為容器的詳細資訊，請參閱[矩形和線條 &#40;報表產生器及 SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md) 和[在矩陣和圖表上顯示相同的資料 &#40;報表產生器&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-rectangle"></a>若要加入矩形  
  
1.  在 [插入] 索引標籤的 [報表項目] 群組中，按一下 [矩形]。  
  
2.  在設計介面上，按一下您要放置矩形左上角的位置，然後拖曳到您要放置圖表右下角的位置。  
  
     請注意，當您移動游標時，只要游標與設計介面上的其他物件對齊，就會出現「對齊線」。 這些線條能協助您對齊物件。  
  
### <a name="to-create-a-container"></a>建立容器  
  
1.  將矩形報表項目加入至報表。  
  
2.  將其他報表項目拖曳至矩形中。  
  
    > [!NOTE]  
    >  矩形只是您可以在矩形中建立或拖曳至矩形之項目的容器。 如果您在已經存在設計介面上的項目周圍繪製矩形，該矩形將不會當做其容器。  
  
### <a name="to-change-rectangle-properties-such-as-color-style-or-weight"></a>若要變更色彩、樣式或粗細等矩形屬性  
  
1.  選取矩形，然後在 [主資料夾] 索引標籤的 [框線] 區段中，按一下線條色彩、樣式或粗細選項。  
  
2.  按一下 [框線] 按鈕旁的箭號，以便決定要變更矩形的哪一面。  
  
    > [!NOTE]  
    >  如果您將線條樣式設定為**Double**和線條的寬度為 1 1/2 pt 或更窄，線條可能不會出現雙線當您在報表產生器、 報表設計師或報表管理員中，會在執行報表時。 當您將報表匯出為其他格式時才會出現雙線，例如 Microsoft Word 及 Acrobat PDF。  
  
## <a name="see-also"></a>另請參閱  
 [矩形和線條 &#40;報表產生器及 SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)  
  
  
