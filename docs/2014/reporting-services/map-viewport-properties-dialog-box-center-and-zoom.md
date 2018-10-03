---
title: 地圖檢視區屬性對話方塊、 置中與縮放 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.centerandzoom.f1
- "10506"
ms.assetid: 642a06f5-293f-48e0-97a6-1489dbefa719
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 205471b262ae041858db72c5db8d9c603eb716b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072028"
---
# <a name="map-viewport-properties-dialog-box-center-and-zoom"></a>地圖檢視區屬性對話方塊、置中與縮放
  選取 **[地圖檢視區屬性]** 對話方塊的 **[置中與縮放]** 來設定地圖的置中檢視與縮放因數。 指定地圖資料來源與您要包含在報表中之報表的界限之後，您可以指定檢視置中與縮放因數來進一步控制地圖顯示。 根據您用來指定置中與縮放值的方法，選項可能有所不同。 按一下 **[運算式]** (*fx*) 按鈕來編輯設定選項值的運算式。  
  
## <a name="options"></a>選項。  
 **設定檢視置中與縮放層級**  
 選擇此選項來指定檢視置中與縮放層級的自訂值。  
  
 **地圖置中以顯示地圖圖層**  
 選擇此選項來指定圖層，並自動將檢視在其地圖資料上置中。 例如，將檢視在 LineLayer1 上置中。  
  
 **地圖置中以顯示內嵌的地圖元素**  
 選擇此選項，將檢視在特定的資料繫結地圖元素上置中。 空間資料與分析資料必須擁有關聯性，才能指定此選項。  
  
 例如，將檢視在符合欄位名稱為 [City] 而符合值為 "Seattle" 的地圖元素上置中。  
  
 **地圖置中以顯示所有資料繫結地圖元素**  
 選擇此選項，將檢視在圖層中的所有地圖元素上置中。 空間資料與分析資料必須擁有關聯性，才能指定此選項。  
  
 例如，將檢視在顯示城市和泡泡大小與人口有關的多邊形泡泡圖層上置中。 計算檢視區的中心時，只會包含人口值相符的城市。  
  
 **置中與縮放選項**  
 選取一個選項來指定檢視置中與縮放層級。  
  
 **檢視置中 (X) %**  
 水平座標。 預設值 50%。 表示將檢視在最小與最大水平值之間的中點上置中。  
  
 **檢視置中 (Y) %**  
 垂直座標。 預設值 50% 表示將檢視在最小與最大垂直值之間的中點上置中。  
  
 **縮放層級 （%）**  
 縮放因數。 預設值 100% 表示無縮放比例。  
  
 **此圖層上置中檢視**  
 指定圖層的名稱。  
  
 **在符合此條件的地圖元素上置中檢視**  
 顯示的唯讀欄位用於比對地圖資料和分析資料。 指定您要比對時所依據的值。 檢視會自動在此地圖元素上置中。 例如，NAME = TEXAS。 根據預設，條件的資料類型為字串，而且比對時會區分大小寫。  
  
 若要針對包含不同資料類型的欄位進行比對，您必須撰寫評估為該資料類型的運算式。 例如，如果符合欄位為儲存為整數的 5 位數郵遞區號，則您必須使用運算式 =98053 來指定郵遞區號 98053。  
  
## <a name="see-also"></a>另請參閱  
 [地圖 &#40;報表產生器及 SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)  
  
  
