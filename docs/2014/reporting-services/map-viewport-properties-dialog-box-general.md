---
title: 地圖檢視區屬性對話方塊、 一般 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.general.f1
- "10505"
ms.assetid: 6c9c773e-5c56-4571-95ed-8a157cfdfe52
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 33849743e47ad910fad44938e7537d7b4be8624a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56018180"
---
# <a name="map-viewport-properties-dialog-box-general"></a>地圖檢視區屬性對話方塊、一般
  選取 **[地圖檢視區屬性]** 對話方塊上的 **[一般]** 來變更座標系統、投射以及界限選項。  
  
## <a name="options"></a>選項。  
 **座標系統**  
 指出地圖資料使用之座標系統的類型。  
  
-   **平面** ：當地圖資料使用 X 和 Y 座標 (例如建置規劃) 時，選擇此選項。  
  
-   **地理** ：當地圖資料使用經度和緯度座標 (例如城市位置) 時，選擇此選項。  
  
 **Projection**  
 指定將地理座標投射在二維度介面所使用的方法。 選擇與您要視覺化之資料相容的投射。 受到投射影響的四個空間屬性為區域、形狀、距離與方向。 若是地球檢視，良好的投射選項取決於置中檢視、地圖界限與縮放因數。  
  
 下列每個屬性都會保留其中一個或多個空間屬性：  
  
-   **Equirectangular** ：選擇此選項可以將經度和緯度當做矩形座標使用。  
  
-   **Mercator** ：如果區域較小、赤道周圍扭曲程度較小，或者您想要以使用 Mercator 投射的現有影像分割圖層加入地圖圖層時，選擇這個常用的投射方法。  
  
-   **Robinson** ：如果從赤道跨越兩極的大型區域扭曲程度較少，選擇此選項。 此屬性是由 Arthur H. Robinson 在 1963 年開發。  
  
-   **Fahey** ：如果從赤道跨越兩極的大型區域扭曲程度較少，選擇此選項。 此屬性是由 Lawrence Fahey 在 1975 年開發。  
  
-   **Eckert1** ：使用此選項以便針對緯度使用等距的平行線，並針對經度的經線使用直線。  
  
-   **Eckert3** ：使用此選項以便針對緯度使用等距的平行線，並針對經度的經線使用曲線。  
  
-   **HammerAitoff** ：針對極地地圖或世界地圖使用此選項。  
  
-   **Wagner3** ：針對世界地圖使用此選項。  
  
-   **Bonne** ：選擇此選項可以在世界出現在地圖集時進行檢視。  
  
 **分頁符號選項**  
 選取選項來指示如何將內容納入報表頁面。  
  
 **界限選項**  
 指定座標的下限與上限來控制地圖出現在報表中的部分。  
  
 **最小 X 值**  
 最小的 X 值。 僅適用於 **[平面]** 。  
  
 **最大 X**  
 最大的 X 值。 僅適用於 **[平面]** 。  
  
 **最小 Y 值**  
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
  
  
