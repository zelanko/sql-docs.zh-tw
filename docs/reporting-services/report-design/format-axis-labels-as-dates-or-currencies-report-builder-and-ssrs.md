---
title: 將軸標籤格式化成日期或貨幣 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: e9a01a74-2f51-4b35-be3a-a6138568f6cf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c8cb54c38710adb381134fc2d443b88e2fea9830
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43266355"
---
# <a name="format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs"></a>將軸標籤格式化成日期或貨幣 (報表產生器及 SSRS)
當您在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分頁報表的座標軸上顯示適當格式化的日期時間值時，圖表會自動將這些值顯示為天。 若要為 X 軸指定日期/時間間隔 (例如月份或小時的間隔)，您必須格式化軸標籤，並將軸間隔的類型設定為有效的日期或時間間隔。  
  
> [!NOTE]  
>  在直條圖與散佈圖中，水平軸 (即 X 軸」) 是類別目錄軸。 而在長條圖中，垂直軸 (即 Y 軸) 是類別目錄軸。  
  
 為了能夠正確格式化時間間隔，X 軸上顯示的值必須評估為 <xref:System.DateTime> 資料類型。 如果您的欄位具有 <xref:System.String>資料類型，圖表不會將間隔計算為日期或時間。 如需詳細資訊，請參閱 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)。  
  
 當數值加入到 Y 軸時，圖表預設不會在顯示數字之前先格式化數字。 如果您的數值欄位是銷售數字，請考慮將數字格式化成貨幣，以增加圖表的可讀性。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-format-x-axis-labels-as-monthly-intervals"></a>將 X 軸標籤格式化成月份間隔  
  
1.  以滑鼠右鍵按一下圖表的水平軸 ( X 軸)，然後選取 [水平軸屬性]。  
  
2.  在 [水平軸屬性] 對話方塊中，選取 [數字]。  
  
3.  從 [類別目錄] 清單中，選取 [日期]。 從 [類型] 清單中，選取要套用到 X 軸標籤的日期格式。  
  
4.  選取 [軸選項]。  
  
5.  在 [間隔] 中，鍵入 **1**。 在 [間隔類型] 屬性中，選取 [月]。  
  
    > [!NOTE]  
    >  如果您未指定間隔類型，圖表將會以日來計算間隔。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-format-y-axis-labels-using-a-currency-format"></a>使用貨幣格式格式化 Y 軸標籤  
  
1.  以滑鼠右鍵按一下圖表的垂直軸 (Y 軸)，然後選取 [垂直軸屬性]。  
  
2.  在 [垂直軸屬性] 對話方塊中，選取 [數字]。  
  
3.  從 [類別目錄] 清單中，選取 [貨幣]。 從 [符號] 清單中，選取要套用到 Y 軸標籤的貨幣格式。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [指定對數刻度 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [指定軸間隔 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  
