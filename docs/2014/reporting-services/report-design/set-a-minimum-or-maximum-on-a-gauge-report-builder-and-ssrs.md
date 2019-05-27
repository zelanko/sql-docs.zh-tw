---
title: 設定最小值或最大值為量測計 （報表產生器及 SSRS） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b4c260c0-5a88-4f30-8977-eb5cc78fc146
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c7a9ad23124105443349720d2d5769fb9227db2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105032"
---
# <a name="set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs"></a>設定量測計的最小值或最大值 (報表產生器及 SSRS)
  與定義多個群組的圖表不同的是，量測計只會顯示一個值。 由於報表產生器和報表設計師會判斷您嘗試在量測計上顯示之單一值的內容或相對重要性，所以您必須定義標尺的最小值和最大值。 例如，如果您的資料值為介於 0 和 10 之間的排名，就會想要將最小值設定為 0 而將最大值設定為 10。 系統會根據您針對最小值和最大值指定的值，自動計算間隔數字。 根據預設，最小值和最大值會設定為 0 和 100，但這是您應該變更的任意值。 應用程式不會將您的值計算成百分比。  
  
 如果值的範圍很大 (例如從 0 到 10000)，請考慮使用乘數來減少量測計上零的數目。 此乘數只會減少量測計上數字的標尺，而非值本身。  
  
 您可以使用運算式來設定 [最小值] 和 [最大值] 選項的值。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-the-minimum-and-maximum-on-the-gauge"></a>設定量測計的最小值和最大值  
  
1.  以滑鼠右鍵按一下標尺，然後選取 [標尺屬性]。 [標尺屬性] 對話方塊隨即顯示。  
  
2.  在 [一般] 中，指定 [最小值] 的值。 根據預設，這個值為 0。 您可以選擇按一下 [運算式]\(*fx*) 按鈕來編輯設定選項值的運算式。  
  
3.  指定 [最大值] 的值。 根據預設，此值為 100。 您可以選擇按一下 [運算式]\(*fx*) 按鈕來編輯設定選項值的運算式。  
  
4.  (選擇性) 如果最小值和最大值的值很大，請指定 [標尺標籤乘數] 選項的值。 若要指定減少標尺的乘數，請使用十進位數字。 例如，如果您的標尺為從 0 到 1000，就可以指定乘數值 0.01 來減少標尺，以便顯示成 0 到 10。  
  
## <a name="see-also"></a>另請參閱  
 [格式化量測計上的標尺 &#40;報表產生器及 SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [格式化量測計上的指標 &#40;報表產生器及 SSRS&#41;](formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [量測計 &#40;報表產生器及 SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
