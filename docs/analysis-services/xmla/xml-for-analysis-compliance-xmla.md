---
title: XML for Analysis (XMLA) 符合 |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b618fdd8cca3faed72afb0276f18cd928a3f31f7
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34576880"
---
# <a name="xml-for-analysis-xmla-compliance"></a>XML for Analysis (XMLA) 相容性
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]  

  XML for Analysis 1.1 規格描述了一套開放標準，可支援對位於全球資訊網上的資料來源進行資料存取。 本主題詳細說明 xml for Analysis 1.1 規格支援的 Azure Analysis Services 和 SQL Server Analysis Services 的相容性層的級。  
  
## <a name="compliant-items"></a>符合的項目  
Analysis Services 符合 XML for Analysis 1.1 規格中所列的所有強制項目。 此外，Analysis Services 實作 XML for Analysis 1.1 規格中所述的下列選擇性項目。  
  
|項目|規格|實作|  
|----------|-------------------|--------------------|  
|工作階段支援|XML for Analysis 1.1 規格之＜支援 XML for Analysis 中的 Statefulness＞一節中所列的 SOAP 標頭元素。|所有列出的 SOAP 標頭元素支援 Analysis Services 規格中所述。|  
  
## <a name="extensions"></a>延伸模組  
 Analysis Services 也會擴充 XML for Analysis 1.1 規格支援下列的其他特性與功能。  
  
|項目|規格|實作|  
|----------|-------------------|--------------------|  
|通訊協定交涉|XML for Analysis 1.1 規格中沒有包含任何資訊。|加入 Analysis Services 支援的通訊協定功能的交涉 ProtocolCapabilities 標頭項目。|  
|Discover 方法所支援的 XML for Analysis (XMLA) 命令|XML for Analysis 1.1 規格支援下列命令：<br /><br /> [陳述式項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|Analysis Services 支援下列命令：<br /><br /> [Alter 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [備份項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [批次項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [BeginTransaction 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [Cancel 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [ClearCache 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [CommitTransaction 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [建立項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [刪除項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [DesignAggregations 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [Drop 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [插入項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [鎖定項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [MergePartitions 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [NotifyTableChange 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [處理項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [Restore 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [RollbackTransaction 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [陳述式項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [Subscribe 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [同步處理項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [Unlock 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [更新項目&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [UpdateCells 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|表格式資料列集中的資料行錯誤|沒有列在 XML for Analysis 1.1 規格中。|[錯誤](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)項目可由 Analysis Services 來報告錯誤的資料行中包含的項目[列](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)項目。|  
  
## <a name="see-also"></a>另請參閱
 [XML for Analysis &#40;XMLA&#41; 參考](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
