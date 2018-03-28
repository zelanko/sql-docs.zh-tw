---
title: 管理複合定義域 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2012
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 47821eff-800b-4053-8d36-e42bbc267f54
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67a253241fff3c1391fba522d6b3b659d03272bb
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="managing-a-composite-domain"></a>管理複合定義域
  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中使用複合定義域。 有時單一定義域無法滿意地表示欄位中的資料，您只能透過群組單一定義域來表示該資料。 若要這樣做，請建立複合定義域。 複合定義域是由兩個或多個單一定義域所組成，而且會對應至由多個相關詞彙所組成的資料欄位，這些詞彙未經過剖析，但是包含在單一複合值中。 此值中的每一個詞彙將由不同的單一定義域表示。 一旦您將單一定義域併入複合定義域，然後將複合定義域對應至資料欄位之後，您就可以藉由在單一定義域中建立知識，於知識庫中建立有關該欄位中之資料的知識。 複合定義域就像單一定義域一樣，都是單一資料欄位中資料的語意表示法。  
  
 複合定義域中的單一定義域必須擁有共同知識領域。 範例如下：擁有街道、縣市、州/省、國家/地區和郵遞區號資料的地址欄位。 此欄位中的不同詞彙可能會有不同的資料類型。 若要處理這種情況，請將這些詞彙對應到不同的單一定義域。 另一個範例如下：擁有名字、中間名和姓氏資料的完整名稱欄位。 若要使用複合定義域，您必須能夠將此欄位中的資料剖析成不同的單一定義域，為此欄位建立複合定義域，並為此欄位的一部分建立單一定義域。  
  
 複合定義域的功能與單一定義域不同。 您無法變更複合定義域中的值，而必須在單一定義域中變更。 有了複合定義域，您就可以使用跨定義域規則來測試複合定義域之單一定義域的值。 您也可以檢視在複合定義域中所找到的值組合。  
  
## <a name="in-this-section"></a>本節內容  
 使用複合定義域可讓您執行以下作業：  
  
|||  
|-|-|  
|針對包含多個未剖析之相關詞彙的資料欄位建立語意表示法|[建立複合網域](../data-quality-services/create-a-composite-domain.md)|  
|當您將複雜資料對應至複合定義域時，除了針對分隔符號進行剖析之外，您也可以根據知識來剖析資料。 DQS 會先嘗試使用它對於單一定義域的知識，以判斷複雜字串的部分如何屬於單一定義域。|[建立複合網域](../data-quality-services/create-a-composite-domain.md)|  
|將參考資料服務 (例如處理地址資料的服務) 加入至複合定義域。|[將網域或複合網域附加至參考資料](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|當複合定義域中一個定義域的值影響另一個定義域的值時，請建立跨定義域規則。|[建立跨網域規則](../data-quality-services/create-a-cross-domain-rule.md)|  
|識別值組合，好讓 DQS 可以報告其頻率。|[使用複合網域中的值關聯](../data-quality-services/use-value-relations-in-a-composite-domain.md)|  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|藉由執行知識探索以及以互動方式管理知識來建立知識庫|[建置知識庫](../data-quality-services/building-a-knowledge-base.md)|  
|將知識匯入知識庫或是從知識庫匯出知識。|[匯入和匯出知識](../data-quality-services/importing-and-exporting-knowledge.md)|  
|建立單一定義域，並將知識加入至定義域。|[管理網域](../data-quality-services/managing-a-domain.md)|  
  
  
