---
title: 命令元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Command Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.command
- Command
- urn:schemas-microsoft-com:xml-analysis#Command
- http://schemas.microsoft.com/analysisservices/2003/engine#Command
helpviewer_keywords:
- Command element
ms.assetid: 9abc14df-7cbe-46bc-ba0f-f0691c19afad
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9b461e0ec565776ead270902cf6c01ebe7409d3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332238"
---
# <a name="command-element-xmla"></a>Command 元素 (XMLA)
  包含要執行命令[Execute](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Execute>  
   ...  
   <Command>  
      <Alter>...</Alter>  
      <!-- or -->  
      <Backup>...</Backup>  
      <!-- or -->  
      <Batch>...</Batch>  
      <!-- or -->  
      <BeginTransaction>...</BeginTransaction>  
      <!-- or -->  
      <Cancel>...</Cancel>  
      <!-- or -->  
      <ClearCache>...</ClearCache>  
      <!-- or -->  
      <CommitTransaction>...</CommitTransaction>  
      <!-- or -->  
      <Create>...</Create>  
      <!-- or -->  
      <Delete>...</Delete>  
      <!-- or -->  
      <DesignAggregations>...</DesignAggregations>  
      <!-- or -->  
      <Drop>...</Drop>  
      <!-- or -->  
      <Insert>...</Insert>  
      <!-- or -->  
      <Lock>...</Lock>  
      <!-- or -->  
      <MergePartitions>...</MergePartitions>  
      <!-- or -->  
      <NotifyTableChange>...</NotifyTableChange>  
      <!-- or -->  
      <Process>...</Process>  
      <!-- or -->  
      <Restore>...</Restore>  
      <!-- or -->  
      <RollbackTransaction>...</RollbackTransaction>  
      <!-- or -->  
      <SetPasswordEncryptionKey>...</SetPasswordEncryptionKey>  
      <!-- or -->  
      <Statement>...</Statement>  
      <!-- or -->  
      <Subscribe>...</Subscribe>  
      <!-- or -->  
      <Synchronize>...</Synchronize>  
      <!-- or -->  
      <Unlock>...</Unlock>  
      <!-- or -->  
      <Update>...</Update>  
      <!-- or -->  
      <UpdateCells>...</UpdateCells>  
   </Command>  
   ...  
</Execute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[執行](../xml-elements-methods-execute.md)|  
|子元素|[Alter](../xml-elements-commands/alter-element-xmla.md)，[備份](../xml-elements-commands/backup-element-xmla.md)，[批次](../xml-elements-commands/batch-element-xmla.md)， [BeginTransaction](../xml-elements-commands/begintransaction-element-xmla.md)，[取消](../xml-elements-commands/cancel-element-xmla.md)， [ClearCache](../xml-elements-commands/clearcache-element-xmla.md)[CommitTransaction](../xml-elements-commands/committransaction-element-xmla.md)，[建立](../xml-elements-commands/create-element-xmla.md)，[刪除](../xml-elements-commands/delete-element-xmla.md)， [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)，[卸除](../xml-elements-commands/drop-element-xmla.md)，[插入](../xml-elements-commands/insert-element-xmla.md)，[鎖定](../xml-elements-commands/lock-element-xmla.md)， [MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)， [NotifyTableChange](../xml-elements-commands/notifytablechange-element-xmla.md)，[程序](../xml-elements-commands/process-element-xmla.md)，[還原](../xml-elements-commands/restore-element-xmla.md)， [RollbackTransaction](../xml-elements-commands/rollbacktransaction-element-xmla.md)， [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e)，[陳述式](../xml-elements-commands/statement-element-xmla.md)， [訂閱](../xml-elements-commands/subscribe-element-xmla.md)，[同步處理](../xml-elements-commands/synchronize-element-xmla.md)，[解除鎖定](../xml-elements-commands/unlock-element-xmla.md)，[更新](../xml-elements-commands/update-element-xmla.md)， [UpdateCells](../xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Command` 方法會使用 `Execute` 元素，將命令轉送至資料來源。 雖然 XML for Analysis (XMLA) 1.1 規格僅支援`Statement`命令， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支援許多新的 XMLA 命令。 如需所支援的 XMLA 命令[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，請參閱 <<c2> [ 命令&#40;XMLA&#41;](../xml-elements-commands/xml-elements-commands.md)。</c2>  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料型別&#40;XMLA&#41;](../xml-data-types/xml-data-types-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
