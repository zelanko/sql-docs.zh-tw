---
title: 地圖色彩規則對話方塊、 一般 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10541"
- sql12.rtp.rptdesigner.shared.mapcolorrulesgeneral.f1
ms.assetid: 14ff5fc1-4cf8-4a45-9d98-47a1bf1c52c4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e97de85cdd57fdb21aa82379243eb6954358ea38
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108314"
---
# <a name="map-color-rules-dialog-box-general"></a>地圖色彩規則對話方塊、一般
  選取 **[色彩規則屬性]** 對話方塊上的 **[一般]** ，定義此圖層上地圖元素的色彩選項。 地圖元素包括多邊形、線條與點。 當您已經根據資料集欄位或空間資料來源欄位中的空間資料與分析資料建立地圖元素之間的關聯性時，可以套用色彩規則。  
  
 若要在圖層上指定包含不同主要色彩與次要色彩的裝飾漸層來顯示所有地圖元素，請使用 [地圖多邊形屬性] 對話方塊的 **[填滿]** 頁面。 色彩規則優先於圖層的顯示屬性。 如需詳細資訊，請參閱[自訂地圖或地圖圖層的資料和顯示 &#40;報表產生器及 SSRS&#41;](report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>選項。  
 **套用範本樣式**  
 選取此選項可以根據您在精靈中選擇的主題，或在多邊形、線條或點圖層屬性中設定的主題，使用色彩。 主題會為地圖設定色彩、字型與框線的預設選項。 若是此選項，不會套用任何規則來指派色彩給每個地圖元素。  
  
 **使用調色盤將資料視覺化**  
 選取此選項可以透過使用特定色彩調色盤中的色彩來視覺化分析資料。  
  
 **使用色彩範圍將資料視覺化**  
 選取此選項可以透過每個地圖元素使用一個範圍的色彩來視覺化分析資料。 例如，當您指定 [紅色] 做為開始色彩、[黃色] 做為中間色彩，而 [綠色] 做為結束色彩時，下限範圍中的值為 [紅色]、中間範圍中的值為 [黃色]，而上限範圍中的值為 [綠色]。  
  
 **使用自訂色彩將資料視覺化**  
 選取此選項可以透過指定您自己的色彩清單來視覺化分析資料。  
  
 **資料欄位**  
 當您選取其中一個 **[將資料視覺化]** 選項時，會出現此選項。  
  
 從下拉式清單中選取要使用的分析資料欄位。 根據空間資料的來源，此清單會顯示空間資料來源與報表資料集 (擁有空間資料與分析資料之間的關聯性) 中的欄位。 若要建立此種關聯性，請針對選取的地圖圖層，在 [分析資料] 頁面上設定資料選項。  
  
 **Palette**  
 輸入或選取色彩調色盤的名稱。  
  
 **開始色彩**  
 指定用於資料範圍下限之資料的色彩。  
  
 **中間色彩**  
 指定用於資料範圍中間之資料的色彩。 選取 **[無色彩]** 即可移除此範圍。  
  
 **結束色彩**  
 指定用於資料範圍上限之資料的色彩。  
  
 **[加入]**  
 按一下 **[加入]** ，針對色彩規則指定您自己的色彩。  
  
## <a name="see-also"></a>另請參閱  
 [地圖 &#40;報表產生器及 SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)   
 [變更地圖圖例、色階與相關的規則 &#40;報表產生器及 SSRS&#41;](report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)  
  
  
