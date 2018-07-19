---
title: FORE_COLOR 及 BACK_COLOR 內容 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
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
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a4909413bb7847d4254020ed2b4135049baaea4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278225"
---
# <a name="forecolor-and-backcolor-contents-mdx"></a>FORE_COLOR 及 BACK_COLOR 內容 (MDX)
  `FORE_COLOR` 及 `BACK_COLOR` 資料格屬性是分別用來以 Microsoft Windows 作業系統的紅-綠-藍 (RGB) 格式，儲存某一資料格的文字與背景的色彩資訊。  
  
 一般 RGB 色彩的有效範圍介於零 (0) 到 16,777,215 (&H00FFFFFF)。 在這個範圍內的數字其高位元永遠等於 0；三個低位元，由最低位元到最高位元，分別決定了紅、綠和藍三種色彩。 紅、綠和藍三種元素分別由 0 到 255 (&HFF) 之間的數字表示。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料格屬性&#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)  
  
  
