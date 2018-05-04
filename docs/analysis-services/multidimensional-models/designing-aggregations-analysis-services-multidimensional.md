---
title: 設計彙總 (Analysis Services-多維度) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1dd918940f12391f3b66bd707a81688169035ba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="designing-aggregations-analysis-services---multidimensional"></a>設計彙總 (Analysis Services - 多維度)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  彙總是 Cube 資料的預先計算摘要，可幫助啟用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以提供快速查詢回應。  
  
 若要設定分割區的儲存選項和設計彙總，請使用彙總設計精靈。 此精靈一次操作一個量值群組的單一分割區，因此您可以為每一個分割區選取不同的選項和設計。 此精靈會逐步引導您設定分割區的儲存和設計彙總。 如需設定儲存的詳細資訊，請參閱。  
  
 選取方法來控制精靈要設計的彙總數目，然後讓精靈設計彙總。  
  
 其目標是要設定最佳的彙總數目。 此數目不只要最佳化回應時間，還要防止分割區的大小過大。 彙總數目越大產生的回應時間越快，但也需要更多的儲存空間，而且可能要花更久的時間來計算。 不僅如此，當精靈設計越來越多的彙總時，較早的彙總會比較晚的彙總產生更大的效能改善。 減少較沒有用的彙總也可增加效能。 您可以藉由精靈中可用的下列其中一個方法，來控制精靈設計的彙總數目：  
  
-   指定彙總的儲存空間限制。  
  
-   指定效能改善限制。  
  
-   當顯示的效能對大小曲線開始拉平且是在可接受的效能改善範圍內，請手動停止精靈。  
  
-   選擇不要設計彙總。  
  
 若要設計儲存，精靈必須能夠連接到目標伺服器上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 未執行於目標伺服器上，或儲存體設計處理序無法連接到目標伺服器，則精靈會顯示錯誤訊息。  
  
 精靈的最後步驟可讓您處理或延遲處理。 處理會建立您以精靈設計的彙總，而延遲處理則會儲存所設計的彙總供未來處理，如此可讓設計活動繼續而不進行處理。 視分割區的大小而定，處理可能需要花費很多時間。 您可以選擇中斷處理分割區。  
  
## <a name="see-also"></a>另請參閱  
 [彙總和彙總設計](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
