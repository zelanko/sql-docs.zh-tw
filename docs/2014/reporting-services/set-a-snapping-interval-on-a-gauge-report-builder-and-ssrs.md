---
title: 設定量測計的貼齊間隔（報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0ece7297-6e2f-47fb-835d-b9e9cce53fe2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3e2a35e4d6fefb6830774ffd7b2c3bc13a5e097c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101371"
---
# <a name="set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs"></a>設定量測計的貼齊間隔 (報表產生器及 SSRS)
  貼齊間隔會定義捨入值的倍數。 根據預設，量測計將指向您在資料窗格中指定之欄位的確切值。 不過，您可能會想要向上或向下捨入確切值，以便讓指標貼齊預設的間隔。 例如，如果量測計的值為 34.2，而且您將貼齊間隔指定為 5，則量測計指標將會指向 35。 如果量測計的值為 31.2，而且您將貼齊間隔指定為 5，則量測計指標將會指向 30。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-snapping-interval-on-a-gauge"></a>設定量測計的貼齊間隔  
  
1.  按一下量測計數字的任何位置，以便反白顯示標尺。  
  
2.  開啟 [屬性] 窗格。  
  
    > [!NOTE]  
    >  如果看不到 [屬性] 窗格，請按一下 [**視圖**] 索引標籤，然後選取 [**屬性**] 核取方塊。  
  
3.  在 [**指標**] 屬性中，按一下（...）按鈕。 指標集合編輯器隨即開啟。  
  
4.  將**SnappingEnabled**屬性設定為`True`。  
  
5.  將**SnappingInterval**設定為代表貼齊間隔的值。 此指標將貼齊您已指定之值的最接近捨入倍數。  
  
## <a name="see-also"></a>另請參閱  
 [格式化量測計上的標尺 &#40;報表產生器及 SSRS&#41;](report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [格式化量測計上的指標 &#40;報表產生器及 SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [量測計 &#40;報表產生器及 SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
