---
title: 疑難排解圖表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 593e926a20d4c2cb001a6da119f6c39e2dc1fd96
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292148"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>疑難排解圖表 (報表產生器及 SSRS)
  使用圖表時，這些問題很有協助。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>為什麼我的圖表計數不會針對值軸上的值加總？  
 大多數的圖表類型都需要沿著值軸 (通常為 Y 軸) 放置數值，才能正確繪製。 如果值欄位的資料型別是`String`，圖表也無法顯示數值的值，即使欄位中有數字。 但是，圖表會顯示在該欄位中包含值之資料列總數的計數。 若要避免發生這個問題，請確定您用於值數列的欄位具有數值資料類型，而不是包含格式化數字的字串。  
  
## <a name="see-also"></a>另請參閱  
 [圖表&#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
