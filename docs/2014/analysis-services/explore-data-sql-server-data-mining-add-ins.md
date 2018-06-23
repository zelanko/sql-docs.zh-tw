---
title: 瀏覽資料 （SQL Server 資料採礦增益集） |Microsoft 文件
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data preparation
- histogram [data mining]
- data visualization
ms.assetid: 714845a9-4c27-461a-9ba3-149e1e818386
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c648fba4cf47f117eb5dd04b76b5d7f0cb4f17c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033793"
---
# <a name="explore-data-sql-server-data-mining-add-ins"></a>瀏覽資料 (SQL Server 資料採礦增益集)
  ![瀏覽資料精靈](media/dmc-explore.gif "瀏覽資料精靈")  
  
 **瀏覽資料**精靈可協助您了解類型和您的資料表中的資料量。 此精靈會一次繪製一個選定資料行的分佈和值。 然後，您可以試驗變更資料的分組方式，或是將顯示內容的圖表複製到 Excel 活頁簿進行檢閱。  
  
 如果您的資料包含連續數值資料，您可以在下列兩種檢視之間切換：  
  
-   **線條圖。** 這種圖表會在 X 軸繪製資料值，在 Y 軸繪製案例數目。  
  
-   **橫條圖。** 這種圖形會依每個值的案例數目來分組值。  
  
 當精靈尋找資料的群組時，它會使用資料值的實際分佈。 因此，橫條圖不會顯示常見的整數值座標軸標記 (例如 10 或 100)。 而是，橫條圖中顯示的範圍可能比較類似於 43521-55603 ([收入] 資料行)。  
  
 如果您要將資料分組成其他範圍，就應該先在 Excel 中進行這項處理，然後再分析資料。 或重定資料標籤使用[重定標籤](relabel-sql-server-data-mining-add-ins.md)精靈。  
  
## <a name="using-the-explore-data-wizard"></a>使用瀏覽資料精靈  
  
1.  在**資料採礦**功能區中，按一下 **瀏覽資料**。  
  
2.  在**選取來源**對話方塊方塊中，選取資料表或資料格範圍，其中包含您的資料。  
  
3.  在**選取資料行**對話方塊方塊中，選擇要分析，請從範例資料 窗格中顯示的資料行。  
  
4.  在**瀏覽資料**對話方塊方塊中，選擇顯示資料分佈的圖表類型。  
  
5.  您可以選擇將新資料行加入資料、變更資料分割的方式，或是將圖表複製到 Excel。  
  
### <a name="requirements"></a>需求  
 若要使用**瀏覽資料**精靈，您的資料必須在 Excel 資料表中。   
  
## <a name="see-also"></a>另請參閱  
 [資料採礦準備清單](checklist-of-preparation-for-data-mining.md)  
  
  