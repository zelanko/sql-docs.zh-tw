---
title: "格式化線條、 色彩和影像 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.textboxproperties.border.f1
- "10502"
- "10094"
- sql13.rtp.rptdesigner.shared.borderdv.f1
- sql13.rtp.rptdesigner.reportbody.border.f1
- "10063"
- sql13.rtp.rptdesigner.pictureproperties.border.f1
- sql13.rtp.rptdesigner.rectangleproperties.border.f1
- "10055"
- "10126"
- "10066"
- sql13.rtp.rptdesigner.subreportproperties.border.f1
ms.assetid: 0f5f0d2a-9537-4152-b441-b40d7f04cf4c
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8ba2dbc33b0d61b35fc7bee87b6171016af73279
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="formatting-lines-colors-and-images-report-builder-and-ssrs"></a>格式化線條、色彩和影像 (報表產生器及 SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 讓您能夠格式化線條、色彩、資料區、影像和其他報表項目。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="borders-lines-and-gridlines"></a>框線、線條和格線  
 框線、線條和格線可透過視覺方式將項目一起繫結在頁面上，並協助您的報表讀者輕鬆地閱讀報表的內容。 使用預先定義的框線樣式，可以快速地在一個文字方塊、一組文字方塊或影像的周圍加入框線。 此外，您也可以變更框線、線條和格線的樣式、寬度和色彩。 整個選取的項目周圍或是此項目邊緣框線的周圍會加入框線，例如，文字方塊底部的框線。  
  
 若要格式化文字方塊中、報表配置中或影像周圍的框線和格線，請使用報表項目之 **[屬性]** 對話方塊的 **[框線]** 索引標籤。 例如，如果您想在影像周圍加上框線，請以滑鼠右鍵按一下影像，然後在 **[影像屬性]** 對話方塊中，按一下 **[框線]**。  
  
 除了標準邊框以外，還可以將其他邊框套用到圖表。 如需詳細資訊，請參閱[將邊框加入至圖表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)。  
  
 您也可以在報表本身加上框線。 如需詳細資訊，請參閱 [Add a Border to a Report &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md) (將邊框加入報表 (報表產生器及 SSRS))。  
  
## <a name="applying-background-colors"></a>套用背景色彩  
 純色可以加入至整個報表的背景、報表內的文字方塊，或是加入至資料區內的一個資料格或一組資料格。 依預設，背景色彩為白色，不過您可以從報表項目之 **[屬性]** 對話方塊的 **[填滿]** 索引標籤選取色彩。 例如，如果您想要變更文字方塊的背景色彩，請以滑鼠右鍵按一下此文字方塊，並選取 **[文字方塊屬性]**。 按一下 **[填滿]** ，然後再選取您想要的色彩。 在此對話方塊中，您可以針對選取的項目選取背景色彩，或是加入出現在背景中的影像。  
  
 當您使用圖表時，也可以為背景色彩指定漸層和圖樣樣式。 如需詳細資訊，請參閱 [Formatting a Chart &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md) (格式化圖表 (報表產生器及 SSRS))。  
  
## <a name="using-images-as-formatting"></a>在格式化時使用影像  
 您可以將包含影像的欄位加入至資料區。 如果您使用影像欄位，則影像會在執行報表時顯示於報表中。  
  
 您也可以將標誌之類的影像加入至報表的背景，或是加入到矩形、文字方塊、資料表、矩陣或圖表的某些部分，或者是加入到報表的主體和頁面區段。 如需詳細資訊，請參閱 [Images &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md) (映像 (報表產生器及 SSRS))。  
  
## <a name="see-also"></a>另請參閱  
 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [格式化數字和日期 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [格式化文字方塊中的文字 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)   
 [填滿對話方塊 &#40;報表產生器及 SSRS&#41;](http://msdn.microsoft.com/library/93a91d02-d558-4a0e-8d17-3fdf21e208d3)  
  
  
