---
title: 地圖視口屬性對話方塊、一般 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.general.f1
- "10505"
ms.assetid: 6c9c773e-5c56-4571-95ed-8a157cfdfe52
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8ec0aaa051ba317cd05a9784c80fb997f5fa19e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108240"
---
# <a name="map-viewport-properties-dialog-box-general"></a>地圖檢視區屬性對話方塊、一般
  選取 **[地圖檢視區屬性]** 對話方塊上的 **[一般]** 來變更座標系統、投射以及界限選項。  
  
## <a name="options"></a>選項。  
 **座標系統**  
 指出地圖資料使用之座標系統的類型。  
  
-   **平面**當對應資料為 X 和 Y 座標（例如，用於建立計畫）時，請選擇此選項。  
  
-   **地理**當地圖資料為經度和緯度座標（例如，城市位置）時，請選擇此選項。  
  
 **投**  
 指定將地理座標投射在二維度介面所使用的方法。 選擇與您要視覺化之資料相容的投射。 受到投射影響的四個空間屬性為區域、形狀、距離與方向。 若是地球檢視，良好的投射選項取決於置中檢視、地圖界限與縮放因數。  
  
 下列每個屬性都會保留其中一個或多個空間屬性：  
  
-   **Equirectangular:** 選擇此選項，可使用經度和緯度作為矩形座標。  
  
-   **Mercator**請為較小的區域選擇這個熱門投射、減少赤道的失真，或是當您想要加入具有使用 Mercator 投影之現有磚圖層的地圖圖層。  
  
-   **Robinson**請選擇這個選項，以減少從赤道到兩極的大型區域失真。 此屬性是由 Arthur H. Robinson 在 1963 年開發。  
  
-   **Fahey**請選擇這個選項，以減少從赤道到兩極的大型區域失真。 此屬性是由 Lawrence Fahey 在 1975 年開發。  
  
-   **Eckert1:** 請選擇這個選項，以在經度中的緯度和直線使用同樣間距的平行，以進行經線。  
  
-   **Eckert3:** 請選擇這個選項，以在經度中使用與經線相同的間距（緯度和曲線）。  
  
-   **HammerAitoff**針對極座標圖或全球地圖服務，請選擇此選項。  
  
-   **Wagner3:** 針對 [全球地圖]，請選擇此選項。  
  
-   **Bonne:** 請選擇這個選項，以在顯示在塔中的世界來觀看。  
  
 **分頁符號選項**  
 選取選項來指示如何將內容納入報表頁面。  
  
 **界限摘要**  
 指定座標的下限與上限來控制地圖出現在報表中的部分。  
  
 **最小 X**  
 最小的 X 值。 僅適用於 **[平面]** 。  
  
 **最大 X**  
 最大的 X 值。 僅適用於 **[平面]** 。  
  
 **最小 Y**  
 最小的 Y 值。 僅適用於 **[平面]** 。  
  
 **最大 Y**  
 最大的 Y 值。 僅適用於 **[平面]** 。  
  
 **最小經度**  
 最小的經度值。 僅適用於 **[地理]** 。  
  
 **最大經度**  
 最大的經度值。 僅適用於 **[地理]** 。  
  
 **最小緯度**  
 最小的緯度值。 僅適用於 **[地理]** 。  
  
 **最大緯度**  
 最大的緯度值。 僅適用於 **[地理]** 。  
  
## <a name="see-also"></a>另請參閱  
 [地圖 &#40;報表產生器及 SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)  
  
  
