---
title: 使用 Analysis Services 中的 XMLA 進行開發 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5a7af006d5d52002480844b8776d8262fa8ae202
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024645"
---
# <a name="developing-with-xmla-in-analysis-services"></a>在 Analysis Services 中使用 XMLA 進行開發
  XML for Analysis (XMLA) 是以 SOAP 為基礎的 XML 通訊協定，它是特別針對可透過 HTTP 連接存取的任何標準多維度資料來源進行通用資料存取而設計。 當與用戶端應用程式通訊時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用 XMLA 做為它唯一的通訊協定。 基本上，Analysis Services 支援的所有用戶端程式庫都會以 XMLA 編寫要求和回應。  
  
 身為開發人員，您可以使用 XMLA 將用戶端應用程式與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 整合，而沒有 .NET Framework 或 COM 介面的相依性。 包括裝載於廣大平台等應用程式需求，可透過 XMLA 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的 HTTP 連接來滿足。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 完全符合 XMLA 1.1 規格，但還擴充它以啟用資料定義、資料操作以及資料控制支援。 Analysis Services 延伸模組稱為 Analysis Services 指令碼語言 (ASSL)。 XMLA 與 ASSL 一起使用比 XMLA 單獨提供會啟用更多的功能。 如需有關 ASSL 的詳細資訊，請參閱[使用 Analysis Services 指令碼語言來開發&#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[管理連接與工作階段&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)|描述如何連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，以及如何管理 XMLA 中的工作階段與 Statefulness。|  
|[處理錯誤和警告&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/handling-errors-and-warnings-xmla.md)|描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 如何為 XMLA 中的方法與命令傳回錯誤與警告資訊。|  
|[定義和識別物件&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)|描述物件識別碼與物件參考，以及如何在 XMLA 命令中使用識別碼與參考。|  
|[管理交易&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-transactions-xmla.md)|詳細說明如何使用[BeginTransaction](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)， [CommitTransaction](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)，和[RollbackTransaction](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)命令來明確地定義和管理目前 XMLA 上的交易工作階段。|  
|[取消命令&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|描述如何使用[取消](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)命令來取消命令、 工作階段和 XMLA 中的連線。|  
|[執行批次作業&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)|描述如何使用[批次](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令來執行多個 XMLA 命令，以序列或是平行方式在相同交易內或當做個別的交易，使用的單一 XMLA [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)方法。|  
|[建立和改變物件&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md)|描述如何使用[建立](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)， [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)，和[刪除](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)命令以及 Analysis Services 指令碼語言 (ASSL) 元素，來定義、 變更或移除從物件[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體。|  
|[鎖定和解除鎖定資料庫&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/locking-and-unlocking-databases-xmla.md)|詳細說明如何使用[鎖定](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)和[Unlock](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)命令來鎖定和解除鎖定[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。|  
|[處理物件 & #40;XMLA & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)|描述如何使用[程序](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)命令處理[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件。|  
|[合併資料分割&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md)|描述如何使用[MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)命令合併資料分割上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體。|  
|[設計彙總&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)|描述如何使用[DesignAggregations](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)命令，在反覆或批次模式，來設計彙總中的彙總設計[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。|  
|[備份、 還原和同步處理資料庫 & #40;XMLA & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)|描述如何使用[備份](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)和[還原](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)命令來備份和還原[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫從備份檔案。<br /><br /> 同時描述如何使用[Synchronize](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令同步處理[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]與現有的資料庫相同的執行個體或不同的執行個體上的資料庫。|  
|[插入、 更新和卸除成員&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)|描述如何使用[插入](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[更新](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)，和[卸除](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)命令來新增、 變更或刪除從可寫入維度的成員。|  
|[更新資料格&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)|描述如何使用[UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)命令來變更啟用寫入的資料分割中的資料格的值。|  
|[管理快取&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-caches-xmla.md)|詳細說明如何使用[ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)命令以清除快取的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件。|  
|[監視追蹤&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/monitoring-traces-xmla.md)|描述如何使用[訂閱](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)命令來訂閱和監視現有的追蹤上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體。|  
  
## <a name="data-mining-with-xmla"></a>使用 XMLA 進行資料採礦  
 XML for Analysis 完全支援資料採礦結構描述資料列集。 這些資料列集提供的查詢使用資料採礦模型資訊[探索](../../analysis-services/xmla/xml-elements-methods-discover.md)方法。 如需有關資料採礦結構描述資料列集的詳細資訊，請參閱[資料採礦結構描述資料列集](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
 如需有關 DMX 的詳細資訊，請參閱[資料採礦延伸模組&#40;DMX&#41;參考](../../dmx/data-mining-extensions-dmx-reference.md)。  
  
## <a name="namespace-and-schema"></a>命名空間與結構描述  
  
### <a name="namespace"></a>네임스페이스  
 此規格中定義的結構描述會使用 XML 命名空間`http://schemas.microsoft.com/AnalysisServices/2003/Engine`以及標準縮寫"DDL"。  
  
### <a name="schema"></a>結構描述  
 對於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件定義語言，XML 結構描述定義語言 (XSD) 的定義是根據本章節中的結構描述元素與階層的定義。  
  
## <a name="extensibility"></a>擴充性  
 藉由提供的物件定義語言結構描述的擴充性**註解**包含所有物件的項目。 這個元素可包含來自任何 XML 命名空間的任何有效 XML (但定義 DDL 的目標命名空間除外)，但受限於下列規則：  
  
-   XML 只能包含元素。  
  
-   每個元素都必須具有唯一的名稱。 建議的值**名稱**參考目標命名空間。  
  
 加諸這些規則，讓內容**註解**標記可以公開為一組名稱/值組決策支援物件 (DSO) 9.0 透過。  
  
 註解和空格**註解**可能不會保留未加上含有子元素的標記。 此外，所有元素都必須是可讀寫的；唯讀元素會被忽略。  
  
 物件定義語言結構描述會關閉，因為伺服器不允許替代在結構描述中定義之元素的衍生類型。 因此，伺服器只會接受在這裡所定義的元素集合，而不會接受其他的元素或是屬性。 未知的元素將使得 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 引擎引發錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Analysis Services 開發的指令碼語言&#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [了解 Microsoft OLAP 架構](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
