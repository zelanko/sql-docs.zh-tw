---
title: 重新整理命令 (TMSL) |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f17bf75dede2c5f05055d2d1e9a4f7ea595e738
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="refresh-command-tmsl"></a>重新整理命令 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  處理目前資料庫中的物件。   
**重新整理**永遠會平行執行的啟用使用節流設定，除非[順序命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md)。  
  
 您可以在資料重新整理作業期間，覆寫某些物件的某些屬性：  
  
-   變更**QueryDefinition**屬性**分割**匯入資料使用上快速篩選器運算式的物件。  
  
-   資料來源認證提供的**重新整理**命令中**ConnectionString**屬性**DataSource**物件。 這種方法無法被視為更安全，提供認證，以及作業的期間暫時使用而不儲存。  
  
 請參閱本主題適用於這些屬性會覆寫的圖例中的範例。  
  
> [!NOTE]  
>  不同於多維度處理，沒有處理進行表格式處理錯誤的任何特殊處理。  

  
## <a name="request"></a>要求  
 **重新整理**採用型別參數和物件定義。  
  
```  
    {  
        "refresh": {  
            "description": "Parameters of Refresh command of Analysis Services JSON API",  
            "properties": {  
            "type": {  
                "enum": [  
                "full",  
                "clearValues",  
                "calculate",  
                "dataOnly",  
                "automatic",  
                "add",  
                "defragment"  
                ]  
            },  
            "objects": {  
. . .   
```  
  
 **類型**參數設定的處理作業的範圍。  
  
||||  
|-|-|-|  
|**重新整理類型**|**適用於**|**說明**|  
|完整|資料庫，<br />資料表中，<br />資料分割|在指定分割區、資料表或資料庫中的所有分割區內，重新整理資料並重新計算所有相依性。 若是計算分割區，請重新計算分割區和所有相依性。|  
|clearValues|資料庫，<br />資料表中，<br />資料分割|清除此物件及其所有相依性中的值。|  
|計算|資料庫，<br />資料表中，<br />資料分割|重新計算此物件及其所有的相依性，但是只有在需要時進行。 除了動態公式之外，此值不會強制重新計算。|  
|dataOnly|資料庫，<br />資料表中，<br />資料分割|重新整理此物件中的資料，並清除所有相依性。|  
|automatic|資料庫，<br />資料表中，<br />資料分割|如果物件需要重新整理與重新計算，請重新整理並重新計算物件，以及其所有的相依性。 若分割區處於 Ready 以外的狀態，則適用。|  
|add|資料分割|將資料附加至此分割區，並重新計算所有相依性。 只有在一般分割區而非計算分割區時，此命令才有效。|  
|重組|資料庫，<br />Table|重組指定資料表中的資料。 當從資料表中新增或移除資料時，每個資料行字典可能被不再存在於實際資料行值的值所干擾。 重組選項將會清除字典中不再使用的值。|  
  
 您可以重新整理下列物件：  
  
 [資料庫物件&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)處理資料庫。  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200"  
      }  
    ]  
  }  
}  
```  
  
 [Tables 物件&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)處理單一資料表。  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "Date"  
      }  
    ]  
  }  
}  
```  
  
 [資料分割物件&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)處理資料表中的單一資料分割。  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota"  
      },  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota - 2011"  
      }  
    ]  
  }  
}  
```  
  
## <a name="response"></a>回應  
 當命令執行成功，則傳回空的結果。 否則，傳回 XMLA 例外狀況。  
  
## <a name="examples"></a>範例  
 覆寫兩個**ConnectionString**及查詢資料分割的定義。  
  
```  
{   
    "refresh": {   
        "type": "data",   
        "objects": [   
            {   
                "database": "tmtestdb",   
                "table": "sales"   
            },   
            {   
                "database": "tmtestdb",   
                "table": "customer"   
            }   
        ],   
        "overrides": [   
            {   
                "dataSources": [ // Bindings for Data Sources   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "dataSource": "contoso"   
                        },   
                        "dataSource": {   
                        "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=contoso;Integrated Security=SSPI;Persist Security Info=false"   
"   
                        }   
                    }   
                ],   
                "partitions": [ // Bindings for Partitions   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "table": "sales",   
                            "partition": "2015"   
                        },   
                        "partition": {   
                            "source": {   
                                "query": [  
                                     "SELECT sales.salesamount, customer.customername FROM sales",  
                                     "JOIN customer on custKey = sales.custkey",  
                                     "JOIN date on date.DateKey = customer.OrderDate",  
                                     "WHERE date.CalendarYear='2015'"  
                                  ],  
                            }   
                        }   
                    }   
                ]   
            }   
        ]   
    }   
}   
```  
  
 特定的範圍覆寫設定的型別參數為**dataOnly**重新整理，中繼資料會保持不變。  
  
```  
{   
        "refresh" : {   
            "type" : "dataOnly",   
            "objects" : [   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Customer"   
                },   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                }   
            ],   
            "overrides" : [{   
                "scope" : {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                },   
                "dataSources" : [{   
                    "originalObject" : {   
                        "dataSource" : "SqlServer sqlcldb2 AS_foodmart_2000"   
                    },   
                    "connectionString" : "Provider=SQLNCLI11;Data Source=sqlcldb2;Initial Catalog=AS_foodmart_2000;Integrated Security=SSPI;Persist Security Info=false"   
                }]   
            }]   
        }   
    }   
```  
  
## <a name="usage-endpoints"></a>使用方式 （端點）  
 這個命令項目用在陳述式的[Execute Method &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md)呼叫透過 XMLA 端點，以下列方式公開：  
  
-   以 XMLA 視窗中 SQL Server Management Studio (SSMS)  
  
-   為輸入檔案**叫用 ascmd** PowerShell cmdlet  
  
-   做為輸入到 SSIS 工作或 SQL Server Agent 作業  
  
 您可以從 SSMS 產生現成的指令碼，此命令。  例如，您可以按一下**指令碼**處理對話方塊中。  
  
 [ \[MS-SSAS T\]: QL Server Analysis Services 表格式 （SQL Server 技術通訊協定）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文件包含區段 3.1.5.2.2 描述結構的 JSON 表格式中繼資料命令和物件。 目前，該文件涵蓋命令和功能尚未實作用於 TMSL 指令碼。 請參閱主題 ([表格式模型指令碼語言&#40;TMSL&#41;參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) 以釐清支援的項目。  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [處理選項和設定&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)  
  
  
