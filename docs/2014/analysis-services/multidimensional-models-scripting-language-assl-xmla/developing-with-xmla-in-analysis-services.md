---
title: 在分析服務中使用XMLA開發 |微軟文檔
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, data mining
- commands [XML for Analysis]
- data mining [XML for Analysis]
- XMLA, data mining
- XML for Analysis, Analysis Services tasks
- XMLA, Analysis Services tasks
ms.assetid: 54445ee7-720c-4683-99a6-e75b3dcca904
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27b143a9cc5c888c6e464d300d2ccfea114ef9bc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2020
ms.locfileid: "80380679"
---
# <a name="developing-with-xmla-in-analysis-services"></a>在 Analysis Services 中使用 XMLA 進行開發
  XML for Analysis (XMLA) 是以 SOAP 為基礎的 XML 通訊協定，它是特別針對可透過 HTTP 連接存取的任何標準多維度資料來源進行通用資料存取而設計。 當與用戶端應用程式通訊時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用 XMLA 做為它唯一的通訊協定。 基本上，Analysis Services 支援的所有用戶端程式庫都會以 XMLA 編寫要求和回應。  
  
 身為開發人員，您可以使用 XMLA 將用戶端應用程式與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 整合，而沒有 .NET Framework 或 COM 介面的相依性。 包括裝載於廣大平台等應用程式需求，可透過 XMLA 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的 HTTP 連接來滿足。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 完全符合 XMLA 1.1 規格，但還擴充它以啟用資料定義、資料操作以及資料控制支援。 Analysis Services 延伸模組稱為 Analysis Services 指令碼語言 (ASSL)。 XMLA 與 ASSL 一起使用比 XMLA 單獨提供會啟用更多的功能。 有關 ASSL 的詳細資訊，請參閱[流量分析服務指令碼語言&#40;ASSL&#41;。](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[管理連接與工作階段 &#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)|描述如何連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，以及如何管理 XMLA 中的工作階段與 Statefulness。|  
|[處理錯誤和警告&#40;XMLA&#41;](handling-errors-and-warnings-xmla.md)|描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 如何為 XMLA 中的方法與命令傳回錯誤與警告資訊。|  
|[定義和識別物件&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)|描述物件識別碼與物件參考，以及如何在 XMLA 命令中使用識別碼與參考。|  
|[管理&#40;XMLA&#41;事務](managing-transactions-xmla.md)|詳細介紹了如何使用["開始事務](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla)"、[提交事務](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)和[回滾事務](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla)命令在當前 XMLA 會話上顯式定義和管理事務。|  
|[取消&#40;XMLA&#41;的命令](../multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|介紹如何使用[Cancel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)命令取消 XMLA 中的命令、會話和連接。|  
|[執行批次處理操作&#40;XMLA&#41;](performing-batch-operations-xmla.md)|描述如何使用[Batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)命令在同一事務中或作為單獨的事務，使用單個 XMLA [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法以串列或並行方式運行多個 XMLA 命令。|  
|[創建和更改物件&#40;XMLA&#41;](creating-and-altering-objects-xmla.md)|描述如何使用[創建](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)、[更改](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)和[刪除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla)命令以及分析服務指令碼語言 （ASSL） 元素來定義、更改或刪除[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]實例中的物件。|  
|[鎖定和解鎖資料庫&#40;XMLA&#41;](locking-and-unlocking-databases-xmla.md)|詳細說明如何使用[鎖定](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)和[解鎖](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)命令來鎖定和解鎖[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。|  
|[處理物件 (XMLA)](processing-objects-xmla.md)|描述如何使用[Process](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)命令處理[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件。|  
|[合併&#40;XMLA&#41;的分區](merging-partitions-xmla.md)|描述如何使用[MergeSs 命令](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla)合併[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]實例上的分區。|  
|[設計聚合&#40;XMLA&#41;](designing-aggregations-xmla.md)|描述如何使用["設計聚合"](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla)命令（在反覆運算模式或批次處理模式下）為 中的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]聚合設計。|  
|[備份、還原和同步處理資料庫 &#40;XMLA&#41;](backing-up-restoring-and-synchronizing-databases-xmla.md)|介紹如何使用[備份](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)和[還原](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)命令從備份檔案備份和還原[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。<br /><br /> 還介紹了如何使用["同步"](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)命令將資料庫與同[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]一實例或不同實例上的現有資料庫同步。|  
|[&#40;XMLA&#41;插入、更新和刪除成員](inserting-updating-and-dropping-members-xmla.md)|描述如何使用["插入](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)"、"[更新](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)"和["刪除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)"命令從啟用寫入的維度添加、更改或刪除成員。|  
|[更新儲存格&#40;XMLA&#41;](updating-cells-xmla.md)|描述如何使用[UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla)命令更改啟用寫入分區中的儲存格值。|  
|[管理緩存&#40;XMLA&#41;](managing-caches-xmla.md)|詳細介紹了如何使用[ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla)命令清除[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件的緩存。|  
|[監視&#40;XMLA&#41;跟蹤](monitoring-traces-xmla.md)|介紹如何使用["訂閱"](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla)命令訂閱和監視[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]實例上的現有跟蹤。|  
  
## <a name="data-mining-with-xmla"></a>使用 XMLA 進行資料採礦  
 XML for Analysis 完全支援資料採礦結構描述資料列集。 這些行集提供了使用["發現"](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)方法查詢資料採礦模型的資訊。 有關資料採礦架構行集的詳細資訊，請參閱[資料採礦架構行集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
 有關 DMX 的詳細資訊，請參閱[資料採礦擴展&#40;DMX&#41; 參考](/sql/dmx/data-mining-extensions-dmx-reference)。  
  
## <a name="namespace-and-schema"></a>命名空間與結構描述  
  
### <a name="namespace"></a>命名空間  
 在此規範中定義的架構使用 XML 命名空間和`https://schemas.microsoft.com/AnalysisServices/2003/Engine`標準縮寫"DDL"。  
  
### <a name="schema"></a>結構描述  
 對於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件定義語言，XML 結構描述定義語言 (XSD) 的定義是根據本章節中的結構描述元素與階層的定義。  
  
## <a name="extensibility"></a>擴充性  
 物件定義語言結構描述的擴充性是透過包括在所有物件的 `Annotation` 元素所提供。 這個元素可包含來自任何 XML 命名空間的任何有效 XML (但定義 DDL 的目標命名空間除外)，但受限於下列規則：  
  
-   XML 只能包含元素。  
  
-   每個元素都必須具有唯一的名稱。 通常建議 `Name` 的值參考目標命名空間。  
  
 加諸這些規則便可透過決策支援物件 (DSO) 9.0 以一組名稱/值配對來公開 `Annotation` 標記的內容。  
  
 `Annotation` 標記內部沒有用子元素括住的註解和空格，可能無法保留下來。 此外，所有元素都必須是可讀寫的；唯讀元素會被忽略。  
  
 物件定義語言結構描述會關閉，因為伺服器不允許替代在結構描述中定義之元素的衍生類型。 因此，伺服器只會接受在這裡所定義的元素集合，而不會接受其他的元素或是屬性。 未知的元素將使得 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 引擎引發錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [流量分析服務編寫指令碼語言&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [了解 Microsoft OLAP 架構](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
