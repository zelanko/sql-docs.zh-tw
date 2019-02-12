---
title: 疑難排解圖表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7462ae28164ed971298e41624455b7fecac55446
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012489"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>疑難排解圖表 (報表產生器及 SSRS)
  使用圖表時，這些問題很有協助。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>為什麼我的圖表計數不會針對值軸上的值加總？  
 大多數的圖表類型都需要沿著值軸 (通常為 Y 軸) 放置數值，才能正確繪製。 如果值欄位的資料類型為 `String`，即使欄位中有數字，圖表也無法顯示數值。 但是，圖表會顯示在該欄位中包含值之資料列總數的計數。 若要避免發生這個問題，請確定您用於值數列的欄位具有數值資料類型，而不是包含格式化數字的字串。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
