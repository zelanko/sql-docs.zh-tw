---
title: 命令元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2f941b50c8e2f6d23fc65d96a3f4eaa61075e76e
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574990"
---
# <a name="command-element-xmla"></a>Command 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含要執行之命令[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
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
|父元素|[執行](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|子元素|[Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)，[備份](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)，[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)， [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)，[取消](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)， [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)[CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)，[建立](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)，[刪除](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)， [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)，[卸除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)，[插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[鎖定](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)， [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)， [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)，[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)，[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)， [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)， [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e)，[陳述式](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)， [訂閱](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)，[同步](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)，[解除鎖定](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)，[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)， [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **命令**所使用項目**Execute**命令轉送至資料來源的方法。 雖然 XML for Analysis (XMLA) 1.1 規格僅支援**陳述式**命令時，Analysis Services 支援許多新的 XMLA 命令。 如需有關所支援之 XMLA 命令[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，請參閱[命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)。  
  
## <a name="see-also"></a>另請參閱
 [XML 資料型別&#40;XMLA&#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
