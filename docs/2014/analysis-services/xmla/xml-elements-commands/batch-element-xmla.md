---
title: 批次元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Batch Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Batch
- microsoft.xml.analysis.batch
- http://schemas.microsoft.com/analysisservices/2003/engine#Batch
helpviewer_keywords:
- Batch command
ms.assetid: 818f3212-9605-4e34-8623-1154d9fae1f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d402c1f6c35370a506ed57c43b8fbc05d0b6bef7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178138"
---
# <a name="batch-element-xmla"></a>Batch 元素 (XMLA)
  執行一或多個 XML for Analysis (XMLA) 命令，以批次作業中，循序或平行執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Batch Transaction="Boolean" ProcessAffectedObjects="Boolean">  
      <Bindings>...</Bindings>  
      <DataSource>...</DataSource>  
      <DataSourceView>...</DataSourceView>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <Parallel>...</Parallel>  
      <!-- One or more XMLA commands -->  
   </Batch>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[繫結](../xml-elements-properties/bindings-element-xmla.md)， [DataSource](../xml-elements-properties/source-element-xmla.md)， [DataSourceView](../xml-elements-properties/datasourceview-element-xmla.md)， [ErrorConfiguration](../../scripting/objects/errorconfiguration-element-assl.md)，[平行](../xml-elements-properties/parallel-element-xmla.md)<br /><br /> 一或多個下列的 XMLA 命令：[改變](alter-element-xmla.md)，[備份](backup-element-xmla.md)， [BeginTransaction](begintransaction-element-xmla.md)， [ClearCache](clearcache-element-xmla.md)， [CommitTransaction](committransaction-element-xmla.md)，[建立](create-element-xmla.md)，[刪除](delete-element-xmla.md)， [DesignAggregations](designaggregations-element-xmla.md)，[卸除](drop-element-xmla.md)， [插入](insert-element-xmla.md)，[鎖定](lock-element-xmla.md)， [MergePartitions](mergepartitions-element-xmla.md)， [NotifyTableChange](notifytablechange-element-xmla.md)，[程序](process-element-xmla.md)， [還原](restore-element-xmla.md)， [RollbackTransaction](rollbacktransaction-element-xmla.md)， [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e)，[陳述式](statement-element-xmla.md)，[訂閱](subscribe-element-xmla.md)，[同步處理](synchronize-element-xmla.md)，[解除鎖定](unlock-element-xmla.md)， [Update](update-element-xmla.md)， [UpdateCells](drop-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|ProcessAffectedObjects|(選擇性 `Boolean` 屬性) 指出是否將處理需要重新處理的所有物件。<br /><br /> 如果設定為 true，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就會處理由於處理 `Batch` 命令中包含的物件而需要重新處理的任何物件。<br /><br /> 如果設定為 `false`，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就只會處理 `Batch` 命令中包含的物件。|  
|Transaction|(選擇性 `Boolean` 屬性) 指出 `Batch` 命令中包含的命令會被視為單一交易或個別交易。<br /><br /> 如果設定為 true，`Batch` 命令中包含的所有命令都會被視為單一交易。 如果任何命令失敗，系統就會回復在失敗命令之前執行的命令，而且 `Batch` 命令會停止，而不執行後續命令。<br /><br /> 如果設定為 `false`，`Batch` 命令就會嘗試執行每一個命令，並認可成功完成之每個命令的結果。|  
  
## <a name="remarks"></a>備註  
  
> [!WARNING]  
>  批次作業目前不支援命令/執行/陳述式。  
  
 如需有關以 XMLA 執行批次作業的詳細資訊，請參閱 <<c0> [ 執行批次運算&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
