---
title: 命令在表格式模型指令碼語言 (TMSL) |Microsoft 文件
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 4eb07192-6f53-4426-830a-d63a945dbcab
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a12ba3199647029fee5bd422000a4adc5ea4e4d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="tmsl-reference---commands"></a>TMSL 參考-命令
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  您可以執行命令，在 XMLA 端點，公式中使用表格式模型指令碼語言 (TMSL)，針對表格式模型資料庫的 JSON 物件定義。   請參閱[表格式模型指令碼語言中的物件定義&#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md)使用下列命令所使用的物件清單。  
  
## <a name="object-operations"></a>物件的作業  
  
|||  
|-|-|  
|[Alter 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)|請內嵌物件的修改，而不必指定完整定義。|  
|[建立命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)|建立新的物件，包括子系。|  
|[為 CreateOrReplace 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)|建立或取代物件定義的組件。 必須提供完整定義。|  
|[Delete 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)|刪除的物件，包括子系。|  
  
## <a name="data-refresh-operations"></a>資料重新整理作業  
  
|||  
|-|-|  
|[MergePartitions 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md)|目標資料分割合併為來源，並刪除目標。|  
|[重新整理命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)|處理資料庫、 資料表或資料分割。|  
  
## <a name="scripting"></a>指令碼  
  
|||  
|-|-|  
|[序列命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md)|循序或平行批次作業|  
  
## <a name="database-management-operations"></a>資料庫管理作業  
  
|||  
|-|-|  
|[附加命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/attach-command-tmsl.md)|將檔案加入至伺服器。|  
|[卸離命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/detach-command-tmsl.md)|從伺服器中移除檔案。|  
|[備份命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/backup-command-tmsl.md)|建立資料庫的備份檔案。|  
|[Restore 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/restore-command-tmsl.md)|將資料庫還原到伺服器。|  
|[Synchronize 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/synchronize-command-tmsl.md)|同步處理 Analysis Services 資料庫與另一個現有的資料庫。|  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [安裝 Analysis Services 資料提供者&#40;AMO、 ADOMD.NET、 MSOLAP&#41;](../../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md)   
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
