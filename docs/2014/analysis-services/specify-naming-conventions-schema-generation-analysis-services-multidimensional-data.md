---
title: 指定命名慣例（架構產生 Wizard）（Analysis Services 多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.schemagenwizard.namingconventions.f1
ms.assetid: 02d830ea-5b1f-4485-9f94-d64b8bea592b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b767484af8266b03cf34ebfe4f625fee6c1ca97
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068347"
---
# <a name="specify-naming-conventions-schema-generation-wizard-analysis-services---multidimensional-data"></a>指定命名慣例 (結構描述產生精靈) (Analysis Services - 多維度資料)
  使用 **[指定命名慣例]** 頁面，即可定義結構描述產生精靈建立結構描述物件時使用的命名慣例。  
  
## <a name="options"></a>選項。  
 **選項**  
 指定命名慣例供精靈使用。 下表描述您可以指定的選項。  
  
|選項|描述|  
|------------|-----------------|  
|**分隔符號**|指定字元，用來分隔物件名稱中的單字。 在 **[值]** 資料行中，選取 **[底線]**、 **[空格]** 或 **[無]**。 預設值是 **[底線]**。|  
|**主索引鍵資料行前置詞**|指定字串，作為每一個主索引鍵資料行的名稱前置詞。 預設值是 **PK**。|  
|**外部索引鍵資料行前置詞**|指定字串，作為每一個外部索引鍵資料行的名稱前置詞。 預設值是 **FK**。|  
|**屬性名稱後置詞**|指定字串，用於附加至每一個屬性資料行的名稱後面。 預設值為**Name**。|  
|**自訂積存後置詞**|指定字串，用於附加至每一個積存資料行的名稱後面。 預設值是 **CustomRollup**。|  
|**自訂積存屬性後置詞**|指定字串，用於附加至每一個積存屬性資料行的名稱後面。 預設值是 **CustomRollupProperties**。|  
|**一元運算子後置詞**|指定字串，用於附加至每一個一元運算子資料行的名稱後面。 預設值是 **UnaryOperator**。|  
  
 **ReplTest1**  
 針對 [選項]**** 中所指定的選項指定一個值，亦即您要在產生結構描述時使用的值。  
  
## <a name="see-also"></a>另請參閱  
 [架構產生嚮導 F1 說明 &#40;Analysis Services-多維度資料&#41;](schema-generation-wizard-f1-help-analysis-services-multidimensional-data.md)   
 [Analysis Services 的 &#40;多維度資料的嚮導&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
