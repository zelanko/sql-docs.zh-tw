---
title: 資料採礦結構描述資料列 |Microsoft 文件
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
topic_type:
- apiref
- apinav
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- schema rowsets [Analysis Services]
- rowsets [Analysis Services], data mining
- data mining [Analysis Services], schema rowsets
ms.assetid: bd7d5df5-500b-4159-8467-880e141bc043
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9302e8dbafd31f4efb3b053ea5247f2b860dc8bc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033367"
---
# <a name="data-mining-schema-rowsets"></a>資料採礦結構描述資料列集
  正在執行的伺服器[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支援下列資料採礦結構描述資料列集。 若要檢查特定 XML/A 提供者是否支援特定的資料列集，請使用[DISCOVER_ENUMERATORS](../xml/discover-enumerators-rowset.md)含有資料列集[探索](../../xmla/xml-elements-methods-discover.md)方法。  
  
 在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中，資料採礦結構描述資料列集會以 Transact-SQL 語言中的資料表格式，在 $SYSTEM 結構描述中公開。 例如，在 Analysis Services 執行個體上的下列查詢會傳回在目前執行個體上可用的結構描述清單。  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>本節內容  
  
|結構描述資料列集|描述|  
|-------------------|-----------------|  
|[DMSCHEMA_MINING_COLUMNS 資料列集](dmschema-mining-columns-rowset.md)|描述部署在伺服器上所有定義之資料採礦模型的個別資料行。|  
|[DMSCHEMA_MINING_FUNCTIONS 資料列集](dmschema-mining-functions-rowset.md)|描述可與安裝在伺服器上的每個資料採礦演算法，搭配使用的預測函數與採礦函數。|  
|[DMSCHEMA_MINING_MODEL_CONTENT 資料列集](dmschema-mining-model-content-rowset.md)|允許用戶端應用程式瀏覽定型資料採礦模型的內容。|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML 資料列集](dmschema-mining-model-content-pmml-rowset.md)|傳回採礦模型內容的 XML (PMML 2.1) 表示。|  
|[DMSCHEMA_MINING_MODEL_XML 資料列集](dmschema-mining-model-xml-rowset.md)|傳回採礦模型的 XML (PMML 2.1) 結構。 這是與 DMSCHEMA_MINING_MODEL_PMML 相同的結構描述，是為了回溯相容性而保留的。|  
|[DMSCHEMA_MINING_MODELS 資料列集](dmschema-mining-models-rowset.md)|列舉在伺服器上部署的資料採礦模型。|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS 資料列集](dmschema-mining-service-parameters-rowset.md)|提供參數清單，這些參數可用以設定每個安裝在伺服器上的資料採礦演算法之行為。|  
|[DMSCHEMA_MINING_SERVICES 資料列集](dmschema-mining-services-rowset.md)|提供伺服器上可用之每個資料採礦演算法的描述。|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS 資料列集](dmschema-mining-structure-columns-rowset.md)|描述在伺服器上部署之所有採礦結構的個別資料行。|  
|[DMSCHEMA_MINING_STRUCTURES 資料列集](dmschema-mining-structures-rowset.md)|列舉採礦結構的資訊。|  
  
 此處所列的所有結構描述資料列所執行的伺服器支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 結構描述資料列集](../../schema-rowsets/analysis-services-schema-rowsets.md)   
 [查詢 SQL Server 系統目錄](https://technet.microsoft.com/en-us/library/ms189082\(v=sql.110\).aspx)   
 [查詢資料採礦結構描述資料列集&#40;Analysis Services-資料採礦&#41;](../../data-mining/data-mining-schema-rowsets-ssas.md)  
  
  