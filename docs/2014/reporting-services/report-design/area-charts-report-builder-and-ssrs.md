---
title: 區域圖 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 245b236d-1d55-4744-b752-80bd133502aa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f8970e77cf6ab77dc5dd4cc0544237d6a1269db2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185832"
---
# <a name="area-charts-report-builder-and-ssrs"></a>區域圖 (報表產生器及 SSRS)
  區域圖會將數列顯示成一組用線條連接的點，線條下會有一個全部填滿的區域。 如需如何將資料加入區域圖的詳細資訊，請參閱 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)。  
  
 下圖顯示堆疊區域圖的範例。 此資料非常適合在堆疊區域圖上顯示，因為此圖表可以顯示所有數列的總計，以及每個數列對於總計所佔據的比例。  
  
 ![區域圖](../media/areachart.gif "區域圖")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>變數  
  
-   **堆疊區域**： 將多個數列垂直堆疊的區域圖。 如果您的圖表中只有一個數列，堆疊區域圖的顯示將與區域圖相同。  
  
-   **百分比堆疊區域**： 將多個數列垂直堆疊以便符合整個圖表區域的區域圖。 如果您的圖表中只有一個數列，堆疊區域圖的顯示將與區域圖相同。  
  
-   **平滑區域圖**： 一種區域圖，其中的資料點是以平滑線相連，而非以一般線條相連。 當您比較注重顯示趨勢，而非顯示各個資料點的值時，請使用平滑區域圖，而非區域圖。  
  
## <a name="data-considerations-for-area-charts"></a>區域圖的資料考量  
  
-   除了折線圖之外，區域圖是連續顯示資料的唯一圖表類型。 因此，區域圖通常用於表示發生超過一段連續時間的資料。  
  
-   百分比堆疊區域圖適用於顯示發生超過一段時間的成比例資料。  
  
-   如果只有一個數列，堆疊區域圖的外觀將與區域圖相同。  
  
-   在一般區域圖中，如果多個數列的值相似，這些區域可能會重疊，而遮蓋到重要資料點的值。 您可以將圖表類型變更為堆疊區域圖 (其設計為顯示區域圖的多個數列) 來解決這個問題。  
  
-   如果您的堆疊區域圖包含間隙，您的資料集可能包含空值，這些值在堆疊區域圖上會顯示為空的區段。 如果您的資料集包含空值，請考慮在圖表上插入空的點。 加入空的點將會在圖表上，以不同的色彩填滿空的區域來表示 Null 或零值。 如需詳細資訊，請參閱 <<c0> [ 新增空白點至圖表&#40;報表產生器及 SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)。</c0>  
  
-   區域圖類型在行為上非常類似於直條圖與折線圖。 如果您要在多個數列間進行比較，請考慮改用直條圖。 如果您要分析一段時間的趨勢，則考慮使用折線圖。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [圖表類型 &#40;報表產生器及 SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [折線圖 &#40;報表產生器及 SSRS&#41;](line-charts-report-builder-and-ssrs.md)   
 [變更圖表類型 &#40;報表產生器及 SSRS&#41;](change-a-chart-type-report-builder-and-ssrs.md)   
 [圖表中的空白和 Null 資料點 &#40;報表產生器及 SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
