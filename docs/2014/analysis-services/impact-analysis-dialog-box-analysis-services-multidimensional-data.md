---
title: 影響分析對話方塊 (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.process.impactanalysisdialog.f1
ms.assetid: 208268eb-4e14-44db-9c64-6f74b776adb6
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: da3a687a637dee6b3b9df59eecebf957f06e64be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022024"
---
# <a name="impact-analysis-dialog-box-analysis-services---multidimensional-data"></a>影響分析對話方塊 (Analysis Services - 多維度資料)
  如果 **[處理]** 對話方塊中所列出的物件已經處理，請使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 **[影響分析]** 對話方塊來識別及選擇性地處理受影響的相依物件。 在 **[處理]** 對話方塊中按一下 **[影響分析]** ，即可顯示 **[影響分析]** 對話方塊。  
  
> [!NOTE]  
>  如果物件受到一個以上的影響，物件就會出現一次以上。  
  
## <a name="options"></a>選項。  
 **物件清單**  
 在方格中顯示相依性物件的清單。 方格包含下列資料行：  
  
 **Object Name**  
 顯示可能需要處理之相依性物件的名稱。 名稱左邊的圖示會指出物件類型。  
  
 **型別**  
 顯示可能需要處理之相依性物件的類型。  
  
 **影響型別**  
 顯示處理 [處理] 對話方塊中的物件時，會對相依物件造成的影響。 下表列出可能的處理效果，並註解每一個處理的結果是會導致警告或錯誤。  
  
|影響|訊息|  
|------------|-------------|  
|將清除物件 (取消處理)|警告|  
|物件將失效|錯誤|  
|將捨棄彙總|警告|  
|將捨棄彈性彙總|警告|  
|將捨棄索引|警告|  
|將處理非子物件|警告|  
  
 **處理序的物件**  
 選取您要進行處理作業的相依性物件。 完成處理作業之後，必須處理未選取的相依性物件。 否則它們將無法使用。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [處理對話方塊&#40;Analysis Services-多維度資料&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  