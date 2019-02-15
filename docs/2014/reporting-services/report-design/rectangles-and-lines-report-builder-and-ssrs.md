---
title: 矩形和線條 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d6226b0c-0398-4185-8565-96099876fc21
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 47e8f2e046e919e4b8f292046b99665ea7a012b5
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292986"
---
# <a name="rectangles-and-lines-report-builder-and-ssrs"></a>矩形和線條 (報表產生器及 SSRS)
  矩形和線條可在報表內建立視覺效果。 您可以從 [主資料夾] 索引標籤的 [框線] 區段設定這些報表項目的顯示屬性，而且可以使用 [屬性] 窗格來設定其他屬性。 您可以將背景色彩或影像、工具提示或書籤等功能加入至矩形。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RectanglesLinesReportParts"></a> 矩形和線條做為報表組件  
 您可以將矩形及其包含的項目當做報表組件，與報表分開發行。 [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
 您無法發行矩形內的報表項目做為報表組件。 將矩形加入至報表時，會獲得矩形和其中包含的項目。  
  

  
##  <a name="RectangleAsContainer"></a> 使用矩形做為容器  
 您可以使用矩形做為其他項目的容器。 當您移動矩形時，包含在矩形中的項目會跟著它移動。 矩形內部的項目會以其 **Parent** 屬性顯示矩形的名稱。 如需使用矩形作為容器的詳細資訊，請參閱[新增矩形或容器 &#40;報表產生器及 SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md) 和[在矩陣和圖表上顯示相同的資料 &#40;報表產生器&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)。  
  
> [!NOTE]  
>  矩形只是您可以在矩形中建立或拖曳至矩形之項目的容器。 如果您在已經存在設計介面上的項目周圍繪製矩形，該矩形將不會當做其容器。 該矩形不會列在項目的 Parent 屬性中。  
  
 使用矩形來包含報表項目時，請考慮在報表轉譯時，可能對項目造成的整體影響。 包含重複資料列的報表項目 (例如資料表) 會展開，以容納查詢所傳回的資料，而這會影響矩形中之其他項目的定位。 如果項目放在資料區域之下，資料表會將項目往下推。 若要將項目放在固定位置，可以將報表項目放在一個上邊緣位於資料表下邊緣上方的矩形中。 如需詳細資訊，請參閱[轉譯行為 &#40;報表產生器及 SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)。  
  

  
##  <a name="ReportBorder"></a> 加入報表框線  
 您可以藉由將框線加入頁首、頁尾和報表主體本身來在報表中加入框線，而不必加入線條或矩形。 如需詳細資訊，請參閱 [在報表中加入框線 &#40;報表產生器及 SSRS&#41;](add-a-border-to-a-report-report-builder-and-ssrs.md)。  
  

  
##  <a name="HowTo"></a> 如何主題  
 [在報表中加入框線 &#40;報表產生器及 SSRS&#41;](add-a-border-to-a-report-report-builder-and-ssrs.md)  
  
 [加入矩形或容器 &#40;報表產生器及 SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
 [加入和修改線條 &#40;報表產生器及 SSRS&#41;](add-and-modify-a-line-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另請參閱  
 [加入矩形或容器 &#40;報表產生器及 SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
  
