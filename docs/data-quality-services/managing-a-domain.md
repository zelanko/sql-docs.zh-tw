---
title: 管理定義域 | Microsoft Docs
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
ms.assetid: c5ab71a3-0dac-45b1-be8e-93bf7e0e03ce
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e988d58dc4f160ae85273762173d129c2cc9c2c
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="managing-a-domain"></a>管理定義域
  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中使用定義域。 定義域包含要分析之資料來源中特定欄位內之資料的語意表示法。 定義域是您為資料來源建立之知識庫的一部分，而且您藉由分析取樣資料來源或匯入資料所建立的知識會加入至知識庫中所定義的定義域。 之後會使用這些定義域中的知識，於資料品質專案中執行清理和比對。 定義域位於 Data Quality Services 中所有活動的核心。  
  
 定義域會對應至資料來源欄位，而且會在知識探索、定義域管理和比對活動中擴展。 定義域屬性中會定義要如何從資料來源及報表中的輸出資料載入資料。 當您使用參考資料提供者來清理資料時，您會將參考資料服務附加至單一或複合定義域。 您會在定義域中建立要套用至資料的規則，而且您可以為定義域建立以詞彙為主的關聯。 您可以檢視及更正定義域中的資料。  
  
 您也可以建立由兩個或多個個別定義域所組成的複合定義域，其中每一個定義域都包含有關一般資料的知識。 如需詳細資訊，請參閱[管理複合定義域](../data-quality-services/managing-a-composite-domain.md)。  
  
## <a name="domain-properties"></a>定義域屬性  
 當您建立定義域時，您可以選擇以下方式從來源資料擴展定義域以及輸出定義域值。 如需詳細資訊，請參閱[設定定義域屬性](../data-quality-services/set-domain-properties.md)。  
  
-   選取您要用來擴展定義域的資料類型。 如需有關每種定義域資料類型所支援之資料類型的詳細資訊，請參閱＜ [DQS 定義域支援的 SQL Server 和 SSIS 資料類型](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md)＞。  
  
-   指定只有前置值 (而非其同義字) 將會是定義域中的輸出。  
  
-   根據資料類型指定定義域值應該是某種格式的輸出。  
  
-   如果資料類型是字串，從資料來源將此字串載入定義域時，您可以移除特殊字元來將此字串標準化。  
  
-   如果資料類型是字串，您可以執行 DQS 拼字檢查來檢查字串的語法、拼字和句子結構，並在 **[定義域管理]** 的 **[定義域值]**頁面中指示任何潛在錯誤。 其中包括指定執行拼字檢查所使用的語言。  
  
-   如果資料類型是字串，當您知道語法錯誤不會出現在字串中時，您可以指定 DQS 不會識別語法錯誤。  
  
## <a name="in-this-section"></a>本節內容  
 使用定義域可讓您執行以下作業：  
  
|||  
|-|-|  
|針對具有特定資料類型的資料欄位建立語意表示法、指定如何擴展定義域，以及設定定義域輸出的格式|[建立網域](../data-quality-services/create-a-domain.md)|  
|將定義域連結到另一個定義域，讓它共用相同的設定與值|[建立連結的網域](../data-quality-services/create-a-linked-domain.md)|  
|將參考資料服務附加至單一或複合定義域|[將網域或複合網域附加至參考資料](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|變更或增加知識庫中的值|[變更網域值](../data-quality-services/change-domain-values.md)|  
|使用驗證和標準化規則|[建立網域規則](../data-quality-services/create-a-domain-rule.md)|  
|使用關聯來更正屬於定義域值之一部分的詞彙|[建立以詞彙為主的關聯](../data-quality-services/create-term-based-relations.md)|  
|完成、關閉或取消定義域管理活動|[結束定義域管理活動](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)|  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|藉由執行知識探索以及以互動方式管理知識來建立知識庫|[建置知識庫](../data-quality-services/building-a-knowledge-base.md)|  
|將知識匯入知識庫或是從知識庫匯出知識。|[匯入和匯出知識](../data-quality-services/importing-and-exporting-knowledge.md)|  
|建立複合定義域，並將知識加入至定義域。|[管理複合網域](../data-quality-services/managing-a-composite-domain.md)|  
  
  
