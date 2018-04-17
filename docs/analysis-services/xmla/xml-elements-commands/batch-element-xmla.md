---
title: 批次元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Batch Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Batch
- microsoft.xml.analysis.batch
- http://schemas.microsoft.com/analysisservices/2003/engine#Batch
helpviewer_keywords:
- Batch command
ms.assetid: 818f3212-9605-4e34-8623-1154d9fae1f0
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8591a521cb1d3fce934e32be3d7b5cd3a4a977c4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="batch-element-xmla"></a>Batch 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]執行一或多個 XML for Analysis (XMLA) 命令，以批次作業，循序或平行的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[繫結](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)， [DataSource](../../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md)， [DataSourceView](../../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md)， [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)，[平行](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)<br /><br /> 一或多個下列的 XMLA 命令： [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)，[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)， [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)， [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)， [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)，[建立](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)，[刪除](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)， [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)，[卸除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)， [插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[鎖定](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)， [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)， [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)，[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)， [還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)， [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)， [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e)，[陳述式](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)，[訂閱](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)，[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)，[解除鎖定](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)，[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)， [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|ProcessAffectedObjects|(選擇性**布林**屬性) 指出是否將處理需要重新處理的所有物件。<br /><br /> 如果設為 true，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體來處理任何物件，而需要重新處理物件中包含的結果。**批次**命令。<br /><br /> 如果設定為**false**、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中包含的物件執行個體來處理**批次**命令。|  
|Transaction|(選擇性**布林**屬性) 指出命令是否包含在**批次**命令會被視為單一交易或個別交易。<br /><br /> 如果設定為 true 的所有命令中包含**批次**命令會被視為單一交易。 如果任何命令失敗，失敗的命令之前執行的命令會回復，而**批次**命令會停止且不執行後續的命令。<br /><br /> 如果設定為**false**、**批次**命令嘗試執行每一個命令，並認可成功完成每個命令的結果。|  
  
## <a name="remarks"></a>備註  
  
> [!WARNING]  
>  批次作業目前不支援命令/執行/陳述式。  
  
 如需有關以 XMLA 執行批次作業的詳細資訊，請參閱[執行批次作業 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="see-also"></a>請參閱  
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
