---
title: XML for Analysis 符合 (XMLA) |Microsoft 文件
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
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fb4279ab8c516f4db18310a03e7b85e389f2bc2b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034847"
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
|通訊協定交涉|XML for Analysis 1.1 規格中沒有包含任何資訊。|[ProtocolCapabilities](xml-elements-headers/protocolcapabilities-element-xmla.md)標頭項目加入[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支援通訊協定功能的交涉。|  
|Discover 方法所支援的 XML for Analysis (XMLA) 命令|XML for Analysis 1.1 規格支援下列命令：<br /><br /> -   [陳述式項目&#40;XMLA&#41;](xml-elements-commands/statement-element-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下列命令：<br /><br /> -   [Alter 元素&#40;XMLA&#41;](xml-elements-commands/alter-element-xmla.md)<br />-   [備份項目&#40;XMLA&#41;](xml-elements-commands/backup-element-xmla.md)<br />-   [批次項目&#40;XMLA&#41;](xml-elements-commands/batch-element-xmla.md)<br />-   [BeginTransaction 元素&#40;XMLA&#41;](xml-elements-commands/begintransaction-element-xmla.md)<br />-   [Cancel 元素&#40;XMLA&#41;](xml-elements-commands/cancel-element-xmla.md)<br />-   [ClearCache 元素&#40;XMLA&#41;](xml-elements-commands/clearcache-element-xmla.md)<br />-   [CommitTransaction 元素&#40;XMLA&#41;](xml-elements-commands/committransaction-element-xmla.md)<br />-   [建立項目&#40;XMLA&#41;](xml-elements-commands/create-element-xmla.md)<br />-   [刪除項目&#40;XMLA&#41;](xml-elements-commands/delete-element-xmla.md)<br />-   [DesignAggregations 元素&#40;XMLA&#41;](xml-elements-commands/designaggregations-element-xmla.md)<br />-   [Drop 元素&#40;XMLA&#41;](xml-elements-commands/drop-element-xmla.md)<br />-   [插入項目&#40;XMLA&#41;](xml-elements-commands/insert-element-xmla.md)<br />-   [鎖定項目&#40;XMLA&#41;](xml-elements-commands/lock-element-xmla.md)<br />-   [MergePartitions 元素&#40;XMLA&#41;](xml-elements-commands/mergepartitions-element-xmla.md)<br />-   [NotifyTableChange 元素&#40;XMLA&#41;](xml-elements-commands/notifytablechange-element-xmla.md)<br />-   [處理項目&#40;XMLA&#41;](xml-elements-commands/process-element-xmla.md)<br />-   [Restore 元素&#40;XMLA&#41;](xml-elements-commands/restore-element-xmla.md)<br />-   [RollbackTransaction 元素&#40;XMLA&#41;](xml-elements-commands/rollbacktransaction-element-xmla.md)<br />-SetPasswordEncryptionKey 元素<br />-   [陳述式項目&#40;XMLA&#41;](xml-elements-commands/statement-element-xmla.md)<br />-   [Subscribe 元素&#40;XMLA&#41;](xml-elements-commands/subscribe-element-xmla.md)<br />-   [同步處理項目&#40;XMLA&#41;](xml-elements-commands/synchronize-element-xmla.md)<br />-   [Unlock 元素&#40;XMLA&#41;](xml-elements-commands/unlock-element-xmla.md)<br />-   [更新項目&#40;XMLA&#41;](xml-elements-commands/update-element-xmla.md)<br />-   [UpdateCells 元素&#40;XMLA&#41;](xml-elements-commands/updatecells-element-xmla.md)|  
|表格式資料列集中的資料行錯誤|沒有列在 XML for Analysis 1.1 規格中。|[錯誤](xml-elements-properties/error-element-xmla.md)所使用項目[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]報告錯誤的資料行中包含的項目[列](xml-elements-properties/error-element-xmla.md)項目。|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis &#40;XMLA&#41;參考](xml-for-analysis-xmla-reference.md)  
  
  