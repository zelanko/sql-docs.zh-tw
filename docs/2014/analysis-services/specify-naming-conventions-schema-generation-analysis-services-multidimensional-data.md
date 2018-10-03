---
title: 指定命名慣例 （結構描述產生精靈） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.schemagenwizard.namingconventions.f1
ms.assetid: 02d830ea-5b1f-4485-9f94-d64b8bea592b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0cbf9d1e9a26c6a9c64cf93974ae9198a13cbf6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48226248"
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
|**屬性名稱後置詞**|指定字串，用於附加至每一個屬性資料行的名稱後面。 預設值是 **Name**。|  
|**自訂積存後置詞**|指定字串，用於附加至每一個積存資料行的名稱後面。 預設值是 **CustomRollup**。|  
|**自訂積存屬性後置詞**|指定字串，用於附加至每一個積存屬性資料行的名稱後面。 預設值是 **CustomRollupProperties**。|  
|**一元運算子尾碼**|指定字串，用於附加至每一個一元運算子資料行的名稱後面。 預設值是 **UnaryOperator**。|  
  
 **值**  
 針對 [選項] 中所指定的選項指定一個值，亦即您要在產生結構描述時使用的值。  
  
## <a name="see-also"></a>另請參閱  
 [結構描述產生精靈 F1 說明&#40;Analysis Services-多維度資料&#41;](schema-generation-wizard-f1-help-analysis-services-multidimensional-data.md)   
 [Analysis Services 精靈&#40;多維度資料&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
