---
title: 批次元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2f249402d3348e491a409da52db76f531bcd594f
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981890"
---
# <a name="batch-element-xmla"></a>Batch 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  執行一或多個 XML for Analysis (XMLA) 命令批次作業、 循序或平行，Analysis Services 執行個體上。  
  
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
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[繫結](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)， [DataSource](../../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md)， [DataSourceView](../../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md)， [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)，[平行](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)<br /><br /> 一或多個下列的 XMLA 命令：[改變](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)，[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)， [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)， [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)， [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)，[建立](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)，[刪除](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)， [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)，[卸除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)， [插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[鎖定](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)， [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)， [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)，[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)， [還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)， [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)， [SetPasswordEncryptionKey](http://msdn.microsoft.com/fb262737-f0f4-4441-985e-3b2a94d00a9e)，[陳述式](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)，[訂閱](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)，[同步處理](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)，[解除鎖定](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)， [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)， [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|ProcessAffectedObjects|(選擇性**布林**屬性) 指出是否將處理需要重新處理的所有物件。<br /><br /> 如果設定為 true，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體處理的任何物件，而需要重新處理物件中包含的結果**批次**命令。<br /><br /> 如果設定為**假**，則[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體都會處理中包含的物件**批次**命令。|  
|Transaction|(選擇性**布林**屬性) 指出命令是否已納入**批次**命令會被視為單一交易或個別交易。<br /><br /> 如果設定為 true，所有命令中包含**批次**命令會被視為單一交易。 如果任何命令失敗，失敗的命令之前執行的命令會回復，而**批次**命令會停止，而不執行後續命令。<br /><br /> 如果設定為**假**，則**批次**命令嘗試執行每一個命令，並認可成功完成每個命令的結果。|  
  
## <a name="remarks"></a>備註  
  
> [!WARNING]  
>  批次作業目前不支援命令/執行/陳述式。  
  
 如需有關以 XMLA 執行批次作業的詳細資訊，請參閱 <<c0> [ 執行批次運算&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)。</c0>  
  
## <a name="see-also"></a>另請參閱
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
