---
title: "XML for Analysis 符合 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5657f57d1f7eee76efb51da0c4bd3ff278aa47ac
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="xml-for-analysis-compliance-xmla"></a>XML for Analysis 符合 (XMLA)
  XML for Analysis 1.1 規格描述了一套開放標準，可支援對位於全球資訊網上的資料來源進行資料存取。 本主題詳細說明的 xml for Analysis 1.1 規格所支援的相容性層級[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
## <a name="compliant-items"></a>符合的項目  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 符合 XML for Analysis 1.1 規格中所列的所有強制項目。 此外，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會實作 XML for Analysis 1.1 規格中所描述的下列選擇性項目。  
  
|項目|規格|實作|  
|----------|-------------------|--------------------|  
|工作階段支援|XML for Analysis 1.1 規格之＜支援 XML for Analysis 中的 Statefulness＞一節中所列的 SOAP 標頭元素。|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援所有列出的 SOAP 標頭元素，如規格所述。|  
  
## <a name="extensions"></a>延伸模組  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也會擴充 XML for Analysis 1.1 規格，以便支援下列額外功能。  
  
|項目|規格|實作|  
|----------|-------------------|--------------------|  
|通訊協定交涉|XML for Analysis 1.1 規格中沒有包含任何資訊。|ProtocolCapabilities 標頭項目加入[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支援通訊協定功能的交涉。|  
|Discover 方法所支援的 XML for Analysis (XMLA) 命令|XML for Analysis 1.1 規格支援下列命令：<br /><br /> [陳述式元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下列命令：<br /><br /> [Alter 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [Backup 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [批次元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [BeginTransaction 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [取消元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [ClearCache 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [CommitTransaction 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [建立元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [刪除項目 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [DesignAggregations 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [卸除元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [插入項目 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [Lock 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [MergePartitions 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [NotifyTableChange 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [Process 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [Restore 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [RollbackTransaction 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [陳述式元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [訂閱元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [同步處理項目 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [解除鎖定元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [Update 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [UpdateCells 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|表格式資料列集中的資料行錯誤|沒有列在 XML for Analysis 1.1 規格中。|[錯誤](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)所使用項目[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]報告錯誤的資料行中包含的項目[列](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)項目。|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis &#40;XMLA&#41; 參考](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
