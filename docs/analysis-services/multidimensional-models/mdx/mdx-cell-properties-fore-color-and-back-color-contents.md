---
title: "FORE_COLOR 及 BACK_COLOR 內容 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FORE_COLOR contents
- backgrounds [MDX]
- cells [MDX]
- colors [MDX]
- storing cell color information
- cell backgrounds
- BACK_COLOR contents
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1c39713f66b15fcf959f6ba3887b7002cd7a2863
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-cell-properties---forecolor-and-backcolor-contents"></a>MDX 資料格屬性-FORE_COLOR 及 BACK_COLOR 內容
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]**FORE_COLOR**和**BACK_COLOR**資料格屬性的文字與資料格的背景色彩資訊分別儲存，在 Microsoft Windows 作業系統的紅-綠-藍 (RGB) 格式.  
  
 一般 RGB 色彩的有效範圍介於零 (0) 到 16,777,215 (&H00FFFFFF)。 在這個範圍內的數字其高位元永遠等於 0；三個低位元，由最低位元到最高位元，分別決定了紅、綠和藍三種色彩。 紅、綠和藍三種元素分別由 0 到 255 (&HFF) 之間的數字表示。  
  
## <a name="see-also"></a>請參閱  
 [使用資料格屬性 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)  
  
  
