---
title: "物件定義的表格式模型指令碼語言 (TMSL) |Microsoft 文件"
ms.custom: 
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 486f0507-cec6-4672-b947-0bb61d1cbc46
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fcf8b3c47b7663e467ad421a3732f8663320f055
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="tmsl-reference---tabular-objects"></a>TMSL 參考-表格式物件
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]應用程式，來建立、 使用，或管理表格式資料庫或連接至表格式模式中的 SQL Server 2016 Analysis Services 執行個體可以使用表格式模型指令碼語言 」 (TMSL) 命令，並以 JSON 格式的物件表示法。  
  
 本文記載使用 SQL Server Management Studio、 SQL Server Data Tools (SSDT) 和 AMO PowerShell 所產生的指令碼中的 TMSL 結構描述的主要物件。  
  
 物件的 JSON 中定義，而且用於 TMSL 指令，例如 Create、 Alter 和刪除。 請參閱[命令中表格式模型指令碼語言 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md)如命令的清單。  
  
## <a name="main-objects"></a>主要物件  
 下表是 TMSL 指令碼中最常使用的物件清單。  
  
|||  
|-|-|  
|[資料庫物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|定義表格式資料庫相容性層級 1200年或更高，相同層級的模型為基礎。|  
|[模型物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|定義在 1200年或更高的相容性層級的表格式模型。|  
|[資料來源物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|當模型處於 DirectQuery 模式時，使用載入模型中，匯入期間或傳遞查詢的資料來源中定義的連接。|  
|[Tables 物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|指定模型的資料表。|  
|[資料分割物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|定義資料表資料列集，包括導出的資料表的儲存的體。|  
|[關聯性物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|定義資料表之間的關聯性。|  
|[角色物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|定義權限、 成員資格，以及安全性篩選，以控制存取資料和作業。|  
  
## <a name="see-also"></a>請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
