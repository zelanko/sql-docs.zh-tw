---
title: 資料分割物件 (TMSL) |Microsoft 文件
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: df1da0d2-d824-42ba-b9dc-47fbd8edc10f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bc820929603cadb400bd19f3afa4d04a6222fb89
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="partitions-object-tmsl"></a>資料分割物件 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  定義資料分割或資料表資料列集的邏輯分割。 資料分割是由 SQL 查詢，用來匯入資料，範例資料在模型化環境中，或做為完整的資料查詢，透過 DirectQuery 透過查詢執行階段所組成。  
  
 磁碟分割上的屬性會決定資料來源資料表的方式。  在物件階層中，資料分割的父物件是資料表物件。  
  
## <a name="object-definition"></a>物件定義  
 所有物件都具有一組常用的屬性，包括名稱、 類型、 描述、 屬性集合，以及註解。 **資料分割**物件也有下列屬性。  
  
 型別  
 磁碟分割類型。 有效的值為數值，並包括下列各項：  
  
-   擷取查詢 (1) – 此分割區中的資料是執行針對查詢**DataSource**。 **DataSource**必須 model.bim 檔案中定義為資料來源。  
  
-   計算 (2) – 執行計算的運算式會填入此資料分割中的資料。  
  
-   無 (3) – 此分割區中的資料會填入發送至伺服器的資料列集的資料重新整理作業的一部分。  
  
 mode  
 定義資料分割的查詢模式。 有效值為**匯入**， **DirectQuery**，或**預設**（繼承）。 這是必要的值。  
  
|||  
|-|-|  
|**匯入**|表示要求針對儲存匯入的資料的記憶體中分析引擎發出的查詢。|  
|**DirectQuery**|傳遞至外部關聯式資料庫的查詢執行。 DirectQuery 模式會使用資料分割來提供模型設計期間使用的範例資料。 部署在實際伺服器上，則應該切換回完整資料檢視。 前文提過，DirectQuery 模式需要一個磁碟分割，每個資料表，且每個模型的一個資料來源。|  
|**default**|如果您想要切換模式高的層級物件樹狀目錄中，在模型或資料庫層級，請將此選項。 當您選擇預設值時，查詢模式會匯入或 DirectQuery。|  
  
 來源  
 識別要查詢之資料的位置。 有效值為**查詢中，計算**，或**無**。 這是必要的值。  
  
|||  
|-|-|  
|**無**|用於匯入模式，已經載入及儲存在記憶體中資料。|  
|**查詢**|若為 DirectQuery 模式中，則針對模型中所指定的關聯式資料庫執行 SQL 查詢**DataSource**。 請參閱[資料來源物件&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)。|  
|**計算**|導出的資料表的來源資料表建立時指定的運算式。 這個運算式會被視為，建立導出資料表的資料分割的來源。|  
  
 dataview  
 對於 DirectQuery 資料分割，進一步其他 dataView 屬性會指定是否擷取資料的查詢是範例還是完整資料集。 有效值為**完整**，**範例**，或**預設**（繼承）。 如前所述，範本會用只在資料模型和測試。 請參閱[將範例資料加入 DirectQuery 模型中設計模式](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)如需詳細資訊。  
  
## <a name="usage"></a>使用方式  
 會使用資料分割物件[Alter 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)，[建立命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)， [CreateOrReplace 命令&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)， [delete 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)，[重新整理命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)，和[MergePartitions 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 建立時，取代或改變分割區的物件，指定物件定義的所有讀寫屬性。 省略的讀 / 寫屬性會被視為刪除。 讀寫屬性包括名稱、 描述、 模式和來源。  
  
## <a name="examples"></a>範例  
 **範例 1** -簡單的資料分割資料表的結構 （而不是事實資料表）。  
  
```  
"partitions": [  
          {  
            "name": "Customer",  
            "source": {  
              "query": "SELECT [dbo].[Customer].* FROM [dbo].[Customer]",  
              "dataSource": "SqlServer localhost FoodmartDB"  
            }  
]  
```  
  
 **範例 2** -分割事實資料通常根據 WHERE 子句，從相同的資料表建立資料的非重疊資料分割。  
  
```  
"partitions": [  
          {  
            "name": "sales_fact_2015",  
            "source": {  
              "query": "SELECT [dbo].[sales_fact_2015].* FROM [dbo].[sales_fact_2015] WHERE [dbo].[sales_fact_2015].[Quarter]=4",                                                                                          
              "dataSource": "SqlServer localhost FoodmartDB"  
            },  
          }  
        ]  
```  
  
 **範例 3** -DAX 運算式為基礎的導出的資料表。  
  
```  
"partitions": [  
          {  
            "name": "CalcTable1",  
            "source": {  
              "type": "calculated",  
              "expression": "'Product Class'"  
            },  
            }  
]  
```  
  
## <a name="full-syntax"></a>完整語法  
 以下是磁碟分割物件的結構描述表示法。  
  
```  
"partitions": {  
                "type": "array",  
                "items": {  
                  "description": "Partition object of Tabular Object Model (TOM)",  
                  "type": "object",  
                  "properties": {  
                    "name": {  
                      "type": "string"  
                    },  
                    "description": {  
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
                    },  
                    "mode": {  
                      "enum": [  
                        "import",  
                        "directQuery",  
                        "default"  
                      ]  
                    },  
                    "dataView": {  
                      "enum": [  
                        "full",  
                        "sample",  
                        "default"  
                      ]  
                    },  
                    "source": {  
                      "anyOf": [  
                        {  
                          "description": "QueryPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "query": {  
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
                            },  
                            "dataSource": {  
                              "type": "string"  
                            }  
                          },  
                          "additionalProperties": false  
                        },  
                        {  
                          "description": "CalculatedPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "expression": {  
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
                      ]  
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
              },  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
