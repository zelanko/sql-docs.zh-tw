---
title: FORE_COLOR 和 BACK_COLOR 內容（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- FORE_COLOR contents
- backgrounds [MDX]
- cells [MDX]
- colors [MDX]
- storing cell color information
- cell backgrounds
- BACK_COLOR contents
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecd8bb157d7b501d29230c91d87f148ae738ff45
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074404"
---
# <a name="fore_color-and-back_color-contents-mdx"></a>FORE_COLOR 及 BACK_COLOR 內容 (MDX)
  `FORE_COLOR` 及 `BACK_COLOR` 資料格屬性是分別用來以 Microsoft Windows 作業系統的紅-綠-藍 (RGB) 格式，儲存某一資料格的文字與背景的色彩資訊。  
  
 一般 RGB 色彩的有效範圍介於零 (0) 到 16,777,215 (&H00FFFFFF)。 在這個範圍內的數字其高位元永遠等於 0；三個低位元，由最低位元到最高位元，分別決定了紅、綠和藍三種色彩。 紅、綠和藍三種元素分別由 0 到 255 (&HFF) 之間的數字表示。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料格屬性 &#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)  
  
  
