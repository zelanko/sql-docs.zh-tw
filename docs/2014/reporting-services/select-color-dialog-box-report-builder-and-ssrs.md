---
title: 選取色彩對話方塊 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.selectcolor.f1
- "10090"
helpviewer_keywords:
- Select Color dialog box
ms.assetid: ac7089a3-5c7b-4f53-8348-180610e86da2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 882f7ba5aed75aec20d656c5ca49da66625ec6e6
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56293106"
---
# <a name="select-color-dialog-box-report-builder-and-ssrs"></a>選取色彩對話方塊 (報表產生器及 SSRS)
  使用 **Select Color** 對話方塊，可以指定資料區或文字方塊內，單一資料格或多個資料格的背景色彩選項或圖表色彩選項。  
  
## <a name="options"></a>選項。  
 **色彩選取器**  
 從指定如何選取色彩的三個選項選擇。  
  
-   **選擇器 - 色彩圓形** ：使用「色調/飽和/亮度」(HSB) 色彩值來選擇色彩。  
  
-   **選擇器 - 色彩方塊** ：使用「紅色/綠色/藍色」(RGB) 色彩值來選擇色彩。  
  
-   **調色盤 - 標準色彩** ：從預先定義的色彩值清單選擇色彩。  
  
 **色彩圓形**  
 用於 HSB 色彩，因為 HSB 值會對應到圓柱座標系統。 色調是實際的色彩、飽和度是色彩的純度，而亮度是相對亮度或暗度。  
  
 挑選色彩時，圓形的中心會決定色彩。 使用色彩滑動軸來變更色調。 X 和 Y 座標分別表示飽和度和亮度的值。  
  
 **色彩正方形**  
 用於 RGB 色彩，因為 RGB 值會對應到笛卡兒 (Cartesian) 座標系統。 R 的值代表紅色、G 的值代表綠色，而 B 的值則代表藍色。  
  
 挑選色彩時，正方形的中心會決定色彩。 使用色彩滑動軸來變更所選色彩的範圍。 X 和 Y 座標代表其他兩種色彩。 例如，如果您挑選綠色，滑動軸會顯示綠色值的範圍，而 X 和 Y 座標則分別代表紅色和藍色值。  
  
 **標準的調色盤色彩**  
 用於命名色彩[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]`KnownColor`列舉型別。  
  
 **色彩系統**  
 指定 RGB 或 HSB 色彩。 此選項會將顯示變更為顯示 RGB 或 HSB 值，這些值會在您將色彩圓形或色彩正方形用於 **[色彩選取器]** 時，以互動方式更新。  
  
 如果色彩可以包含透明值，系統會針對某些屬性顯示 **Alpha** 值。 例如，圖表數列填滿。 對於不支援透明的屬性，系統會停用這個值。  
  
 **紅色**  
 RGB 色彩紅色部分的十進位值。 使用微調方塊來變更值，或輸入一個介於 0 和 255 之間的值。  
  
 **綠色**  
 RGB 色彩綠色部分的十進位值。 使用微調方塊來變更值，或輸入一個介於 0 和 255 之間的值。  
  
 **藍色**  
 RGB 色彩藍色部分的十進位值。 使用微調方塊來變更值，或輸入一個介於 0 和 255 之間的值。  
  
 **Alpha**  
 色彩 α 或透明部分的十進位值。 啟用這個值時，您可以使用滑動軸參數來調整您需要的透明程度。  
  
 **色調**  
 HSB 色彩色調的十進位值。 使用微調方塊來變更值，或輸入一個介於 0 和 255 之間的值。  
  
 **飽和度**  
 HSB 色彩飽和度的十進位值。 使用微調方塊來變更值，或輸入一個介於 0 和 255 之間的值。  
  
 **亮度**  
 HSB 色彩亮度的十進位值。 使用微調方塊來變更值，或輸入一個介於 0 和 255 之間的值。  
  
 **色彩範例**  
 在窗格的左半部顯示目前的色彩，並在窗格的右半部以互動方式顯示您所選擇的新色彩。 如果沒有預設色彩，窗格的左半部為白色。 大部分的 RDL 屬性都沒有預設色彩。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表項目的格式 &#40;報表產生器及 SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)  
  
  
