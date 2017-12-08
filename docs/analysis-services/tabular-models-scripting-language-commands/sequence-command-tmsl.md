---
title: "序列命令 (TMSL) |Microsoft 文件"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 898d6ec2-9b40-441b-be2b-5728d1d2882e
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6fe2e7416c4c86b926f30295b6fe2f75a334751f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sequence-command-tmsl"></a>Sequence 命令 (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  使用**順序**批次模式中執行一組連續的作業，Analysis Services 執行個體上的命令。  整個命令，以及其元件部分的所有必須完成才會成功的交易順序。  
  
 可以執行下列命令以循序方式，除了針對**重新整理**會同時處理多個物件的平行執行的命令。  
  
-   [建立命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)  
  
-   [為 CreateOrReplace 命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)  
  
-   [Alter 命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)  
  
-   [刪除命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)  
  
-   [重新整理命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)  
  
-   [備份命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/backup-command-tmsl.md)  
  
-   [還原命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/restore-command-tmsl.md)  
  
-   [附加命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/attach-command-tmsl.md)  
  
-   [卸離命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/detach-command-tmsl.md)  
  
## <a name="request"></a>要求  
 **maxParallelism**是選擇性的屬性會決定是否**重新整理**循序或平行執行的作業。  
  
 預設行為是盡可能使用最多的平行處理原則。 內嵌**重新整理**內**順序**，您可以控制執行緒處理，包括限制只在一個執行緒的作業期間使用的確切數目。  
  
> [!NOTE]  
>  指派給整數**maxParallelism**決定在處理期間所使用的執行緒數目上限。 有效值為任何正整數。 將值設定為 1 等於無法同時 （使用一個執行緒）。  
  
 只有**重新整理**以平行方式執行。 如果您修改**maxParallelism**若要使用固定的數目的執行緒，請務必檢閱的內容上[重新整理命令 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md) ，了解潛在的影響。 很可能破壞平行處理原則，即使您已供多個執行緒使用的方式來設定屬性。 下列的重新整理類型序列可讓您最佳的平行處理原則程度：  
  
-   首先，指定使用 ClearValues 的所有物件的 重新整理  
  
-   接下來，指定使用 DataOnly 的所有物件的 重新整理  
  
-   上次重新整理指定使用完整、 Calculate、 自動或新增的所有物件  
  
 任何變化，這會中斷平行處理原則。  
  
```  
{   
  "sequence":    
    {   
      "maxParallelism": 3,   
      "operations": [   
        {   
          "mergepartitions": {   
            "sources": [   
              {   
                "database": "salesdatabase",   
                "table": "Sales",   
                "partition": "partition1"   
              },   
              {   
                "database": "salesdatabase",   
                "table": "Sales",   
                "partition": "partition2"   
              }   
            ]   
          }   
        },   
        {   
          "refresh": {   
            "type": "calculate",   
            "object": {   
             "database": "salesdatabase"   
            }   
          }   
        }   
      ]   
    }      
}   
```  
  
## <a name="response"></a>回應  
 當命令執行成功，則傳回空的結果。 否則，傳回 XMLA 例外狀況。  
  
## <a name="usage-endpoints"></a>使用方式 （端點）  
 這個命令項目用在陳述式的[Execute Method &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)呼叫透過 XMLA 端點，以下列方式公開：  
  
-   以 XMLA 視窗中 SQL Server Management Studio (SSMS)  
  
-   為輸入檔案**叫用 ascmd** PowerShell cmdlet  
  
-   做為輸入到 SSIS 工作或 SQL Server Agent 作業  
  
 您無法從 SSMS 產生現成的指令碼，此命令。 相反地，您可以開始使用範例，或撰寫您自己。  
  
 [ \[MS-SSAS T\]: SQL Server Analysis Services 表格式 （SQL Server 技術通訊協定）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文件包含區段 3.1.5.2.2 描述結構的 JSON 表格式中繼資料命令和物件. 目前，該文件涵蓋命令和功能尚未實作用於 TMSL 指令碼。 請參閱主題 ([表格式模型指令碼語言 &#40;TMSL &#41;參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) 以釐清支援的項目。  
  
## <a name="see-also"></a>請參閱＜  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
