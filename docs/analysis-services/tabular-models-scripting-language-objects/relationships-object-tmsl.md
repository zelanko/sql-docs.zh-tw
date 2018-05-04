---
title: 關聯性物件 (TMSL) |Microsoft 文件
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 7588565f-ea34-4402-8be9-331188bdb8c2
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 77fc17b6a92976452b3f94a88aafbb115a3167ed
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="relationships-object-tmsl"></a>關聯性物件 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  定義來源和目標資料表，能夠指定基數，以及查詢和安全性篩選方向之間的關聯性。  
  
## <a name="object-definition"></a>物件定義  
 所有物件都具有一組常用的屬性，包括名稱、 類型、 描述、 屬性集合，以及註解。 **關聯性**物件也有下列屬性。  
  
 isActive  
 布林值，指出是否要將關聯性標記為作用中] 或 [非使用。 使用中的關聯性會自動用於資料表之間的篩選。 非使用中關聯性可搭配 USERELATIONSHIP 函式用於 DAX 計算。  
  
 crossFilteringBehavior  
 表示關聯性如何影響資料的篩選。 請參閱[雙向交叉篩選的 SQL Server 2016 Analysis Services 表格式模型](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)如需詳細資訊。 下列是有效值：  
  
-   為 OneDirection (1)-"To"關聯性的一端在選取的資料列會自動篩選"From"關聯性的端點中的資料表掃描。  
  
-   BothDirections (2)-關聯性任一端點篩選器會自動篩選另一個資料表。  
  
-   自動 (3)-此引擎會分析關聯性，並使用啟發學習法選擇其中一個行為。  
  
 joinOnDateBehavior  
 在聯結兩個日期時間資料行時，指出要聯結日期與時間部分，或只有日期部分。  
  
-   DateAndTime (1)-當聯結兩個日期時間資料行，聯結日期和時間部分。  
  
-   DatePartOnly (2)-當聯結兩個日期時間資料行，聯結只有日期部分。  
  
 relyOnReferentialIntegrity  
 未使用。保留供日後使用。  
  
 securityFilteringBehavior  
 列舉，指出關聯性如何影響資料的篩選評估資料列層級安全性運算式時。 下列是有效值：  
  
-   為 OneDirection (1)-"To"關聯性的一端在選取的資料列會自動篩選"From"關聯性的端點中的資料表掃描。  
  
-   BothDirections (2)-關聯性任一端點篩選器會自動篩選另一個資料表。  
  
## <a name="usage"></a>使用方式  
 關聯性物件中使用[Alter 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)，[建立命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)， [CreateOrReplace 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)，和[Delete 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)。  
  
 建立時，取代或改變關聯性的物件，指定物件定義的所有讀寫屬性。 省略的讀 / 寫屬性會被視為刪除。  
  
## <a name="full-syntax"></a>完整語法  
 以下是關聯性物件的結構描述表示法。  
  
```  
"relationships": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "SingleColumnRelationship object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "isActive": {  
                    "type": "boolean"  
                  },  
                  "type": {  
                    "enum": [  
                      "singleColumn"  
                    ]  
                  },  
                  "crossFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections",  
                      "automatic"  
                    ]  
                  },  
                  "joinOnDateBehavior": {  
                    "enum": [  
                      "dateAndTime",  
                      "datePartOnly"  
                    ]  
                  },  
                  "relyOnReferentialIntegrity": {  
                    "type": "boolean"  
                  },  
                  "securityFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections"  
                    ]  
                  },  
                  "fromCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "toCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "fromColumn": {  
                    "type": "string"  
                  },  
                  "fromTable": {  
                    "type": "string"  
                  },  
                  "toColumn": {  
                    "type": "string"  
                  },  
                  "toTable": {  
                    "type": "string"  
                  },  
                  "annotations": {  
                    "type": "array",  
                    "items": {  
                      "description": "Annotation object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "name": {  
                          "type": "string"  
                        },  
                        "value": {  
                          "anyOf": [  
                            {  
                              "type": "string"  
                            },  
                            {  
                              "type": "array",  
                              "items": {  
                                "type": "string"  
                              }  
                            }  
                          ]  
                        }  
                      },  
                      "additionalProperties": false  
                    }  
                  }  
                },  
                "additionalProperties": false  
              }  
            ]  
          }  
        }  
```  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [建立關聯性](../../integration-services/data-flow/transformations/create-relationships.md)  
  
  
