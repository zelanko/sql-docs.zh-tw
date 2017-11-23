---
title: "Analysis Services 結構描述資料列 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- SSAS, data access interfaces
- Analysis Services data access interfaces, schema rowsets
- data access interfaces [Analysis Services]
- XML for Analysis, schema rowsets
- rowsets [Analysis Services], retrieving schema rowsets
- retrieving schema rowsets
- XMLA, schema rowsets
- rowsets [Analysis Services]
- schema rowsets [Analysis Services], retrieving
ms.assetid: 820d4b59-d428-4616-b792-c848e5da407e
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0d6e87251e1ab08a87929cd3dba78a584e7c62fd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="analysis-services-schema-rowsets"></a>Analysis Services 結構描述資料列集
  結構描述資料列集是預先定義的資料表，其中包含有關 Analysis Services 物件和伺服器狀態的資訊，包括在伺服器上執行的資料庫結構描述、使用中工作階段、連接、命令及作業。 您可以在 SQL Server Management Studio 中的 XML/A 指令碼視窗內查詢結構描述資料列集資料表、針對結構描述資料列集執行 DMV 查詢，或是建立可併入結構描述資料列集資訊的自訂應用程式 (例如，擷取可用於建立報表之可用維度清單的報表應用程式)。  
  
> [!NOTE]  
>  如果您使用結構描述資料列中的 XML/A 指令碼，會在傳回的資訊*結果*參數[探索](../../analysis-services/xmla/xml-elements-methods-discover.md)根據所述的資料列集資料行配置化方法一節。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者支援 XML for Analysis 規格所需的資料列集。 XMLA 提供者也支援 OLE DB、OLE DB for OLAP 和 OLE DB for Data Mining 資料來源提供者的一些標準結構描述資料列集。 下列主題會描述支援的資料列集。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[XML for Analysis 結構描述資料列集](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)|描述 XMLA 提供者所支援的 XMLA 資料列集。|  
|[OLE DB 結構描述資料列集](../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)|描述 XMLA 提供者所支援的 OLE DB 結構描述資料列集。|  
|[OLE DB for OLAP 結構描述資料列集](../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)|描述 XMLA 提供者所支援的 OLE DB for OLAP 結構描述資料列集。|  
|[資料採礦結構描述資料列集](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)|描述 XMLA 提供者所支援的資料採礦結構描述資料列集。|  
  
## <a name="see-also"></a>請參閱＜  
 [多維度模型資料存取 &#40;Analysis Services-多維度資料 &#41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)   
 [使用動態管理檢視 &#40;DMV&#41; 監視 Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
