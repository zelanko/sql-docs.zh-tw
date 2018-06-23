---
title: 指定維度索引鍵和類型 （維度精靈） |Microsoft 文件
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
- sql12.asvs.dimensionwizard.dimensionkeyandtype.f1
ms.assetid: d7d5db55-36c3-45f6-ade3-29aa516589c1
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1ce08115251beee6dc71509bc4d3a53420ecd678
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131576"
---
# <a name="specify-dimension-key-and-type-dimension-wizard"></a>指定維度索引鍵和類型 (維度精靈)
  使用 [指定維度索引鍵和類型] 頁面，即可定義維度的索引鍵屬性，並表示維度是否為緩時變維度 (SCD)。  
  
> [!NOTE]  
>  唯有選取了 [選取建立方法] 頁面上的 [Build the dimension without using a data source (不使用資料來源而建立維度)]，以及選取了 [選取維度類型] 頁面上的 [標準維度] 之後，才會顯示此頁面。  
  
## <a name="options"></a>選項。  
 **索引鍵屬性**  
 選取會成為維度之索引鍵屬性的屬性。  
  
> [!NOTE]  
>  如果未針對維度定義任何屬性，此選項唯一可用的值就是 [自動建立索引鍵屬性。] 如果針對維度定義了任何屬性，此值就不可以使用。  
  
 **這是變更維度**  
 選取以表示維度是緩時變維度。 選取此選項會建立其他的資料行和屬性，而這些資料行和屬性可用來長時間追蹤成員在維度階層內的移動。  
  
## <a name="see-also"></a>另請參閱  
 [維度精靈 F1 說明](dimension-wizard-f1-help.md)   
 [維度&#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多維度模型中的維度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  