---
title: 批次元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 76fcd68ca71db298bc66dc63a3fa20c394c196c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137158"
---
# <a name="batch-element-xmla"></a>Batch 元素 (XMLA)
  執行一或多個 XML for Analysis (XMLA) 命令，以批次作業，循序或平行的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[繫結](../xml-elements-properties/bindings-element-xmla.md)， [DataSource](../xml-elements-properties/source-element-xmla.md)， [DataSourceView](../xml-elements-properties/datasourceview-element-xmla.md)， [ErrorConfiguration](../../scripting/objects/errorconfiguration-element-assl.md)，[平行](../xml-elements-properties/parallel-element-xmla.md)<br /><br /> One or more of the following XMLA commands: [Alter](alter-element-xmla.md), [Backup](backup-element-xmla.md), [BeginTransaction](begintransaction-element-xmla.md), [ClearCache](clearcache-element-xmla.md), [CommitTransaction](committransaction-element-xmla.md), [Create](create-element-xmla.md), [Delete](delete-element-xmla.md), [DesignAggregations](designaggregations-element-xmla.md), [Drop](drop-element-xmla.md), [Insert](insert-element-xmla.md), [Lock](lock-element-xmla.md), [MergePartitions](mergepartitions-element-xmla.md), [NotifyTableChange](notifytablechange-element-xmla.md), [Process](process-element-xmla.md), [Restore](restore-element-xmla.md), [RollbackTransaction](rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [Statement](statement-element-xmla.md), [Subscribe](subscribe-element-xmla.md), [Synchronize](synchronize-element-xmla.md), [Unlock](unlock-element-xmla.md), [Update](update-element-xmla.md), [UpdateCells](drop-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|ProcessAffectedObjects|(選擇性 `Boolean` 屬性) 指出是否將處理需要重新處理的所有物件。<br /><br /> 如果設定為 true，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就會處理由於處理 `Batch` 命令中包含的物件而需要重新處理的任何物件。<br /><br /> 如果設定為 `false`，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就只會處理 `Batch` 命令中包含的物件。|  
|Transaction|(選擇性 `Boolean` 屬性) 指出 `Batch` 命令中包含的命令會被視為單一交易或個別交易。<br /><br /> 如果設定為 true，`Batch` 命令中包含的所有命令都會被視為單一交易。 如果任何命令失敗，系統就會回復在失敗命令之前執行的命令，而且 `Batch` 命令會停止，而不執行後續命令。<br /><br /> 如果設定為 `false`，`Batch` 命令就會嘗試執行每一個命令，並認可成功完成之每個命令的結果。|  
  
## <a name="remarks"></a>備註  
  
> [!WARNING]  
>  批次作業目前不支援命令/執行/陳述式。  
  
 如需有關以 XMLA 執行批次作業的詳細資訊，請參閱[執行批次作業&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  