---
title: Analysis Services 結構描述資料列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 474de14a40b24fe113cebf1c933f7e28a351d5bd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227898"
---
# <a name="analysis-services-schema-rowsets"></a>Analysis Services 結構描述資料列集
  結構描述資料列集是預先定義的資料表，其中包含有關 Analysis Services 物件和伺服器狀態的資訊，包括在伺服器上執行的資料庫結構描述、使用中工作階段、連接、命令及作業。 您可以在 SQL Server Management Studio 中的 XML/A 指令碼視窗內查詢結構描述資料列集資料表、針對結構描述資料列集執行 DMV 查詢，或是建立可併入結構描述資料列集資訊的自訂應用程式 (例如，擷取可用於建立報表之可用維度清單的報表應用程式)。  
  
> [!NOTE]  
>  如果您使用結構描述資料列中的 XML/A 指令碼，會在傳回的資訊*結果*的參數[Discover](../xmla/xml-elements-methods-discover.md)結構方法是在此所述的資料列集資料行配置一節。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者支援 XML for Analysis 規格所需的資料列集。 XMLA 提供者也支援 OLE DB、OLE DB for OLAP 和 OLE DB for Data Mining 資料來源提供者的一些標準結構描述資料列集。 下列主題會描述支援的資料列集。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[XML for Analysis 結構描述資料列集](xml/xml-for-analysis-schema-rowsets.md)|描述 XMLA 提供者所支援的 XMLA 資料列集。|  
|[OLE DB 結構描述資料列集](ole-db/ole-db-schema-rowsets.md)|描述 XMLA 提供者所支援的 OLE DB 結構描述資料列集。|  
|[OLE DB for OLAP 結構描述資料列集](ole-db-olap/ole-db-for-olap-schema-rowsets.md)|描述 XMLA 提供者所支援的 OLE DB for OLAP 結構描述資料列集。|  
|[資料採礦結構描述資料列集](data-mining/data-mining-schema-rowsets.md)|描述 XMLA 提供者所支援的資料採礦結構描述資料列集。|  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型資料存取&#40;Analysis Services-多維度資料&#41;](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)   
 [使用動態管理檢視&#40;Dmv&#41;若要監視 Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
