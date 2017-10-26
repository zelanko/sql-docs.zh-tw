---
title: "MergePartitions 命令 (TMSL) |Microsoft 文件"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: dd568426-a415-41bf-b1e9-ea2261babf81
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 290e5e99219a37a1ff1f6793d640756ba21f7467
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="mergepartitions-command-tmsl"></a>MergePartitions 命令 (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  將一或多個來源資料分割的資料合併至目標資料分割，然後刪除來源分割區。 合併的一部分，將不會更新目標資料分割的 SQL 查詢。 若要確保後續處理分割區的所有資料，您應該將查詢修訂，讓它在合併分割區會選取所有資料。  
  
## <a name="request"></a>要求  
 您必須指定資料庫、 資料表，以及來源和目標資料分割。 您只可以合併來自相同資料表的資料分割。  
  
```  
{   
  "mergePartitions": {   
    "object": {   
      "database": "salesdatabase",   
      "table": "sales",   
      "partition": "may2015"   
    },   
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
}  
  
```  
  
## <a name="response"></a>回應  
 當命令執行成功，則傳回空的結果。 否則，傳回 XMLA 例外狀況。  
  
## <a name="usage-endpoints"></a>使用方式 （端點）  
 這個命令項目用在陳述式的[Execute Method &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)呼叫透過 XMLA 端點，以下列方式公開：  
  
-   以 XMLA 視窗中 SQL Server Management Studio (SSMS)  
  
-   為輸入檔案**叫用 ascmd** PowerShell cmdlet  
  
-   做為輸入到 SSIS 工作或 SQL Server Agent 作業  
  
 您可以從 SSMS 產生現成的指令碼，此命令。  例如，您可以按一下**指令碼**資料分割管理員 對話方塊中。  
  
 [ \[MS-SSAS T\]: QL Server Analysis Services 表格式 （SQL Server 技術通訊協定）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文件包含區段 3.1.5.2.2 描述結構的 JSON 表格式中繼資料命令和物件。 目前，該文件涵蓋命令和功能尚未實作用於 TMSL 指令碼。 請參閱主題[表格式模型指令碼語言 &#40;TMSL &#41;參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)以釐清支援的項目  

## <a name="see-also"></a>另請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [建立及管理表格式模型資料分割 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  

