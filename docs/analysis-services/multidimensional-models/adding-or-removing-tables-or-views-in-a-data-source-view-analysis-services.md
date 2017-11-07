---
title: "新增或移除資料表或檢視表中的資料來源檢視 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.dsvdesigner.tablespane.f1
helpviewer_keywords:
- deleting tables
- tables [Analysis Services]
- removing tables
- adding tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 98307d04-6548-4d7d-9244-2371dd165249
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b2f865766530f174cc3affe410679f1880e9813
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services"></a>在資料來源檢視中加入或移除資料表或檢視 (Analysis Services)
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中建立資料來源檢視 (DSV) 之後，即可在資料來源檢視設計工具中，透過加入或移除資料表和資料行 (包括其他資料來源中的資料表和資料行) 來進行修改。  
  
 若要在資料來源檢視設計工具中開啟 DSV，請在 [方案總管] 中按兩下 DSV。 開啟 DSV 之後，即可使用按鈕列或功能表上的 [加入/移除資料表] 命令，修改或擴充 DSV。 您也可以使用圖表中的物件。 例如，您可以選取物件，然後使用鍵盤上的 Delete 鍵移除物件。  
  
> [!WARNING]  
>  移除資料表時請格外小心。 移除資料表會從 DSV 中刪除所有相關聯的資料行和關聯性，並使繫結至該資料表的所有物件失效。  
  
## <a name="selecting-tables-or-views-to-add-or-remove"></a>選取要加入或移除的資料表或檢視表  
 您可以使用 [加入/移除資料表] 對話方塊，在 [可用的物件] 和 [包含的物件] 清單之間移動資料表或檢視表。 [可用的物件] 清單一開始會包含主要資料來源中尚未出現在資料來源檢視中的任何資料表或檢視表。 如果主要資料來源支援 **OPENROWSET** 函數，您也可以在專案或資料庫中加入來自其他資料來源的資料表或檢視表。  
  
 在 DSV 中加入或移除資料表，也會在 DSV 中目前所選取的圖表內加入或移除資料表。 如需圖表的詳細資訊，請參閱 [在資料來源檢視設計工具中使用圖表 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)。  
  
 將資料表移到 [加入/移除資料表] 對話方塊中的 [包含的物件] 清單之後，您還可以加入所有相關資料表。 此作業會根據資料來源中的外部索引鍵條件約束來加入資料表 (如果有這樣的條件約束存在的話)。 如果外部索引鍵條件約束不存在，您可以使用資料來源檢視的 **NameMatchingCriteria** 屬性來決定關聯性，做法是指定用來比對資料表中之資料行名稱的準則來產生可能的關聯性。 如果針對資料來源檢視指定了 **NameMatchingCriteria** 屬性，請按一下 [加入相關資料表] 來加入資料來源中有相符之資料行名稱的資料表。 如需設定 **NameMatchingCriteria** 屬性的詳細資訊，請參閱[多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
> [!NOTE]  
>  在資料來源檢視中加入或移除物件不會影響基礎資料來源。  
  
## <a name="see-also"></a>請參閱＜  
 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [在資料來源檢視設計工具中使用圖表 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  

